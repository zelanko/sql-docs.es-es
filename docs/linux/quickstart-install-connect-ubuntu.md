---
title: 'Ubuntu: Instalación de SQL Server en Linux'
description: En este inicio rápido se explica cómo instalar SQL Server 2017 o SQL Server 2019 en Ubuntu y, después, crear y consultar una base de datos con sqlcmd.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: seo-lt-2019
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: df3609c5bf4f31ee8a32992127681d42609b9528
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558430"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>Inicio rápido: Instalación de SQL Server y creación de una base de datos en Ubuntu
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]


<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En este inicio rápido, instalará SQL Server 2017 o SQL Server 2019 en Ubuntu 16.04. Después, se conectará con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En este inicio rápido, instalará SQL Server 2019 en Ubuntu 16.04. Después, se conectará con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

::: moniker-end

> [!TIP]
> Este tutorial necesita la intervención del usuario y una conexión a Internet. Si le interesan los procedimientos de instalación desatendida o sin conexión, consulte la [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

Debe tener un equipo Ubuntu 16.04 con **al menos 2 GB** de memoria.

Para instalar Ubuntu 16.04 en su propio equipo, vaya a [http://releases.ubuntu.com/xenial/](http://releases.ubuntu.com/xenial/). También puede crear máquinas virtuales de Ubuntu en Azure. Consulte [Creación y administración de máquinas virtuales Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> En este momento, no se admite como destino de instalación el [subsistema de Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10.

Para conocer otros requisitos del sistema, vea [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

> [!NOTE]
> Ubuntu 18.04 todavía no se admite oficialmente, pero la ejecución de SQL Server es posible con [modificaciones](https://blogs.msdn.microsoft.com/sql_server_team/installing-sql-server-2017-for-linux-on-ubuntu-18-04-lts/).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en Ubuntu, ejecute los siguientes comandos en un terminal para instalar el paquete **mssql-server**.

1. Importe las claves de GPG del repositorio público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registre el repositorio de Ubuntu de Microsoft SQL Server:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > Si quiere instalar SQL Server 2019, debe registrar en su lugar el repositorio de SQL Server 2019. Use el comando siguiente para las instalaciones de SQL Server 2019:
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   > ```

3. Ejecute los comandos siguientes para instalar SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. Cuando finalice la instalación del paquete, ejecute **mssql-conf setup** y siga las indicaciones para establecer la contraseña de administrador del sistema y elegir la edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Las siguientes ediciones de SQL Server 2017 tienen licencia gratuita: Evaluation, Developer y Express.

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta del administrador del sistema (longitud mínima de 8 caracteres, incluidas mayúsculas y minúsculas, dígitos en base 10 o símbolos no alfanuméricos).

5. Cuando finalice la configuración, compruebe que el servicio se esté ejecutando:

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. Si planea conectarse de forma remota, es posible que también tenga que abrir el puerto TCP de SQL Server (valor predeterminado: 1433) en el firewall.

En este momento, SQL Server se está ejecutando en el equipo Ubuntu y está listo para usarse.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en Ubuntu, ejecute los siguientes comandos en un terminal para instalar el paquete **mssql-server**.

1. Importe las claves de GPG del repositorio público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registre el repositorio de Ubuntu de Microsoft SQL Server para SQL Server 2019:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   ```

3. Ejecute los comandos siguientes para instalar SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. Cuando finalice la instalación del paquete, ejecute **mssql-conf setup** y siga las indicaciones para establecer la contraseña de administrador del sistema y elegir la edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta del administrador del sistema (longitud mínima de 8 caracteres, incluidas mayúsculas y minúsculas, dígitos en base 10 o símbolos no alfanuméricos).

5. Cuando finalice la configuración, compruebe que el servicio se esté ejecutando:

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. Si planea conectarse de forma remota, es posible que también tenga que abrir el puerto TCP de SQL Server (valor predeterminado: 1433) en el firewall.

En este momento, SQL Server 2019 se está ejecutando en el equipo Ubuntu y está listo para usarse.

::: moniker-end

## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, necesita conectarse con una herramienta que pueda ejecutar instrucciones Transact-SQL en SQL Server. En los pasos siguientes, se instalan las herramientas de línea de comandos de SQL Server [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

Siga estos pasos para instalar **mssql-tools** en Ubuntu. 

1. Importe las claves de GPG del repositorio público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre el repositorio de Ubuntu de Microsoft.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Actualice la lista de orígenes y ejecute el comando de instalación con el paquete para desarrolladores de unixODBC.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Para actualizar a la versión más reciente de **mssql-tools**, ejecute los siguientes comandos:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Opcional**: agregue `/opt/mssql-tools/bin/` a la variable de entorno **PATH** en un shell de Bash.

   Para que **sqlcmd/bcp** sea accesible desde el shell de Bash para inicios de sesión, modifique la variable **PATH** en el archivo **~/.bash_profile** con el comando siguiente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para que **sqlcmd/bcp** sea accesible desde el shell de Bash para sesiones interactivas o que no sean de inicio de sesión, modifique la variable **PATH** en el archivo **~/.bashrc** con el comando siguiente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
