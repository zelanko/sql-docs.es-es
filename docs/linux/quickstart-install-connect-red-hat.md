---
title: Introducción a SQL Server en Red Hat Enterprise Linux
titleSuffix: SQL Server
description: Este inicio rápido muestra cómo instalar SQL Server 2017 ni SQL Server 2019 en Red Hat Enterprise Linux y, a continuación, crear y consultar una base de datos con sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: b811ea193dd15b2d472224dfc7d719a60174ed4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713518"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>Inicio rápido: Instalar a SQL Server y crear una base de datos en Red Hat

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En este tutorial, instala SQL Server 2017 ni SQL Server 2019 en Red Hat Enterprise Linux (RHEL). A continuación, conecte con **sqlcmd** para crear su primera base de datos y ejecutar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En este tutorial, instale versión preliminar de SQL Server 2019 en Red Hat Enterprise Linux (RHEL) 7.3 +. A continuación, conecte con **sqlcmd** para crear su primera base de datos y ejecutar consultas.

::: moniker-end

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, vea [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener una máquina RHEL 7.3, 7.4, 7.5 o 7.6 con **al menos 2 GB** de memoria.

Para instalar la Red Hat Enterprise Linux en su propio equipo, vaya a [ https://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation). También puede crear máquinas virtuales RHEL en Azure. Consulte [crear y administrar máquinas virtuales Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)y usar `--image RHEL` en la llamada a `az vm create`.

Si anteriormente ha instalado un CTP o la versión RC de SQL Server 2017, primero debe quitar el repositorio antiguo antes de seguir estos pasos. Para obtener más información, consulte [repositorios de configuración de Linux para SQL Server 2017 y 2019](sql-server-linux-change-repo.md).

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en RHEL, ejecute los siguientes comandos en un terminal para instalar el **mssql-server** paquete:

1. Descargue el archivo de configuración del repositorio de Microsoft SQL Server 2017 Red Hat:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > Si desea probar SQL Server 2019, en su lugar, debe registrar el **Preview (2019)** repositorio. Use el comando siguiente para las instalaciones de SQL Server 2019:
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   > ```

2. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Después de finaliza de la instalación de paquetes, ejecutar **el programa de instalación de mssql-conf** y siga las indicaciones para establecer la contraseña de SA y seleccione su edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Las siguientes ediciones de SQL Server 2017 libremente cuentan con licencia: Evaluation, Developer y Express.

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta de SA (caracteres de longitud de 8 como mínimo, incluidas letras mayúsculas y minúsculas, dígitos de base 10 o símbolos no alfanuméricos).

4. Una vez que se realiza la configuración, compruebe que el servicio se está ejecutando:

   ```bash
   systemctl status mssql-server
   ```

5. Para permitir conexiones remotas, abra el puerto de SQL Server en el firewall en RHEL. El puerto de SQL Server predeterminado es TCP 1433. Si usas **FirewallD** para el firewall, puede usar los siguientes comandos:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

En este momento, SQL Server se está ejecutando en el equipo RHEL y está listo para usarse.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en RHEL, ejecute los siguientes comandos en un terminal para instalar el **mssql-server** paquete:

1. Descargue la versión preliminar de Microsoft SQL Server 2019 archivo de configuración de Red Hat repositorio:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   ```

2. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Después de finaliza de la instalación de paquetes, ejecutar **el programa de instalación de mssql-conf** y siga las indicaciones para establecer la contraseña de SA y seleccione su edición.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Asegúrese de especificar una contraseña segura para la cuenta de SA (caracteres de longitud de 8 como mínimo, incluidas letras mayúsculas y minúsculas, dígitos de base 10 o símbolos no alfanuméricos).

4. Una vez que se realiza la configuración, compruebe que el servicio se está ejecutando:

   ```bash
   systemctl status mssql-server
   ```

5. Para permitir conexiones remotas, abra el puerto de SQL Server en el firewall en RHEL. El puerto de SQL Server predeterminado es TCP 1433. Si usas **FirewallD** para el firewall, puede usar los siguientes comandos:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

En este momento, vista previa de SQL Server 2019 se está ejecutando en el equipo RHEL y está listo para usarse.

::: moniker-end

## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, debe conectarse con una herramienta que puede ejecutar instrucciones Transact-SQL en SQL Server. Los pasos siguientes instalan las herramientas de línea de comandos de SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

1. Descargue el archivo de configuración del repositorio Microsoft Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. Si tiene una versión anterior de **mssql-tools** instalado, quite los paquetes de unixODBC anteriores.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Ejecute los comandos siguientes para instalar **mssql-tools** con el paquete de desarrollador de unixODBC.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. Para mayor comodidad, agregar `/opt/mssql-tools/bin/` a su **ruta** variable de entorno. Esto le permite ejecutar las herramientas sin especificar la ruta de acceso completa. Ejecute los comandos siguientes para modificar el **ruta de acceso** de sesiones de inicio de sesión y sesiones/no-inicio de sesión interactivo:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
