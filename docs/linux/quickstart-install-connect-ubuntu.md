---
title: Introducción a SQL Server 2017 en Ubuntu | Microsoft Docs
description: Este inicio rápido muestra cómo instalar SQL Server 2017 en Ubuntu y, a continuación, crear y consultar una base de datos con sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: ebe7da1e1024cefc14c52d0a02e0517b764c8d07
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057323"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>Inicio rápido: Instalar SQL Server y crear una base de datos en Ubuntu

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial, primero instale SQL Server 2017 en Ubuntu 16.04. A continuación, tendrá que conectar con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, vea [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener una máquina Ubuntu 16.04 con **al menos 2 GB** de memoria.

Para instalar Ubuntu en su propio equipo, vaya a [ http://www.ubuntu.com/download/server ](http://www.ubuntu.com/download/server). También puede crear máquinas virtuales Ubuntu en Azure. Consulte [crear y administrar máquinas virtuales Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> En este momento, el [subsistema Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 no se admite como destino de la instalación.

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en Ubuntu, ejecute los siguientes comandos en un terminal para instalar el **mssql-server** paquete.

> [!IMPORTANT]
> Si anteriormente ha instalado un CTP o la versión RC de SQL Server 2017, primero debe quitar el repositorio antiguo antes de registrar uno de los repositorios de GA. Para obtener más información, consulte [cambiar repositorios desde el repositorio de vista previa en el repositorio GA](sql-server-linux-change-repo.md).

1. Importe las claves GPG repositorio público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registrar el repositorio de Microsoft SQL Server Ubuntu:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!NOTE]
   > Este es el repositorio de actualización acumulativa (CU). Para obtener más información acerca de las opciones de repositorio y sus diferencias, vea [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

1. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

1. Después de finaliza de la instalación de paquetes, ejecutar **el programa de instalación de mssql-conf** y siga las indicaciones para establecer la contraseña de SA y seleccione su edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Si está tratando de SQL Server 2017 en este tutorial, se ofrece licencias gratuitamente las siguientes ediciones: Evaluation, Developer y Express.

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta de SA (caracteres de longitud de 8 como mínimo, incluidas letras mayúsculas y minúsculas, dígitos de base 10 o símbolos no alfanuméricos).

1. Una vez que se realiza la configuración, compruebe que el servicio se está ejecutando:

   ```bash
   systemctl status mssql-server
   ```

1. Si tiene previsto conectarse de forma remota, deberá abrir el puerto TCP de SQL Server (predeterminado: 1433) en el firewall.

En este momento, SQL Server se está ejecutando en la máquina Ubuntu y está listo para usarse.

## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, debe conectarse con una herramienta que puede ejecutar instrucciones Transact-SQL en SQL Server. Los pasos siguientes instalan las herramientas de línea de comandos de SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

Use los pasos siguientes para instalar el **mssql-tools** en Ubuntu. 

1. Importe las claves GPG repositorio público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registrar el repositorio de Microsoft Ubuntu.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Actualizar la lista de orígenes y ejecute el comando de instalación con el paquete de desarrollador de unixODBC.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Para actualizar a la versión más reciente de **mssql-tools** ejecute los siguientes comandos:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Opcional**: agregar `/opt/mssql-tools/bin/` a su **ruta** variable de entorno en un shell de bash.

   Para realizar **sqlcmd y bcp** accesible desde el shell de bash para sesiones de inicio de sesión, modifique su **ruta de acceso** en el **~/.bash_profile** archivo con el siguiente comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para realizar **sqlcmd y bcp** accesible desde el shell de bash para sesiones/no-inicio de sesión interactivo, modifique la **ruta de acceso** en el **~/.bashrc** archivo con el siguiente comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** es simplemente una herramienta para conectarse a SQL Server para ejecutar consultas y realizar tareas de administración y desarrollo. Otras herramientas son:
>
> * [SQL Server Operations Studio (versión preliminar)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-manage-ssms.md)
> * [Código de Visual Studio](sql-server-linux-develop-use-vscode.md).
> * [mssql-cli (versión preliminar)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
