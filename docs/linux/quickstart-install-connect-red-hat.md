---
title: Introducción a SQL Server 2017 en Red Hat Enterprise Linux | Documentos de Microsoft
description: Este tutorial rápido muestra cómo instalar SQL Server 2017 en Red Hat Enterprise Linux y, a continuación, crear y consultar una base de datos con sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.workload: Active
ms.openlocfilehash: 145f829b3baf5392ed3d6ed93db43b01603b9b8f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>Inicio rápido: Instalar SQL Server y crear una base de datos en Red Hat

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial rápido, primero instalar SQL Server 2017 en Red Hat Enterprise Linux (RHEL) 7.3 +. A continuación, tendrá que conectar con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener un 7.3 RHEL o máquina 7.4 con **al menos 2 GB** de memoria.

Para instalar Red Hat Enterprise Linux en su propio equipo, vaya a [ http://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation). También puede crear máquinas virtuales RHEL en Azure. Vea [crear y administrar máquinas virtuales de Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)y usar `--image RHEL` en la llamada a `az vm create`.

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en RHEL, ejecute los siguientes comandos en un terminal para instalar el **mssql server** paquete:

> [!IMPORTANT]
> Si anteriormente ha instalado una versión de CTP o versión RC de 2017 de SQL Server, primero debe quitar el antiguo repositorio antes de registrar uno de los repositorios de GA. Para obtener más información, consulte [cambiar repositorios desde el repositorio de vista previa en el repositorio de GA](sql-server-linux-change-repo.md).

1. Descargue el archivo de configuración del repositorio de Red Hat de Microsoft SQL Server:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!NOTE]
   > Esto es el repositorio de actualización acumulativa (CU). Para obtener más información acerca de las opciones de repositorio y sus diferencias, vea [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

1. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

1. Cuando finalice de instalación el paquete, ejecute **el programa de instalación de mssql-conf** y siga las indicaciones para establecer la contraseña de SA y elija su edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```
   > [!TIP]
   > Si está tratando de 2017 de SQL Server en este tutorial, libremente tienen licencia las siguientes ediciones: Evaluation, Developer y Express.

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta SA (mínimo 8 caracteres, incluidas letras mayúsculas y minúsculas, dígitos de base 10 o símbolos que no sean alfanuméricos).

1. Una vez que se realiza la configuración, compruebe que el servicio se está ejecutando:

   ```bash
   systemctl status mssql-server
   ```
   
1. Para permitir conexiones remotas, abra el puerto de SQL Server en el firewall en RHEL. El puerto de SQL Server predeterminado es TCP 1433. Si utilizas **FirewallD** para el firewall, puede usar los siguientes comandos:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

En este momento, SQL Server se ejecuta en el equipo RHEL y está listo para usarse.

## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, debe conectarse con una herramienta que se puede ejecutar instrucciones Transact-SQL en SQL Server. Los siguientes pasos instalación las herramientas de línea de comandos de SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

1. Descargue el archivo de configuración del repositorio de Microsoft Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. Si tiene una versión anterior de **mssql herramientas** instalado, quite los paquetes de unixODBC anteriores.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Ejecute los comandos siguientes para instalar **mssql herramientas** con el paquete de desarrollador de unixODBC.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. Para mayor comodidad, agregue `/opt/mssql-tools/bin/` a su **ruta de acceso** variable de entorno. Esto le permite ejecutar las herramientas sin especificar la ruta de acceso completa. Ejecute los comandos siguientes para modificar el **ruta de acceso** para las sesiones de inicio de sesión y las sesiones / no-inicio de sesión interactivo:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** es simplemente una herramienta para conectarse a SQL Server para ejecutar consultas y realizar tareas de administración y desarrollo. Otras herramientas incluyen:
>
> * [SQL Server Operations Studio (versión preliminar)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * [Código de Visual Studio](sql-server-linux-develop-use-vscode.md).
> * [mssql-cli (versión preliminar)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
