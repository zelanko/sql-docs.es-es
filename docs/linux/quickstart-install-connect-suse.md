---
title: "Introducción a SQL Server 2017 en SUSE Linux Enterprise Server | Documentos de Microsoft"
description: "Este tutorial de inicio rápido muestra cómo instalar SQL Server 2017 en SUSE Linux Enterprise Server y, a continuación, crear y consultar una base de datos con sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 6d18cbe5b20882581afa731ce5d207cbbc69be6c
ms.openlocfilehash: a15f88d8bc7d7684e8e8d0014bb24a082c5b0be2
ms.contentlocale: es-es
ms.lasthandoff: 10/21/2017

---
# <a name="install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Instalar a SQL Server y crear una base de datos en SUSE Linux Enterprise Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tutorial de inicio rápido, en primer lugar instale 2017 de SQL Server en SUSE Linux Enterprise Server (SLES) v12 SP2. A continuación, conecte con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener una máquina SLES v12 SP2 con **3,25 GB como mínimo** de memoria. El sistema de archivos debe ser **XFS** o **EXT4**. Otros los sistemas de archivos, como **BTRFS**, no son compatibles.

Para instalar SUSE Linux Enterprise Server en su propio equipo, vaya a [https://www.suse.com/products/server](https://www.suse.com/products/server). También puede crear máquinas virtuales SLES en Azure. Vea [crear y administrar máquinas virtuales de Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)y usar `--image SLES` en la llamada a `az vm create`.

> [!NOTE]
> En este momento, el [subsistema de Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 no se admite como un destino de instalación.

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en SLES, ejecute los siguientes comandos en un terminal para instalar el **mssql server** paquete:

> [!IMPORTANT]
> Si anteriormente ha instalado una versión de CTP o versión RC de 2017 de SQL Server, primero debe quitar el antiguo repositorio antes de registrar uno de los repositorios de GA. Para obtener más información, consulte [cambiar repositorios desde el repositorio de vista previa en el repositorio de GA](sql-server-linux-change-repo.md).

1. Descargue el archivo de configuración del repositorio de Microsoft SQL Server SLES:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   sudo zypper --gpg-auto-import-keys refresh
   ```

   > [!NOTE]
   > Esto es el repositorio de actualización acumulativa (CU). Para obtener más información acerca de las opciones de repositorio y sus diferencias, vea [cambiar repositorios de origen](sql-server-linux-setup.md#repositories).

1. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo zypper install -y mssql-server
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

1. Si tiene previsto conectarse de forma remota, también tendrá que abrir el puerto TCP de SQL Server (predeterminado: 1433) en el firewall. Si se usa el firewall de SuSE, debe editar el **/etc/sysconfig/SuSEfirewall2** archivo de configuración. Modificar el **FW_SERVICES_EXT_TCP** entrada que se va a incluir el número de puerto de SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

En este momento, SQL Server está ejecutando en el equipo SLES y está listo para usarse.

## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, debe conectarse con una herramienta que se puede ejecutar instrucciones Transact-SQL en SQL Server. Los siguientes pasos instalación las herramientas de línea de comandos de SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

1. Agregue el repositorio de Microsoft SQL Server para Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instalar **mssql herramientas** con el paquete de desarrollador de unixODBC.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. Para mayor comodidad, agregue `/opt/mssql-tools/bin/` a su **ruta de acceso** variable de entorno. Esto le permite ejecutar las herramientas sin especificar la ruta de acceso completa. Ejecute los comandos siguientes para modificar el **ruta de acceso** para las sesiones de inicio de sesión y las sesiones / no-inicio de sesión interactivo:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** es simplemente una herramienta para conectarse a SQL Server para ejecutar consultas y realizar tareas de administración y desarrollo. Otras herramientas incluyen [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md) y [código de Visual Studio](sql-server-linux-develop-use-vscode.md).

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]

