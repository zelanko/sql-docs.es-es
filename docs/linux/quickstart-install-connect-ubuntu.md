---
title: "Introducción a SQL Server 2017 en Ubuntu | Documentos de Microsoft"
description: "Este tutorial de inicio rápido muestra cómo instalar SQL Server 2017 en Ubuntu y, a continuación, crear y consultar una base de datos con sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 09/07/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f530c1fb9f1d21054631598a2d2ff06d6e2c5f46
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="install-sql-server-and-create-a-database-on-ubuntu"></a>Instalar a SQL Server y crear una base de datos en Ubuntu

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tutorial de inicio rápido, en primer lugar instale SQL Server 2017 RC2 en Ubuntu 16.04. A continuación, conecte con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener una máquina Ubuntu con **3,25 GB como mínimo** de memoria.

Para instalar Ubuntu en su propio equipo, vaya a [http://www.ubuntu.com/download/server](http://www.ubuntu.com/download/server). También puede crear máquinas virtuales de Ubuntu en Azure. Vea [crear y administrar máquinas virtuales de Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en Ubuntu, ejecute los siguientes comandos en un terminal para instalar el **mssql server** paquete.

1. Importar las claves GPG repositorio público:

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre el repositorio de Microsoft SQL Server Ubuntu:

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list)"
   ```

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
   > Asegúrese de especificar una contraseña segura para la cuenta SA (mínimo 8 caracteres, incluidas letras mayúsculas y minúsculas, dígitos de base 10 o símbolos que no sean alfanuméricos).

   > [!TIP]
   > Al instalar RC2, no hay licencias adquiridas tienen que lleve a cabo cualquiera de las ediciones. Dado que es un candidato de versión comercial, independientemente de la edición que seleccione aparece el siguiente mensaje:
   >
   > `This is an evaluation version.  There are [175] days left in the evaluation period.`
   >
   > Este mensaje no refleja la edición que seleccionó. Se relaciona con el período de vista previa para RC2.

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
> **Sqlcmd** es simplemente una herramienta para conectarse a SQL Server para ejecutar consultas y realizar tareas de administración y desarrollo. Otras herramientas incluyen [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md) y [código de Visual Studio](sql-server-linux-develop-use-vscode.md).

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]

