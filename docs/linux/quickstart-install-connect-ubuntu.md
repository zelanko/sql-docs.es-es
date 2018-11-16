---
title: Introducción a SQL Server en Ubuntu | Microsoft Docs
description: Este inicio rápido muestra cómo instalar SQL Server 2017 ni SQL Server 2019 en Ubuntu y, a continuación, crear y consultar una base de datos con sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 917e43dd6a9c78e5199967df58a2d46c4843cf13
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677962"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>Inicio rápido: Instalar SQL Server y crear una base de datos en Ubuntu

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En este tutorial, instale SQL Server 2017 o la versión preliminar de SQL Server 2019 en Ubuntu 16.04. A continuación, conecte con **sqlcmd** para crear su primera base de datos y ejecutar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En este inicio rápido, se instala vista previa de SQL Server 2019 en Ubuntu 16.04. A continuación, conecte con **sqlcmd** para crear su primera base de datos y ejecutar consultas.

::: moniker-end

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, vea [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener una máquina Ubuntu 16.04 con **al menos 2 GB** de memoria.

Para instalar Ubuntu en su propio equipo, vaya a [ https://www.ubuntu.com/download/server ](https://www.ubuntu.com/download/server). También puede crear máquinas virtuales Ubuntu en Azure. Consulte [crear y administrar máquinas virtuales Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> En este momento, el [subsistema Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 no se admite como destino de la instalación.

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en Ubuntu, ejecute los siguientes comandos en un terminal para instalar el **mssql-server** paquete.

1. Importe las claves GPG repositorio público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrar el repositorio de Microsoft SQL Server Ubuntu:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > Si desea probar SQL Server 2019, en su lugar, debe registrar el **Preview (2019)** repositorio. Use el comando siguiente para las instalaciones de SQL Server 2019:
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   > ```

3. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
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

6. Si tiene previsto conectarse de forma remota, deberá abrir el puerto TCP de SQL Server (predeterminado: 1433) en el firewall.

En este momento, SQL Server se está ejecutando en la máquina Ubuntu y está listo para usarse.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en Ubuntu, ejecute los siguientes comandos en un terminal para instalar el **mssql-server** paquete.

1. Importe las claves GPG repositorio público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrar el repositorio de Ubuntu de Microsoft SQL Server para SQL Server 2019 preview:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   ```

3. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
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

6. Si tiene previsto conectarse de forma remota, deberá abrir el puerto TCP de SQL Server (predeterminado: 1433) en el firewall.

En este momento, vista previa de SQL Server 2019 se está ejecutando en la máquina Ubuntu y está listo para usarse.

::: moniker-end

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

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
