---
title: Introducción a SQL Server en Red Hat Enterprise Linux
titleSuffix: SQL Server
description: En este inicio rápido, se muestra cómo instalar SQL Server 2017 o SQL Server 2019 en Red Hat Enterprise Linux y, después, crear y consultar una base de datos con sqlcmd.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: b94ea0ef8956e7807f075da548ae817dc6a205df
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531373"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>Inicio rápido: instalar SQL Server y crear una base de datos en Red Hat

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En este inicio rápido, instalará SQL Server 2017 o SQL Server 2019 en Red Hat Enterprise Linux (RHEL). Después, se conectará con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En este inicio rápido, instalará SQL Server 2019 en Red Hat Enterprise Linux (RHEL) 7.3+. Después, se conectará con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

::: moniker-end

> [!TIP]
> Este tutorial necesita la intervención del usuario y una conexión a Internet. Para obtener más información sobre los procedimientos de instalación [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline), vea la [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

Necesita un equipo con RHEL 7.3, 7.4, 7.5 o 7.6 con un **mínimo de 2 GB** de memoria.

Para instalar Red Hat Enterprise Linux en su propio equipo, vaya a [https://access.redhat.com/products/red-hat-enterprise-linux/evaluation](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation). También puede crear máquinas virtuales con RHEL en Azure. Vea [Creación y administración de máquinas virtuales Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm) y use `--image RHEL` en la llamada a `az vm create`.

Si anteriormente instaló una versión CTP o RC de SQL Server, necesita quitar el repositorio anterior antes de seguir estos pasos. Para obtener más información, vea [Configurar repositorios de Linux para SQL Server 2017 y 2019](sql-server-linux-change-repo.md).

Para conocer otros requisitos del sistema, vea [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en RHEL, ejecute los comandos siguientes en un terminal para instalar el paquete **mssql-server**:

1. Descargue el archivo de configuración del repositorio de Red Hat de Microsoft SQL Server 2017:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > Si quiere instalar SQL Server 2019, debe registrar en su lugar el repositorio de SQL Server 2019. Use el comando siguiente para las instalaciones de SQL Server 2019:
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   > ```

2. Ejecute los comandos siguientes para instalar SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Cuando finalice la instalación del paquete, ejecute **mssql-conf setup** y siga las indicaciones para establecer la contraseña de administrador del sistema y elegir la edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Las siguientes ediciones de SQL Server 2017 tienen licencia gratuita: Evaluation, Developer y Express.

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta del administrador del sistema (longitud mínima de 8 caracteres, incluidas mayúsculas y minúsculas, dígitos en base 10 o símbolos no alfanuméricos).

4. Cuando finalice la configuración, compruebe que el servicio se esté ejecutando:

   ```bash
   systemctl status mssql-server
   ```

5. Para permitir las conexiones remotas, abra el puerto de SQL Server en el firewall en RHEL. El puerto de SQL Server predeterminado es TCP 1433. Si usa **FirewallD** para el firewall, puede usar los comandos siguientes:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

En este momento, SQL Server se ejecuta en el equipo con RHEL y está listo para usarse.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en RHEL, ejecute los comandos siguientes en un terminal para instalar el paquete **mssql-server**:

1. Descargue el archivo de configuración del repositorio de Red Hat de Microsoft SQL Server 2019:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```

2. Ejecute los comandos siguientes para instalar SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Cuando finalice la instalación del paquete, ejecute **mssql-conf setup** y siga las indicaciones para establecer la contraseña de administrador del sistema y elegir la edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta del administrador del sistema (longitud mínima de 8 caracteres, incluidas mayúsculas y minúsculas, dígitos en base 10 o símbolos no alfanuméricos).

4. Cuando finalice la configuración, compruebe que el servicio se esté ejecutando:

   ```bash
   systemctl status mssql-server
   ```

5. Para permitir las conexiones remotas, abra el puerto de SQL Server en el firewall en RHEL. El puerto de SQL Server predeterminado es TCP 1433. Si usa **FirewallD** para el firewall, puede usar los comandos siguientes:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

En este momento, SQL Server 2019 se ejecuta en el equipo con RHEL y está listo para usarse.

::: moniker-end

## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, necesita conectarse con una herramienta que pueda ejecutar instrucciones Transact-SQL en SQL Server. En los pasos siguientes, se instalan las herramientas de línea de comandos de SQL Server [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

1. Descargue el archivo de configuración del repositorio de Red Hat de Microsoft.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. Si tiene instalada una versión anterior de **mssql-tools**, quite los paquetes unixODBC anteriores.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Ejecute los comandos siguientes para instalar **mssql-tools** con el paquete de desarrollador de unixODBC.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. Por comodidad, agregue `/opt/mssql-tools/bin/` a la variable de entorno **PATH**. De este modo, podrá ejecutar las herramientas sin especificar la ruta de acceso completa. Ejecute los comandos siguientes para modificar la variable **PATH**, tanto para las sesiones de inicio de sesión como para las sesiones interactivas o sin inicio de sesión:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
