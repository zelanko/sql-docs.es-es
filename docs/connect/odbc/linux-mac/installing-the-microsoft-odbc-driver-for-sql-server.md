---
title: Instalación de Microsoft ODBC Driver for SQL Server en Linux y macOS | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 5a7e7a5b528779092ff7740289c8325ba95ce3d5
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896794"
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Instalación de Microsoft ODBC Driver for SQL Server en Linux y macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este artículo se explica cómo instalar el controlador ODBC [!INCLUDE[msCoName](../../../includes/msconame_md.md)] para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS, así como las herramientas de línea de comandos opcionales para SQL Server (`bcp` y `sqlcmd`) y los encabezados de desarrollo unixODBC.

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 for SQL Server 

> [!IMPORTANT]
> Si ha instalado el paquete `msodbcsql` v17 que estaba disponible brevemente, debe quitarlo antes de instalar el paquete `msodbcsql17`. Esto evitará conflictos. El paquete `msodbcsql17` se puede instalar en paralelo con el paquete `msodbcsql` v13.

### <a name="alpine-linux"></a>Alpine Linux
```
#Download the desired package(s)
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.apk
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.2.1-1_amd64.apk


#(Optional) Verify signature, if 'gpg' is missing install it using 'apk add gnupg':
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.sig
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.2.1-1_amd64.sig

curl https://packages.microsoft.com/keys/microsoft.asc  | gpg --import -
gpg --verify msodbcsql17_17.5.2.1-1_amd64.sig msodbcsql17_17.5.2.1-1_amd64.apk
gpg --verify mssql-tools_17.5.2.1-1_amd64.sig mssql-tools_17.5.2.1-1_amd64.apk


#Install the package(s)
sudo apk add --allow-untrusted msodbcsql17_17.5.2.1-1_amd64.apk
sudo apk add --allow-untrusted mssql-tools_17.5.2.1-1_amd64.apk

```
> [!NOTE]
> - Se requiere la versión del controlador 17.5 o posterior para la compatibilidad con Alpine.

### <a name="debian"></a>Debian
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 10
curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
# optional: kerberos library for debian-slim distributions
sudo apt-get install libgssapi-krb5-2
```

> [!NOTE]
> - Puede sustituir el valor de la variable de entorno "ACCEPT_EULA" con el establecimiento de la variable debconf "msodbcsql/ACCEPT_EULA" en su lugar: `echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`


### <a name="redhat-enterprise-server-and-oracle-linux"></a>RedHat Enterprise Server y Oracle Linux
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 8 and Oracle Linux 8
curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo

exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
#Ensure SUSE Linux Enterprise 11 Security Module has been installed 
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

#SUSE Linux Enterprise Server 15
zypper ar https://packages.microsoft.com/config/sles/15/prod.repo
#(Only for driver 17.3 and below)
SUSEConnect -p sle-module-legacy/15/x86_64

exit
sudo ACCEPT_EULA=Y zypper install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu"></a>Ubuntu
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 19.10
curl https://packages.microsoft.com/config/ubuntu/19.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```
> [!NOTE]
> - Se requiere la versión del controlador 17.2 o posterior para la compatibilidad con Ubuntu 18.04.
> - Se requiere la versión del controlador 17.3 o posterior para la compatibilidad con Ubuntu 18.10.

> [!NOTE]
> - Puede sustituir el valor de la variable de entorno "ACCEPT_EULA" con el establecimiento de la variable debconf "msodbcsql/ACCEPT_EULA" en su lugar: `echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`

### <a name="macos"></a>MacOS

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=Y brew install msodbcsql17 mssql-tools
```

## <a name="microsoft-odbc-driver-131-for-sql-server"></a>Microsoft ODBC Driver 13.1 for SQL Server 

### <a name="debian-8"></a>Debian 8
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11"></a>SUSE Linux Enterprise Server 11

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1610"></a>Ubuntu 16.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="os-x-1011-el-capitan-and-macos-1012-sierra"></a>OS X 10.11 (El Capitan) y macOS 10.12 (Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su 
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo 
zypper update 
sudo ACCEPT_EULA=Y zypper install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
zypper install unixODBC-utf16-devel
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="offline-installation"></a>Instalación sin conexión
Si prefiere o necesita que la versión 13 del controlador ODBC de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] se instale en un equipo sin conexión a Internet, deberá resolver manualmente las dependencias del paquete. La versión 13 del controlador ODBC de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] tiene las siguientes dependencias directas:
- Ubuntu: libc6 (>= 2.21), libstdc++6 (>= 4.9), libkrb5-3, libcurl3, openssl, debconf (>= 0.5), unixodbc (>= 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

Cada uno de estos paquetes a su vez tiene sus propias dependencias, que pueden o no estar presentes en el sistema. Para una solución general de este problema, consulte la documentación del administrador de paquetes de su distribución: [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian) y [SUSE](https://en.opensuse.org/Portal:Zypper)

También es común descargar manualmente todos los paquetes dependientes y colocarlos juntos en el equipo de instalación, luego instalar manualmente cada paquete a su vez, finalizando con el paquete de la versión 13 del controlador ODBC de [!INCLUDE[msCoName](../../../includes/msconame_md.md)].

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - Descargue `msodbcsql` `.rpm` más recientes aquí: https://packages.microsoft.com/rhel/7/prod/
  - Instalar las dependencias y el controlador
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- Descargue `msodbcsql` `.deb` más recientes aquí: https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- Instalar las dependencias y el controlador 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- Descargue `msodbcsql` `.rpm` más recientes aquí: https://packages.microsoft.com/sles/12/prod/
- Instalar las dependencias y el controlador

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

Una vez que haya completado la instalación del paquete, puede comprobar que la versión 13 del controlador ODBC de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] encuentre todas sus dependencias ejecutando ldd e inspeccionando su salida para las bibliotecas que faltan:
```
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-linux"></a>Microsoft ODBC Driver 11 for SQL Server en Linux

