---
title: Instalación de Microsoft ODBC Driver for SQL Server en Linux y macOS | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
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
ms.openlocfilehash: 7cbc1a78a2cce71494da04ffeb19649b22b2585e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736483"
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Instalación de Microsoft ODBC Driver for SQL Server en Linux y macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este artículo se explica cómo instalar el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS, así como las herramientas de línea de comandos opcionales para SQL Server (`bcp` y `sqlcmd`) y el desarrollo de encabezados de unixODBC.

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 for SQL Server 

> [!IMPORTANT]
> Si ha instalado el v17 `msodbcsql` paquete que estaba disponible brevemente, debe quitarlo antes de instalar el `msodbcsql17` paquete. Esto evitará conflictos. El `msodbcsql17` paquete se puede instalar en paralelo con la `msodbcsql` v13 paquete.

### <a name="debian-8-and-9"></a>Debian 8 y 9
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

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

### <a name="redhat-enterprise-server-6-and-7"></a>Red Hat Enterprise Server 6 y 7
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

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

### <a name="suse-linux-enterprise-server-11sp4-and-12"></a>SUSE Linux Enterprise Server 11SP4 y 12

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

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

### <a name="ubuntu-1404-1604-1710-and-1804"></a>Ubuntu 14.04, 16.04, con 17.10 y 18.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 14.04
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 17.10
curl https://packages.microsoft.com/config/ubuntu/17.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

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
> Es necesario para la compatibilidad con Ubuntu 18.04 versión 17.2 o posterior del controlador.

### <a name="os-x-1011-el-capitan-macos-1012-sierra-and-macos-1013-high-sierra"></a>OS X 10.11 (El capitán), macOS 10.12 (Sierra) y macOS 10.13 (High Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql17 mssql-tools
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

### <a name="redhat-enterprise-server-6"></a>Red Hat Enterprise Server 6
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

### <a name="redhat-enterprise-server-7"></a>Servidor de Red Hat Enterprise 7
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

### <a name="os-x-1011-el-capitan-and-macos-1012-sierra"></a>OS X 10.11 (El capitán) y macOS 10.12 (Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>Red Hat Enterprise Server 6
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

