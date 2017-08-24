---
title: "Instalación desatendida de SQL Server en Red Hat Enterprise Linux | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos SQL Server - instalación desatendida en Red Hat Enterprise Linux"
author: edmacauley
ms.author: edmacauley
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 8b97ec59acf463f73a9277566a89f32a2498a856
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="sample-unattended-sql-server-installation-script-for-red-hat-enterprise-linux"></a>Ejemplo: Script de instalación desatendida de SQL Server para Red Hat Enterprise Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Esta secuencia de comandos de ejemplo intensiva de errores instala SQL Server 2017 RC2 en Red Hat Enterprise Linux (RHEL) sin entrada interactiva. Proporciona ejemplos de cómo instalar el motor de base de datos, las herramientas de línea de comandos de SQL Server, Agente SQL Server y sigue los pasos posteriores a la instalación. Opcionalmente, puede instalar la búsqueda de texto completo y crear un usuario administrativo.

> [!TIP]
> Si no necesita una secuencia de comandos de instalación desatendida, la manera más rápida para instalar SQL Server es seguir el [tutorial de inicio rápido para Red Hat](quickstart-install-connect-red-hat.md). Para otros datos de configuración, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

- Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
- El sistema de archivos debe ser **XFS** o **EXT4**. Otros los sistemas de archivos, como **BTRFS**, no son compatibles.
- Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="sample-script"></a>Script de ejemplo
Guardar el script de ejemplo en un archivo y, a continuación, para personalizarlo, reemplace los valores de variables en el script. También puede establecer cualquiera de las variables de secuencias de comandos como variables de entorno, siempre y cuando se eliminen en el archivo de script.

```bash
#!/bin/bash

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_INSTALL_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server.repo
sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo

echo Running yum update -y...
sudo yum update -y

echo Installing SQL Server...
sudo yum install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y yum install -y mssql-tools unixODBC-devel

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo yum install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo yum install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring firewall to allow traffic on port 1433...
sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
sudo firewall-cmd --reload

# Example of setting post-installation configuration options
# Set trace flags 1204 and 1222 for deadlock tracing:
#echo Setting trace flags...
#sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after making configuration changes:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 5s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

## <a name="running-the-script"></a>Ejecuta la secuencia de comandos

Para ejecutar el script

1. Pegue el ejemplo en el editor de texto y guárdelo con un nombre fácil de recordar, como `install_sql.sh`.

1. Personalizar `MSSQL_SA_PASSWORD`, `MSSQL_PID`y cualquiera de las otras variables que desea cambiar.

1. Marcar la secuencia de comandos ejecutable

   ```bash
   chmod +x install_sql.sh
   ```

1. Ejecute la secuencia de comandos

   ```bash
   ./install_sql.sh
   ```

## <a name="understanding-the-script"></a>Descripción de la secuencia de comandos

Lo primero que hace la secuencia de comandos de Bash se establece algunas variables.  Puede tratarse de las variables de scripting, como en el ejemplo, o las variables de entorno.  La variable ``` MSSQL_SA_PASSWORD ``` es **requiere** por la instalación de SQL Server, los demás son variables personalizadas creadas para la secuencia de comandos.  El script de ejemplo realiza los pasos siguientes:

1. Importar las claves públicas de Microsoft GPG.

1. Registrar los repositorios de Microsoft para SQL Server y las herramientas de línea de comandos.

1. Actualizar los repositorios locales

1. Instalar SQL Server

1. Configurar SQL Server con el ```MSSQL_SA_PASSWORD``` y acepte automáticamente el contrato de licencia para el usuario final.

1. Acepte el contrato de licencia para el usuario final para las herramientas de línea de comandos de SQL Server, instalarlos e instalará automáticamente el paquete de unixodbc-dev.

1. Agregar las herramientas de línea de comandos de SQL Server a la ruta de acceso para facilitar su uso.

1. Instalar el Agente SQL Server si la variable de scripting ```SQL_INSTALL_AGENT``` se establece, de forma predeterminada.

1. Si lo desea instalar la búsqueda de texto completo de SQL Server, si la variable ```SQL_INSTALL_FULLTEXT``` se establece.

1. Desbloquear el puerto 1433 para TCP en el firewall de sistema, es necesario para conectarse a SQL Server desde otro sistema.

1. Si lo desea establecer marcas de seguimiento para el seguimiento de interbloqueo. (requiere el comentario de las líneas)

1. SQL Server ya está instalado, para que sea operativa, reinicie el proceso.

1. Compruebe que SQL Server está instalado correctamente, al tiempo que oculta los mensajes de error.

1. Crear un nuevo usuario de administrador del servidor si ```SQL_INSTALL_USER``` y ```SQL_INSTALL_USER_PASSWORD``` están establecidos.

## <a name="next-steps"></a>Pasos siguientes

Simplificar varias instalaciones desatendidas y crear una secuencia de comandos de Bash independiente que establece las variables de entorno adecuada.  Puede quitar cualquiera de las variables de la secuencia de comandos de ejemplo usa y colocarlos en sus propios scripts de Bash.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

A continuación, ejecute la secuencia de comandos de Bash como sigue:
```bash
. ./my_script_name.sh
```

Para obtener más información acerca de SQL Server en Linux, consulte [SQL Server en la introducción a Linux](sql-server-linux-overview.md).
