---
title: Instalar SQL Server Integration Services en Linux | Documentos de Microsoft
description: "En este tema se describe cómo instalar SQL Server Integration Services (SSIS) en Linux."
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: d265d1c4fa25f10c58e321cef06cf293fdce5ac5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalar SQL Server Integration Services (SSIS) en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Siga los pasos de este artículo para instalar SQL Server Integration Services (`mssql-server-is`) en Linux. Para obtener información sobre las características admitidas en esta versión de servicios de integración para Linux, consulte la [notas de la versión](sql-server-linux-release-notes.md).

Instalar a servidores de integración de SQL Server para su plataforma:

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a>Instalar SSIS en Ubuntu
Para instalar el `mssql-server-is` el paquete en Ubuntu, siga estos pasos:

1. Importar las claves GPG repositorio público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrar el repositorio de Microsoft SQL Server Ubuntu.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. Ejecute los comandos siguientes para instalar SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Después de instalar Integration Services, ejecutar `ssis-conf`. Para obtener más información, consulte [configurar SSIS en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

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
sudo apt-get remove msssql-server-is
```

## <a name="RHEL"></a>Instalar SSIS en RHEL
Para instalar el `mssql-server-is` el paquete en RHEL, siga estos pasos:

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
sudo yum remove msssql-server-is
```




## <a name="run-a-package"></a>Ejecutar un paquete
Copie el paquete SSIS en el equipo Linux. A continuación, utilice el siguiente comando para ejecutar el paquete.

```bash
dtexec /F <package name> /DE <protection password>
```



## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de cómo usar SSIS en Linux para extraer, transformar y cargar los datos, vea [extraer, transformar y cargar datos de SQL Server en Linux con SSIS](sql-server-linux-migrate-ssis.md).
