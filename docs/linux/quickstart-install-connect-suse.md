---
title: Introducción a SQL Server 2017 en SUSE Linux Enterprise Server | Microsoft Docs
description: Este inicio rápido muestra cómo instalar SQL Server 2017 en SUSE Linux Enterprise Server y, a continuación, crear y consultar una base de datos con sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: 7534ea052c5c277edb195c2a6a2a12ead1661e33
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102593"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Inicio rápido: Instalar SQL Server y crear una base de datos en SUSE Linux Enterprise Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial, primero instale SQL Server 2017 en SUSE Linux Enterprise Server (SLES) v12 SP2. A continuación, tendrá que conectar con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, vea [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener una máquina SLES v12 SP2 con **al menos 2 GB** de memoria. El sistema de archivos debe ser **XFS** o **EXT4**. Otros sistemas de archivos como **BTRFS**, no se admiten.

Para instalar SUSE Linux Enterprise Server en su propio equipo, vaya a [ https://www.suse.com/products/server ](https://www.suse.com/products/server). También puede crear máquinas virtuales SLES en Azure. Consulte [crear y administrar máquinas virtuales Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)y usar `--image SLES` en la llamada a `az vm create`.

> [!NOTE]
> En este momento, el [subsistema Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 no se admite como destino de la instalación.

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en SLES, ejecute los siguientes comandos en un terminal para instalar el **mssql-server** paquete:

> [!IMPORTANT]
> Si anteriormente ha instalado un CTP o la versión RC de SQL Server 2017, primero debe quitar el repositorio antiguo antes de registrar uno de los repositorios de GA. Para obtener más información, consulte [cambiar repositorios desde el repositorio de vista previa en el repositorio GA](sql-server-linux-change-repo.md).

1. Descargue el archivo de configuración del repositorio de Microsoft SQL Server SLES:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!NOTE]
   > Este es el repositorio de actualización acumulativa (CU). Para obtener más información acerca de las opciones de repositorio y sus diferencias, vea [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

1. Actualice los repositorios.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
1. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo zypper install -y mssql-server
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

1. Si tiene previsto conectarse de forma remota, deberá abrir el puerto TCP de SQL Server (predeterminado: 1433) en el firewall. Si usa el firewall de SuSE, deberá editar la **/etc/sysconfig/SuSEfirewall2** archivo de configuración. Modificar el **FW_SERVICES_EXT_TCP** entrada debe incluir el número de puerto de SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

En este momento, SQL Server se está ejecutando en el equipo SLES y está listo para usarse.

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