### <a name="redhat-enterprise-server-7"></a>Servidor de Red Hat Enterprise 7
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
Si prefiere o requiere la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 para instalarse en un equipo sin conexión a internet, deberá resolver manualmente las dependencias del paquete. El [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 tiene las siguientes dependencias directas:
- Ubuntu: libc6 (> = 2.21), libstdc ++ 6 (> = 4.9), libkrb5-3, libcurl3, openssl, debconf (> = 0,5), unixodbc (> = 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

Cada uno de estos paquetes a su vez tiene sus propias dependencias, que pueden o no pueden estar presentes en el sistema. Una solución general para este problema, consulte la documentación de administrador de paquetes de su distribución: [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](http://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian), y [SUSE](https://en.opensuse.org/Portal:Zypper)

También es común para descargar manualmente todos los paquetes dependientes y colocarlas juntas en el equipo de instalación y, a continuación, instalar manualmente cada paquete a su vez, finalizando con la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 paquete.

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - Descargue la última versión `msodbcsql` `.rpm` desde aquí: http://packages.microsoft.com/rhel/7/prod/
  - Instalar las dependencias y el controlador
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- Descargue la última versión `msodbcsql` `.deb` desde aquí: http://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- Instalar las dependencias y el controlador 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- Descargue la última versión `msodbcsql` `.rpm` desde aquí: http://packages.microsoft.com/sles/12/prod/
- Instalar las dependencias y el controlador

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

Una vez haya completado la instalación del paquete, puede comprobar que el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 encontrar todas sus dependencias, ejecutando ldd e inspeccionar su salida para las bibliotecas que faltan:
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

2.  Cambie al directorio donde la descarga colocó el archivo `msodbcsql-11.0.2270.0.tar.gz`. Asegúrese de que dispone del archivo \*.tar.gz que coincida con la versión de Linux. Para extraer los archivos, ejecute el comando siguiente: `tar xvzf msodbcsql-11.0.2270.0.tar.gz`.  
  
3.  Cambie al directorio `msodbcsql-11.0.2270.0`; allí verá un archivo llamado **install.sh**.  
  
4.  Para ver una lista de las opciones de instalación disponibles, ejecute el siguiente comando: **./install.sh**.  
  
5.  Realice una copia de seguridad de **odbcinst.ini**. El programa de instalación del controlador actualiza **odbcinst.ini**. odbcinst.ini contiene la lista de controladores que están registrados en el Administrador de controladores unixODBC. Para detectar la ubicación de odbcinst.ini en el equipo, ejecute el siguiente comando: ```odbc_config --odbcinstini```.  
  
6.  Antes de instalar el controlador, ejecute el siguiente comando: `./install.sh verify`. La salida de `./install.sh verify` notifica si el equipo tiene el software necesario para admitir el controlador ODBC en Linux.  
  
7.  Cuando esté preparado para instalar el controlador ODBC en Linux, ejecute el comando `./install.sh install`. Si tiene que especificar un comando de instalación (`bin-dir` o `lib-dir`), especifíquelo después de la opción **install**.  
  
8.  Cuando revise el contrato de licencia, escriba **YES** para continuar con la instalación.  
  
Programa de instalación coloca el controlador `/opt/microsoft/msodbcsql/11.0.2270.0`. El controlador y sus archivos auxiliares deben estar en `/opt/microsoft/msodbcsql/11.0.2270.0`.  
  
Para comprobar que se haya registrado correctamente Microsoft ODBC Driver en Linux, ejecute el siguiente comando: ```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```.  
  
En el artículo sobre el[uso de muestras de ODBC con C++ de MSDN existentes para el controlador ODBC en Linux](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) , se muestra un ejemplo de código que se conecta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el controlador ODBC en Linux.  
  
**Desinstalación**  
  
Puede desinstalar ODBC Driver 11 en Linux ejecutando los siguientes comandos:  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>Solucionar problemas de conexión  
Si no se puede establecer una conexión con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el controlador ODBC, utilice la siguiente información para identificar el problema.  
  
El problema de conexión más común es que existan dos copias instaladas del Administrador de controladores unixODBC. Busque libodbc\*.so\*en /usr. Si ve más de una versión del archivo, posiblemente signifique que tiene instalado más de un administrador de controladores. La aplicación podría utilizar una versión incorrecta.
  
Habilitar el registro de conexión mediante la edición de su `/etc/odbcinst.ini` archivo contenga la siguiente sección con estos elementos:

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
  
No hay más de un administrador de controladores instalados y la aplicación está usando uno o el Administrador de controladores no se creó correctamente equivocados.  
  
Para obtener más información sobre cómo resolver errores de conexión, consulte:  
  
-   [Pasos para solucionar problemas de conectividad de SQL](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [Solución de problemas de conectividad de SQL Server 2005 (parte I)](http://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [Solución de problemas de conectividad en SQL Server 2008 con el búfer en anillo de conectividad](http://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [Solucionador de problemas de autenticación de SQL Server](http://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [Detalles del error: http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    El número de error especificado en la dirección URL (11001) debe cambiarse para que coincida con el error que se muestra.  
  
## <a name="driver-files"></a>Archivos de controlador
El controlador ODBC en Linux y MacOS consta de los siguientes componentes:

### <a name="linux"></a>Linux

|Componente|Descripción|  
|---------------|-----------------|  
|libmsodbcsql-17. X.so.X.X o libmsodbcsql-13. X.so.X.X|El archivo de biblioteca dinámica del objeto compartido (`so`) que contiene toda la funcionalidad del controlador. Este archivo se instala en `/opt/microsoft/msodbcsql17/lib64/` para el 17 de controlador y en `/opt/microsoft/msodbcsql/lib64/` para Microsoft ODBC Driver 13.|  
|`msodbcsqlr17.rll` o `msodbcsqlr13.rll`|El archivo de recursos asociado de la biblioteca de controladores. Este archivo se instala en `[driver .so directory]../share/resources/en_US/`| 
|msodbcsql.h|El archivo de encabezado que contiene todas las definiciones nuevas necesarias para utilizar el controlador.<br /><br /> **Nota:**  No se puede hacer referencia a msodbcsql.h y odbcss.h en el mismo programa.<br /><br /> msodbcsql.h está instalado en `/opt/microsoft/msodbcsql17/include/` para Driver 17 y en `/opt/microsoft/msodbcsql/include/` para Microsoft ODBC Driver 13. |
|LICENSE.txt|El archivo de texto que contiene los términos del contrato de licencia del usuario final. Este archivo se coloca en `/usr/share/doc/msodbcsql17/` para Driver 17 y en `/usr/share/doc/msodbcsql/` para Microsoft ODBC Driver 13.|
|RELEASE_NOTES|El archivo de texto que contiene las notas de la versión. Este archivo se coloca en `/usr/share/doc/msodbcsql17/` para Driver 17 y en `/usr/share/doc/msodbcsql/` para Microsoft ODBC Driver 13.|


### <a name="macos"></a>MacOS

|Componente|Descripción|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib o libmsodbcsql.13.dylib|El archivo de biblioteca dinámica (`dylib`) que contiene toda la funcionalidad del controlador. Este archivo se instala en `/usr/local/lib/`.|  
|`msodbcsqlr17.rll` o `msodbcsqlr13.rll`|El archivo de recursos asociado de la biblioteca de controladores. Este archivo se instala en `[driver .dylib directory]../share/msodbcsql17/resources/en_US/` para Driver 17 y en `[driver .dylib directory]../share/msodbcsql/resources/en_US/` para Microsoft ODBC Driver 13. | 
|msodbcsql.h|El archivo de encabezado que contiene todas las definiciones nuevas necesarias para utilizar el controlador.<br /><br /> **Nota:**  No se puede hacer referencia a msodbcsql.h y odbcss.h en el mismo programa.<br /><br /> msodbcsql.h está instalado en `/usr/local/include/msodbcsql17/` para Driver 17 y en `/usr/local/include/msodbcsql/` para Microsoft ODBC Driver 13. |
|LICENSE.txt|El archivo de texto que contiene los términos del contrato de licencia del usuario final. Este archivo se coloca en `/usr/local/share/doc/msodbcsql17/` para Driver 17 y en `/usr/local/share/doc/msodbcsql/` para Microsoft ODBC Driver 13. |
|RELEASE_NOTES|El archivo de texto que contiene las notas de la versión. Este archivo se coloca en `/usr/local/share/doc/msodbcsql17/` para Driver 17 y en `/usr/local/share/doc/msodbcsql/` para Microsoft ODBC Driver 13. |

## <a name="resource-file-loading"></a>Carga del archivo de recursos

El controlador debe cargar el archivo de recursos para poder funcionar. Este archivo se denomina `msodbcsqlr17.rll` o `msodbcsqlr13.rll` según la versión del controlador. La ubicación de la `.rll` archivo es relativa a la ubicación del controlador de sí mismo (`so` o `dylib`), tal y como se indicó en la tabla anterior. A partir de la versión 17.1 el controlador también intentará cargar el `.rll` desde el valor predeterminado la active si la carga de la ruta de acceso relativa se produce un error. Las rutas de acceso de archivo de recursos de forma predeterminada son:

Linux: `/opt/microsoft/msodbcsql17/share/resources/en_US/`

MacOS: `/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>Ver también

[Instalación del Administrador de controladores](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)

[Requisitos del sistema](../../../connect/odbc/linux-mac/system-requirements.md)