Para poder utilizar el controlador, instale el Administrador de controladores unixODBC. Para obtener más información, vea [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) (Instalación del administrador de controladores).

**Pasos para la instalación**  

> [!IMPORTANT]  
> En estas instrucciones se hace referencia a `msodbcsql-11.0.2270.0.tar.gz`, que es el archivo de instalación para Red Hat Linux. Si va a instalar la versión preliminar para SUSE Linux, el nombre de archivo es `msodbcsql-11.0.2260.0.tar.gz`.  
  
Para instalar el controlador, haga lo siguiente:

1.  Asegúrese de que tiene permisos de raíz.  

2.  Cambie al directorio donde la descarga ha colocado el archivo `msodbcsql-11.0.2270.0.tar.gz`. Asegúrese de que dispone del archivo \*.tar.gz que coincida con la versión de Linux. Para extraer los archivos, ejecute el comando siguiente: `tar xvzf msodbcsql-11.0.2270.0.tar.gz`.  
  
3.  Cambie al directorio `msodbcsql-11.0.2270.0`; allí verá un archivo llamado **install.sh**.  
  
4.  Para ver una lista de las opciones de instalación disponibles, ejecute el siguiente comando: **./install.sh**.  
  
5.  Realice una copia de seguridad de **odbcinst.ini**. El programa de instalación del controlador actualiza **odbcinst.ini**. odbcinst.ini contiene la lista de controladores que están registrados en el Administrador de controladores unixODBC. Para detectar la ubicación de odbcinst.ini en el equipo, ejecute el siguiente comando: ```odbc_config --odbcinstini```.  
  
6.  Antes de instalar el controlador, ejecute el siguiente comando: `./install.sh verify`. La salida de `./install.sh verify` notifica si el equipo tiene el software necesario para admitir el controlador ODBC en Linux.  
  
7.  Cuando esté preparado para instalar el controlador ODBC en Linux, ejecute el comando `./install.sh install`. Si tiene que especificar un comando de instalación (`bin-dir` o `lib-dir`), especifíquelo después de la opción **install**.  
  
8.  Cuando revise el contrato de licencia, escriba **YES** para continuar con la instalación.  
  
El programa de instalación coloca el controlador en `/opt/microsoft/msodbcsql/11.0.2270.0`. El controlador y sus archivos auxiliares deben estar en `/opt/microsoft/msodbcsql/11.0.2270.0`.  
  
Para comprobar que se haya registrado correctamente Microsoft ODBC Driver en Linux, ejecute el siguiente comando: ```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```.  
  
En el artículo sobre el[uso de muestras de ODBC con C++ de MSDN existentes para el controlador ODBC en Linux](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) , se muestra un ejemplo de código que se conecta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el controlador ODBC en Linux.  
  
**Desinstalación**  
  
Puede desinstalar ODBC Driver 11 en Linux ejecutando los siguientes comandos:  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>Solucionar problemas de conexión  
Si no se puede establecer una conexión con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el controlador ODBC, utilice la siguiente información para identificar el problema.  
  
El problema de conexión más común es que existan dos copias instaladas del Administrador de controladores unixODBC. Busque libodbc\*.so\*en /usr. Si ve más de una versión del archivo, posiblemente signifique que tiene instalado más de un administrador de controladores. La aplicación podría utilizar una versión incorrecta.
  
Habilite el registro de conexión editando el archivo `/etc/odbcinst.ini` para que contenga la siguiente sección con estos elementos:

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
Si obtiene otro error de conexión y no ve un archivo de registro, posiblemente signifique que tiene dos copias del Administrador de controladores en el equipo. De lo contrario, los resultados del registro deberían ser similares a los siguientes:  
  
```  
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
Si la codificación de caracteres ASCII no es UTF-8, por ejemplo: 
  
```  
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
hay más de un administrador de controladores instalados y la aplicación utiliza el incorrecto, o bien el administrador de controladores no se creó correctamente.  
  
