---
title: Instalar SQL Server Integration Services en Linux | Documentos de Microsoft
description: "En este tema se describe cómo instalar SQL Server Integration Services en Linux."
author: leolimsft
ms.author: lle
manager: craigg
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c3943870ec10b8430ac4819398908c5459a8b03c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalar SQL Server Integration Services (SSIS) en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Siga los pasos de este artículo para instalar SQL Server Integration Services (`mssql-server-is`) en Linux. Para obtener información sobre las características admitidas en esta versión de servicios de integración para Linux, consulte la [notas de la versión](sql-server-linux-release-notes.md).

Instalar a servidores de integración de SQL Server para su plataforma:

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)



## <a name="ubuntu"></a>Instalar SSIS en Ubuntu
Para instalar el `mssql-server-is` el paquete en Ubuntu, siga estos pasos:


1.  Importar las claves GPG repositorio público.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```


2.  Registrar el repositorio de Microsoft SQL Server Ubuntu.

    ```bash
    curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list | sudo tee /etc/apt/sources.list.d/mssql-server.list
    ```


3.  Ejecute los comandos siguientes para instalar SQL Server Integration Services.

    ```bash
    sudo apt-get update
    sudo apt-get install -y mssql-server-is
    ```


4.  Después de instalar Integration Services, ejecutar `ssis-conf`.

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


5.  Después de realiza la configuración, establezca la ruta de acceso.

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


Si ya tiene `mssql-server-is` instalado, puede actualizar a la versión más reciente con el siguiente comando:

```bash
sudo apt-get install mssql-server-is
```


Para quitar `mssql-server-is`, puede ejecutar el comando siguiente:
```bash
sudo apt-get remove msssql-server-is
```



## <a name="RHEL"></a>Instalar SSIS en RHEL
Para instalar el `mssql-server-is` el paquete en RHEL, siga estos pasos:


1.  ENTRAR en el modo de superusuario.

    ```bash
    sudo su
    ```


2.  Descargue el archivo de configuración del repositorio de Microsoft SQL Server Red Hat.

    ```bash
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
    ```


3.  Salir del modo de superusuario.

    ```bash
    exit
    ```


4.  Ejecute los comandos siguientes para instalar SQL Server Integration Services.

    ```bash
    sudo yum install -y mssql-server-is
    ```


5.  Después de la instalación, vuelva a ejecutar `ssis-conf`.

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


6.  Una vez que se realiza la configuración, establezca la ruta de acceso.

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


Si ya tiene `mssql-server-is` instalado, puede actualizar a la versión más reciente con el siguiente comando:

```bash
sudo yum update mssql-server-is
```


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
