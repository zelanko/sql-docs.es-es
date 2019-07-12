---
title: Instalar SQL Server Integration Services en Linux
description: En este artículo se describe cómo instalar SQL Server Integration Services (SSIS) en Linux.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: jroth
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 7c142b9b06e18acc3a97e6ae8b8fb7aa57a17ec1
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834671"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalar SQL Server Integration Services (SSIS) en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Siga los pasos descritos en este artículo para instalar SQL Server Integration Services (`mssql-server-is`) en Linux. Para obtener información sobre las características admitidas en esta versión de servicios de integración para Linux, consulte el [notas de la versión](sql-server-linux-release-notes.md).

Instalar a servidores de integración de SQL Server para su plataforma:

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Instalación de SSIS en Ubuntu
Para instalar el `mssql-server-is` del paquete en Ubuntu, siga estos pasos:

1. Importe las claves GPG repositorio público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrar el repositorio de Ubuntu de Microsoft SQL Server.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. Ejecute los comandos siguientes para instalar SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Después de instalar Integration Services, ejecute `ssis-conf`. Para obtener más información, consulte [configurar SSIS en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. Después de realiza la configuración, establezca la ruta de acceso.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Actualización de SSIS
Si ya tiene `mssql-server-is` instalado, puede actualizar a la versión más reciente con el siguiente comando:

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>Quitar SSIS
Para quitar `mssql-server-is`, puede ejecutar el comando siguiente:
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> Instalación de SSIS en RHEL
Para instalar el `mssql-server-is` empaquetar en RHEL, siga estos pasos:

1. Descargue el archivo de configuración del repositorio de Microsoft SQL Server Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. Ejecute los comandos siguientes para instalar SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. Después de la instalación, ejecute `ssis-conf`. Para obtener más información, consulte [configurar SSIS en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Una vez que se realiza la configuración, establezca la ruta de acceso.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Actualización de SSIS
Si ya tiene `mssql-server-is` instalado, puede actualizar a la versión más reciente con el siguiente comando:

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>Quitar SSIS
Para quitar `mssql-server-is`, puede ejecutar el comando siguiente:
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>Instalación desatendida
Para ejecutar una instalación desatendida al ejecutar `ssis-conf setup`, realice lo siguiente:
1.  Especifique el `-n` (sin preguntar) opción.
2.  Proporcione los valores necesarios mediante el establecimiento de variables de entorno.

En el siguiente ejemplo hace lo siguiente:
-   Instala SSIS.
-   Especifica la edición Developer, proporcionando un valor para el `SSIS_PID` variable de entorno.
-   Acepta los términos de licencia proporcionando un valor para el `ACCEPT_EULA` variable de entorno.
-   Ejecuta una instalación desatendida mediante la especificación de la `-n` (sin preguntar) opción.

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>Variables de entorno para la instalación desatendida

| Variable de entorno | Descripción |
|---|---|
| **ACCEPT_EULA** | Acepta el contrato de licencia de SQL Server cuando se establece en cualquier valor (por ejemplo, `Y`).|
| **SSIS_PID** | Establece la clave de producto o la edición de SQL Server. Estos son los valores posibles:<br/>Evaluation<br/>Desarrollador<br/>Express <br/>Web <br/>Estándar<br/>Enterprise <br/>Una clave de producto<br/><br/>Si especifica una clave de producto, la clave de producto debe tener el formato `#####-#####-#####-#####-#####`, donde `#` es una letra o un número.  |
| | |

## <a name="next-steps"></a>Pasos siguientes

Para ejecutar paquetes SSIS en Linux, consulte [extracción, transformación y carga de datos para SQL Server en Linux con SSIS](sql-server-linux-migrate-ssis.md).

Para configurar opciones adicionales de SSIS en Linux, consulte [configurar SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="related-content-about-ssis-on-linux"></a>Contenido relacionado sobre SSIS en Linux
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Configurar SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md)
-   [Ejecución en Linux con cron de paquetes de programación de SQL Server Integration Services](sql-server-linux-schedule-ssis-packages.md)
