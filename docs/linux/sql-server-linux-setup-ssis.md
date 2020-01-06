---
title: Instalación de SQL Server Integration Services en Linux
description: En este artículo se explica cómo instalar SQL Server Integration Services (SSIS) en Linux.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 0ee4c32568a52f5eb7664fa8f22250370f46f033
ms.sourcegitcommit: a92fa97e7d3132ea201e4d86c76ac39cd564cd3c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2019
ms.locfileid: "75325482"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalación de SQL Server Integration Services (SSIS) en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Siga los pasos de este artículo para instalar SQL Server Integration Services (`mssql-server-is`) en Linux. Para obtener información sobre las características admitidas en esta versión de Integration Services para Linux, vea las [Notas de la versión](sql-server-linux-release-notes.md).

Instale SQL Server Integration Services para la plataforma:

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Instalación de SSIS en Ubuntu
Para instalar el paquete `mssql-server-is` en Ubuntu, siga estos pasos:

1. Importe las claves de GPG del repositorio público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registre el repositorio de Ubuntu de Microsoft SQL Server.
<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"
   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```
::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"
   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   ```
::: moniker-end
3. Ejecute los comandos siguientes para instalar SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Después de instalar Integration Services, ejecute `ssis-conf`. Para obtener más información, vea [Configuración de SSIS en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. Una vez finalizada la configuración, establezca la ruta de acceso.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Actualización de SSIS
Si ya tiene `mssql-server-is` instalado, puede actualizar a la versión más reciente con el comando siguiente:

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>Eliminación de SSIS
Para quitar `mssql-server-is`, puede ejecutar el siguiente comando:
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> Instalación de SSIS en RHEL
Para instalar el paquete `mssql-server-is` en RHEL, siga estos pasos:

1. Descargue el archivo de configuración del repositorio de Red Hat de Microsoft SQL Server.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"
   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```
::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"
   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```
::: moniker-end
1. Ejecute los comandos siguientes para instalar SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. Después de la instalación, ejecute `ssis-conf`. Para obtener más información, vea [Configuración de SSIS en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Una vez finalizada la configuración, establezca la ruta de acceso.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Actualización de SSIS
Si ya tiene `mssql-server-is` instalado, puede actualizar a la versión más reciente con el comando siguiente:

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>Eliminación de SSIS
Para quitar `mssql-server-is`, puede ejecutar el siguiente comando:
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>Instalación desatendida
Para realizar una instalación desatendida al ejecutar `ssis-conf setup`, haga lo siguiente:
1.  Especifique la opción `-n` (sin solicitud).
2.  Proporcione los valores necesarios al establecer las variables de entorno.

El siguiente ejemplo hace lo siguiente:
-   Instala SSIS.
-   Especifica la edición Developer al proporcionar un valor para la variable de entorno `SSIS_PID`.
-   Acepta el CLUF al proporcionar un valor para la variable de entorno `ACCEPT_EULA`.
-   Ejecuta una instalación desatendida mediante la especificación de la opción `-n` (sin solicitud).

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>Variables de entorno para instalación desatendida

| Variable de entorno | Descripción |
|---|---|
| **ACCEPT_EULA** | Acepta el contrato de licencia de SQL Server cuando se establece en cualquier valor (por ejemplo, `Y`).|
| **SSIS_PID** | Establece la edición de SQL Server o la clave de producto. Estos son los valores posibles:<br/>Evaluación<br/>Desarrollador<br/>Express <br/>Web <br/>Estándar<br/>Enterprise <br/>Una clave de producto<br/><br/>Si especifica una clave de producto, esta debe tener el formato `#####-#####-#####-#####-#####`, donde `#` es una letra o un número.  |
| | |

## <a name="next-steps"></a>Pasos siguientes

Para ejecutar paquetes en Linux, vea [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md).

Para configurar opciones adicionales de SSIS en Linux, vea [Configuración de SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="related-content-about-ssis-on-linux"></a>Contenido relacionado sobre SSIS en Linux
-   [Extracción, transformación y carga de datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Configurar SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md)
-   [Programación de la ejecución de paquetes de SQL Server Integration Services en Linux con cron](sql-server-linux-schedule-ssis-packages.md)
