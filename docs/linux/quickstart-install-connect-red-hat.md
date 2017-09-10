---
title: "Introducción a SQL Server 2017 en Red Hat Enterprise Linux | Documentos de Microsoft"
description: "Este tutorial de inicio rápido muestra cómo instalar SQL Server 2017 en Red Hat Enterprise Linux y, a continuación, crear y consultar una base de datos con sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 09/07/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 5309c2884fa4bf46a4c9c7224f4c1f21be23e7e6
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="install-sql-server-and-create-a-database-on-red-hat"></a>Instalar a SQL Server y crear una base de datos en Red Hat

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tutorial de inicio rápido, primero instalar SQL Server de 2017 RC2 en Red Hat Enterprise Linux (RHEL) 7.3. A continuación, conecte con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

> [!TIP]
> Este tutorial requiere la intervención del usuario y una conexión a internet. Si está interesado en el [desatendida](sql-server-linux-setup.md#unattended) o [sin conexión](sql-server-linux-setup.md#offline) procedimientos de instalación, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

Debe tener una máquina de RHEL 7.3 con **3,25 GB como mínimo** de memoria.

Para instalar Red Hat Enterprise Linux en su propio equipo, vaya a [http://access.redhat.com/products/red-hat-enterprise-linux/evaluation](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation). También puede crear máquinas virtuales RHEL en Azure. Vea [crear y administrar máquinas virtuales de Linux con la CLI de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)y usar `--image RHEL` en la llamada a `az vm create`.

Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar SQL Server

Para configurar SQL Server en RHEL, ejecute los siguientes comandos en un terminal para instalar el **mssql server** paquete:

1. Descargue el archivo de configuración del repositorio de Red Hat de Microsoft SQL Server:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server.repo
   ```

1. Ejecute los comandos siguientes para instalar a SQL Server:

   ```bash
   sudo yum update
   sudo yum install -y mssql-server
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
   
1. Para permitir conexiones remotas, abra el puerto de SQL Server en el firewall en RHEL. El puerto de SQL Server predeterminado es TCP 1433. Si utilizas **FirewallD** para el firewall, puede usar los siguientes comandos:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

En este momento, SQL Server se ejecuta en el equipo RHEL y está listo para usarse.

## <a id="tools"></a>Instalar las herramientas de línea de comandos de SQL Server

Para crear una base de datos, debe conectarse con una herramienta que se puede ejecutar instrucciones Transact-SQL en SQL Server. Los siguientes pasos instalación las herramientas de línea de comandos de SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) y [bcp](../tools/bcp-utility.md).

1. Descargue el archivo de configuración del repositorio de Microsoft Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. Si tiene una versión anterior de **mssql herramientas** instalado, quite los paquetes de unixODBC anteriores.

   ```bash
   sudo yum update
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Ejecute los comandos siguientes para instalar **mssql herramientas** con el paquete de desarrollador de unixODBC.

   ```bash
   sudo yum update
   sudo yum install -y mssql-tools unixODBC-devel
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

