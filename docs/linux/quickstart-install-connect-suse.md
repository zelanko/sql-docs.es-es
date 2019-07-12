---
title: Introducción a SQL Server en SUSE Linux Enterprise Server
titleSuffix: SQL Server
description: Este inicio rápido muestra cómo instalar SQL Server 2017 ni SQL Server 2019 en SUSE Linux Enterprise Server y, a continuación, crear y consultar una base de datos con sqlcmd.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: 19f74067db365fd9bdc867b97cef6ee5aa5162d8
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833249"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Inicio rápido: Instalar a SQL Server y crear una base de datos en SUSE Linux Enterprise Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En este tutorial, instale SQL Server 2017 o la vista previa de 2019 de SQL Server en SUSE Linux Enterprise Server (SLES) v12 SP2. A continuación, conecte con **sqlcmd** para crear su primera base de datos y ejecutar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En este tutorial, instalar vista previa de 2019 de SQL Server en SUSE Linux Enterprise Server (SLES) v12 SP2. A continuación, conecte con **sqlcmd** para crear su primera base de datos y ejecutar consultas.

::: moniker-end

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, vea [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener una máquina SLES v12 SP2 con **al menos 2 GB** de memoria. El sistema de archivos debe ser **XFS** o **EXT4**. Otros sistemas de archivos como **BTRFS**, no se admiten.

Para instalar SUSE Linux Enterprise Server en su propio equipo, vaya a [ https://www.suse.com/products/server ](https://www.suse.com/products/server). También puede crear máquinas virtuales SLES en Azure. Consulte [crear y administrar máquinas virtuales Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)y usar `--image SLES` en la llamada a `az vm create`.

Si anteriormente ha instalado un CTP o la versión RC de SQL Server 2017, primero debe quitar el repositorio antiguo antes de seguir estos pasos. Para obtener más información, consulte [repositorios de configuración de Linux para SQL Server 2017 y 2019](sql-server-linux-change-repo.md).

> [!NOTE]
> En este momento, el [subsistema Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 no se admite como destino de la instalación.

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en SLES, ejecute los siguientes comandos en un terminal para instalar el **mssql-server** paquete:

1. Descargue el archivo de configuración del repositorio de Microsoft SQL Server 2017 SLES:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > Si desea probar SQL Server 2019, en su lugar, debe registrar el **Preview (2019)** repositorio. Use el comando siguiente para las instalaciones de SQL Server 2019:
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   > ```

2. Actualice los repositorios.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo zypper install -y mssql-server
   ```

4. Después de finaliza de la instalación de paquetes, ejecutar **el programa de instalación de mssql-conf** y siga las indicaciones para establecer la contraseña de SA y seleccione su edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Las siguientes ediciones de SQL Server 2017 libremente cuentan con licencia: Evaluation, Developer y Express.

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta de SA (caracteres de longitud de 8 como mínimo, incluidas letras mayúsculas y minúsculas, dígitos de base 10 o símbolos no alfanuméricos).

5. Una vez que se realiza la configuración, compruebe que el servicio se está ejecutando:

   ```bash
   systemctl status mssql-server
   ```

6. Si tiene previsto conectarse de forma remota, deberá abrir el puerto TCP de SQL Server (predeterminado: 1433) en el firewall. Si usa el firewall de SuSE, deberá editar la **/etc/sysconfig/SuSEfirewall2** archivo de configuración. Modificar el **FW_SERVICES_EXT_TCP** entrada debe incluir el número de puerto de SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

En este momento, SQL Server se está ejecutando en el equipo SLES y está listo para usarse.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en SLES, ejecute los siguientes comandos en un terminal para instalar el **mssql-server** paquete:

1. Descargue el archivo de configuración de repositorio de Microsoft SQL Server 2019 preview SLES:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   ```

2. Actualice los repositorios.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo zypper install -y mssql-server
   ```

4. Después de finaliza de la instalación de paquetes, ejecutar **el programa de instalación de mssql-conf** y siga las indicaciones para establecer la contraseña de SA y seleccione su edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta de SA (caracteres de longitud de 8 como mínimo, incluidas letras mayúsculas y minúsculas, dígitos de base 10 o símbolos no alfanuméricos).

5. Una vez que se realiza la configuración, compruebe que el servicio se está ejecutando:

   ```bash
   systemctl status mssql-server
   ```

6. Si tiene previsto conectarse de forma remota, deberá abrir el puerto TCP de SQL Server (predeterminado: 1433) en el firewall. Si usa el firewall de SuSE, deberá editar la **/etc/sysconfig/SuSEfirewall2** archivo de configuración. Modificar el **FW_SERVICES_EXT_TCP** entrada debe incluir el número de puerto de SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

En este momento, vista previa de SQL Server 2019 se está ejecutando en el equipo SLES y está listo para usarse.

::: moniker-end


## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, debe conectarse con una herramienta que puede ejecutar instrucciones Transact-SQL en SQL Server. Los pasos siguientes instalan las herramientas de línea de comandos de SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

1. Agregue el repositorio de Microsoft SQL Server a Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instalar **mssql-tools** con el paquete de desarrollador de unixODBC.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. Para mayor comodidad, agregar `/opt/mssql-tools/bin/` a su **ruta** variable de entorno. Esto le permite ejecutar las herramientas sin especificar la ruta de acceso completa. Ejecute los comandos siguientes para modificar el **ruta de acceso** de sesiones de inicio de sesión y sesiones/no-inicio de sesión interactivo:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
