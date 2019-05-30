---
title: Instalar las herramientas de línea de comandos de SQL Server en Linux
titleSuffix: SQL Server
description: En este artículo se describe cómo instalar las herramientas de SQL Server en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/28/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 86a452237628df8952beaa09277a79b1de507aa1
ms.sourcegitcommit: 02df4e7965b2a858030bb508eaf8daa9bc10b00b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265403"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Instalar sqlcmd y bcp las herramientas de línea de comandos de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Los pasos siguientes instalan las herramientas de línea de comandos, controladores ODBC de Microsoft y sus dependencias. El **mssql-tools** paquete contiene:

- **sqlcmd**: Utilidad de línea de comandos de consulta.
- **bcp**: Utilidad de importación y exportación de forma masiva.

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
   sudo yum remove mssql-tools unixODBC-utf16-devel
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

1. **Opcional**: Agregar `/opt/mssql-tools/bin/` a su **ruta** variable de entorno en un shell de bash.

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

1. **Opcional**: Agregar `/opt/mssql-tools/bin/` a su **ruta** variable de entorno en un shell de bash.

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

1. **Opcional**: Agregar `/opt/mssql-tools/bin/` a su **ruta** variable de entorno en un shell de bash.

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
brew install mssql-tools
#for silent install: 
#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-tools
```

## <a id="docker"></a> Docker

Las herramientas de línea de comandos de SQL Server se incluyen en la imagen de Docker. Si se adjunta a la imagen con una línea de comandos interactiva, puede ejecutar las herramientas localmente.

## <a name="offline-installation"></a>Instalación sin conexión

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

1. En primer lugar, busque y copie el **mssql-tools** paquete para su distribución de Linux:

   | Distribución de Linux | **MSSQL-tools** ubicación del paquete |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools) |

1. También, busque y copie el **msodbcsql** paquete, que es una dependencia. El **msodbcsql** paquete también tiene una dependencia en cualquiera **unixODBC-desarrollo** (Red Hat y SLES) o **unixodbc-dev** (Ubuntu). La ubicación de la **msodbcsql** paquetes aparecen en la tabla siguiente:

   | Distribución de Linux | Ubicación de los paquetes ODBC |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [**msodbcsql**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql)<br/>[**unixodbc-dev**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/u/unixodbc/) |

1. **Mover los paquetes descargados en el equipo Linux**. Si usa un equipo diferente para descargar los paquetes, es una manera de mover los paquetes a la máquina Linux con la **scp** comando.

1. **Instalar los paquetes y**: Instalar el **mssql-tools** y **msodbc** paquetes. Si recibe errores de dependencia, omitir hasta el paso siguiente.

    | Plataforma | Comandos de instalación del paquete |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-<version>.rpm`<br/>`sudo yum localinstall mssql-tools-<version>.rpm` |
    | SLES | `sudo zypper install msodbcsql-<version>.rpm`<br/>`sudo zypper install mssql-tools-<version>.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_<version>.deb`<br/>`sudo dpkg -i mssql-tools_<version>.deb` |

1. **Resolver las dependencias que faltan**: Es posible que tenga dependencias que faltan en este momento. Si no es así, puede omitir este paso. En algunos casos, debe buscar manualmente e instalar estas dependencias.

    Para los paquetes RPM, puede inspeccionar las dependencias necesarias con los siguientes comandos:

    ```bash
    rpm -qpR msodbcsql-<version>.rpm
    rpm -qpR mssql-tools-<version>.rpm
    ```

    Para los paquetes de Debian, si tiene acceso a repositorios aprobados que contiene esas dependencias, la solución más fácil es usar el **apt-get** comando:

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > Este comando complete la instalación de los paquetes de SQL Server también.

    Si esto no funciona para el paquete de Debian, puede inspeccionar las dependencias necesarias con los siguientes comandos:

    ```bash
    dpkg -I msodbcsql_<version>_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_<version>_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>Pasos siguientes

Para obtener un ejemplo de cómo usar **sqlcmd** para conectarse a SQL Server y crear una base de datos, vea uno de los siguientes tutoriales:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)

Para obtener un ejemplo de cómo usar **bcp** para datos de exportación e importación masivas, vea [copia masiva de datos a SQL Server en Linux](sql-server-linux-migrate-bcp.md).