Para obtener más información sobre cómo resolver errores de conexión, consulte:  
  
-   [Pasos para solucionar problemas de conectividad de SQL](https://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [Solución de problemas de conectividad de SQL Server 2005 (parte I)](https://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [Solución de problemas de conectividad en SQL Server 2008 con el búfer en anillo de conectividad](https://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [Solucionador de problemas de autenticación de SQL Server](https://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [Detalles del error: https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    El número de error especificado en la dirección URL (11001) debe cambiarse para que coincida con el error que se muestra.  
  
## <a name="driver-files"></a>Archivos de controlador
El controlador ODBC en Linux y MacOS consta de los siguientes componentes:

### <a name="linux"></a>Linux

|Componente|Descripción|  
|---------------|-----------------|  
|libmsodbcsql-17.X.so.X.X o libmsodbcsql-13.X.so.X.X|El archivo de biblioteca dinámica del objeto compartido (`so`) que contiene toda la funcionalidad del controlador. Este archivo se instala en `/opt/microsoft/msodbcsql17/lib64/` para el controlador 17 y en `/opt/microsoft/msodbcsql/lib64/` para el controlador 13.|  
|`msodbcsqlr17.rll` o `msodbcsqlr13.rll`|El archivo de recursos asociado de la biblioteca de controladores. Este archivo se instala en `[driver .so directory]../share/resources/en_US/`.| 
|msodbcsql.h|El archivo de encabezado que contiene todas las definiciones nuevas necesarias para utilizar el controlador.<br /><br /> **Nota:**  No se puede hacer referencia a msodbcsql.h y odbcss.h en el mismo programa.<br /><br /> msodbcsql.h se instala en `/opt/microsoft/msodbcsql17/include/` para el controlador 17 y en `/opt/microsoft/msodbcsql/include/` para el controlador 13. |
|LICENSE.txt|El archivo de texto que contiene los términos del Contrato de licencia del usuario final. Este archivo se coloca en `/usr/share/doc/msodbcsql17/` para el controlador 17 y en `/usr/share/doc/msodbcsql/` para el controlador 13.|
|RELEASE_NOTES|El archivo de texto que contiene las notas de la versión. Este archivo se coloca en `/usr/share/doc/msodbcsql17/` para el controlador 17 y en `/usr/share/doc/msodbcsql/` para el controlador 13.|


### <a name="macos"></a>MacOS

|Componente|Descripción|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib o libmsodbcsql.13.dylib|El archivo de biblioteca dinámica (`dylib`) que contiene toda la funcionalidad del controlador. Este archivo se instala en `/usr/local/lib/`.|  
|`msodbcsqlr17.rll` o `msodbcsqlr13.rll`|El archivo de recursos asociado de la biblioteca de controladores. Este archivo se instala en `[driver .dylib directory]../share/msodbcsql17/resources/en_US/` para el controlador 17 y en `[driver .dylib directory]../share/msodbcsql/resources/en_US/` para el controlador 13. | 
|msodbcsql.h|El archivo de encabezado que contiene todas las definiciones nuevas necesarias para utilizar el controlador.<br /><br /> **Nota:**  No se puede hacer referencia a msodbcsql.h y odbcss.h en el mismo programa.<br /><br /> msodbcsql.h se instala en `/usr/local/include/msodbcsql17/` para el controlador 17 y en `/usr/local/include/msodbcsql/` para el controlador 13. |
|LICENSE.txt|El archivo de texto que contiene los términos del Contrato de licencia del usuario final. Este archivo se coloca en `/usr/local/share/doc/msodbcsql17/` para el controlador 17 y en `/usr/local/share/doc/msodbcsql/` para el controlador 13. |
|RELEASE_NOTES|El archivo de texto que contiene las notas de la versión. Este archivo se coloca en `/usr/local/share/doc/msodbcsql17/` para el controlador 17 y en `/usr/local/share/doc/msodbcsql/` para el controlador 13. |

## <a name="resource-file-loading"></a>Carga del archivo de recursos

El controlador debe cargar el archivo de recursos para poder funcionar. Este archivo se denomina `msodbcsqlr17.rll` o `msodbcsqlr13.rll` según la versión del controlador. La ubicación del archivo `.rll` es relativa a la ubicación del propio controlador (`so` o `dylib`), tal como se indica en la tabla anterior. A partir de la versión 17.1, el controlador también intentará cargar el `.rll` desde el directorio predeterminado si se produce un error en la carga de la ruta de acceso relativa. Las rutas de acceso predeterminadas del archivo de recursos son:

Linux: `/opt/microsoft/msodbcsql17/share/resources/en_US/`

MacOS: `/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>Consulte también

[Instalación del Administrador de controladores](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)

[Requisitos del sistema](../../../connect/odbc/linux-mac/system-requirements.md)
