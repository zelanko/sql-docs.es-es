---
title: Instalar las herramientas de línea de comandos de SQL Server en Linux | Microsoft Docs
description: En este artículo se describe cómo instalar las herramientas de SQL Server en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 6a5625563e32923abefe3dee3bcb29a694303d42
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981746"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Instalar sqlcmd y bcp las herramientas de línea de comandos de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Los pasos siguientes instalan las herramientas de línea de comandos, controladores ODBC de Microsoft y sus dependencias. El **mssql-tools** paquete contiene:

- **Sqlcmd**: utilidad de línea de comandos de consulta.
- **BCP**: utilidad de importación y exportación de forma masiva.

Instalar las herramientas para su plataforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

En este artículo se describe cómo instalar las herramientas de línea de comandos. Si desea obtener ejemplos de cómo usar **sqlcmd** o **bcp**, consulte el [vínculos](#next-steps) al final de este tema.

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>Instalar las herramientas en RHEL 7

Use los pasos siguientes para instalar el **mssql-tools** en Red Hat Enterprise Linux. 

1. ENTRAR en modo de superusuario.

   ```bash
   sudo su
   ```

1. Descargue el archivo de configuración del repositorio Microsoft Red Hat.

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. Salir del modo de superusuario.

   ```bash
   exit
   ```

1. Si tiene una versión anterior de **mssql-tools** instalado, quite los paquetes de unixODBC anteriores.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Ejecute los comandos siguientes para instalar **mssql-tools** con el paquete de desarrollador de unixODBC.

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Para actualizar a la versión más reciente de **mssql-tools** ejecute los siguientes comandos:
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
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

## <a id="ubuntu"></a>Instalar las herramientas en Ubuntu 16.04

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

## <a id="SLES"></a>Instalar las herramientas en SLES 12

Use los pasos siguientes para instalar el **mssql-tools** en SUSE Linux Enterprise Server. 

1. Agregue el repositorio de Microsoft SQL Server a Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instalar **mssql-tools** con el paquete de desarrollador de unixODBC.

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Para actualizar a la versión más reciente de **mssql-tools** ejecute los siguientes comandos:
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
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

## <a id="macos"></a> Instalar las herramientas en macOS

Una vista previa de **sqlcmd** y **bcp** ahora está disponible en Mac OS. Para obtener más información, consulte el [anuncio](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/).

*Instalar [Homebrew](https://brew.sh) si no tiene ya:*

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Para instalar las herramientas para Mac El capitán y Sierra, use los siguientes comandos:

```
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox mssql-tools
#for silent install: 
#ACCEPT_EULA=y brew install --no-sandbox mssql-tools
```

## <a id="docker"></a> Docker

A partir de SQL Server 2017 CTP 2.0, las herramientas de línea de comandos de SQL Server se incluyen en la imagen de Docker. Si se adjunta a la imagen con una línea de comandos interactiva, puede ejecutar las herramientas localmente.

## <a name="offline-installation"></a>Instalación sin conexión

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

En la tabla siguiente se proporciona la ubicación de los paquetes de herramientas más recientes:

| Paquete de herramientas | Versión | Descargar |
|-----|-----|-----|
| Paquete de herramientas de Red Hat RPM | 14.0.5.0-1 | [paquete de MSSQL-tools RPM](https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Paquete de herramientas de RPM SLES | 14.0.5.0-1 | [paquete de MSSQL-tools RPM](https://packages.microsoft.com/sles/12/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Paquete de herramientas de Ubuntu 16.04 Debian | 14.0.5.0-1 | [paquete de Debian MSSQL-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |
| Paquete de herramientas de Ubuntu 16.10 Debian | 14.0.5.0-1 | [paquete de Debian MSSQL-tools](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |

Estos paquetes dependen **msodbcsql**, que debe instalarse primero. El **msodbcsql** paquete descartasen también tiene una dependencia en cualquiera **unixODBC-desarrollo** (RPM) o **unixodbc-dev** (Debian). La ubicación de la **msodbcsql** paquetes aparecen en la tabla siguiente:

| paquete msodbcsql | Versión | Descargar |
|-----|-----|-----|
| Paquete de Red Hat RPM msodbcsql | 13.1.6.0-1 | [paquete RPM msodbcsql](https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Paquete de SLES RPM msodbcsql | 13.1.6.0-1 | [paquete RPM msodbcsql](https://packages.microsoft.com/sles/12/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Paquete de Debian msodbcsql Ubuntu 16.04 | 13.1.6.0-1 | [paquete de Debian msodbcsql](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |
| Paquete de Debian msodbcsql Ubuntu 16.10 | 13.1.6.0-1 | [paquete de Debian msodbcsql](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |

Para instalar manualmente estos paquetes, siga estos pasos:

1. **Mover los paquetes descargados en el equipo Linux**. Si usa un equipo diferente para descargar los paquetes, es una manera de mover los paquetes a la máquina Linux con la **scp** comando.

1. **Instalar los paquetes y**: instalar el **mssql-tools** y **msodbc** paquetes. Si recibe errores de dependencia, omitir hasta el paso siguiente.

    | Plataforma | Comandos de instalación del paquete |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | SLES | `sudo zypper install msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo zypper install mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_13.1.6.0-1_amd64.deb`<br/>`sudo dpkg -i mssql-tools_14.0.5.0-1_amd64.deb` |

1. **Resolver las dependencias que faltan**: es posible que tenga dependencias que faltan en este momento. Si no es así, puede omitir este paso. En algunos casos, debe buscar manualmente e instalar estas dependencias.

    Para los paquetes RPM, puede inspeccionar las dependencias necesarias con los siguientes comandos:

    ```bash
    rpm -qpR msodbcsql-13.1.6.0-1.x86_64.rpm
    rpm -qpR mssql-tools-14.0.5.0-1.x86_64.rpm
    ```

    Para los paquetes de Debian, si tiene acceso a repositorios aprobados que contiene esas dependencias, la solución más fácil es usar el **apt-get** comando:

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > Este comando complete la instalación de los paquetes de SQL Server también.

    Si esto no funciona para el paquete de Debian, puede inspeccionar las dependencias necesarias con los siguientes comandos:

    ```bash
    dpkg -I msodbcsql_13.1.6.0-1_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_14.0.5.0-1_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>Pasos siguientes

Para obtener un ejemplo de cómo usar **sqlcmd** para conectarse a SQL Server y crear una base de datos, vea uno de los siguientes tutoriales:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)

Para obtener un ejemplo de cómo usar **bcp** para datos de exportación e importación masivas, vea [copia masiva de datos a SQL Server en Linux](sql-server-linux-migrate-bcp.md).
