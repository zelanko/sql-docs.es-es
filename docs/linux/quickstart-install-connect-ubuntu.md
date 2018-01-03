---
title: "Introducción a SQL Server 2017 en Ubuntu | Documentos de Microsoft"
description: "Este tutorial rápido muestra cómo instalar SQL Server 2017 en Ubuntu y, a continuación, crear y consultar una base de datos con sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.workload: Active
ms.openlocfilehash: 17d6ebb3df10a5bc8b5801c11cc8ac12cde372a2
ms.sourcegitcommit: 73043fe1ac5d60b67e33b44053c0a7733b98bc3d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/23/2017
---
# <a name="install-sql-server-and-create-a-database-on-ubuntu"></a>Instalar a SQL Server y crear una base de datos en Ubuntu

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tutorial rápido, primero instalar SQL Server 2017 en Ubuntu 16.04. A continuación, conecte con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

Debe tener una máquina Ubuntu 16.04 con **al menos 2 GB** de memoria.

Para instalar Ubuntu en su propio equipo, vaya a [http://www.ubuntu.com/download/server](http://www.ubuntu.com/download/server). También puede crear máquinas virtuales de Ubuntu en Azure. Vea [crear y administrar máquinas virtuales de Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> En este momento, el [subsistema de Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 no se admite como un destino de instalación.

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en Ubuntu, ejecute los siguientes comandos en un terminal para instalar el **mssql server** paquete.

> [!IMPORTANT]
> Si anteriormente ha instalado una versión de CTP o versión RC de 2017 de SQL Server, primero debe quitar el antiguo repositorio antes de registrar uno de los repositorios de GA. Para obtener más información, consulte [cambiar repositorios desde el repositorio de vista previa en el repositorio de GA](sql-server-linux-change-repo.md).

1. Importar las claves GPG repositorio público:

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre el repositorio de Microsoft SQL Server Ubuntu:

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!NOTE]
   > Esto es el repositorio de actualización acumulativa (CU). Para obtener más información acerca de las opciones de repositorio y sus diferencias, vea [cambiar repositorios de origen](sql-server-linux-setup.md#repositories).

1. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
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

1. Si tiene previsto conectarse de forma remota, también tendrá que abrir el puerto TCP de SQL Server (predeterminado: 1433) en el firewall.

En este momento, SQL Server se ejecuta en su equipo Ubuntu y está listo para usar!

## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, debe conectarse con una herramienta que se puede ejecutar instrucciones Transact-SQL en SQL Server. Los siguientes pasos instalación las herramientas de línea de comandos de SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

1. Importar las claves GPG repositorio público:

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre el repositorio de Microsoft Ubuntu:

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
   ```

1. Actualizar la lista de orígenes y ejecute el comando de instalación con el paquete de desarrollador de unixODBC:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-tools unixodbc-dev
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
> * [Studio de operaciones de SQL Server (versión preliminar)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * [Código de Visual Studio](sql-server-linux-develop-use-vscode.md).
> * [MSSQL-cli (versión preliminar)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
