---
title: Instalación desatendida para SQL Server en Ubuntu
titleSuffix: SQL Server
description: 'Ejemplo de Script SQL Server: instalación desatendida en Ubuntu'
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.openlocfilehash: ab93dde353b8576f682a2e032888da36a5743012
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160503"
---
# <a name="sample-unattended-sql-server-installation-script-for-ubuntu"></a>Ejemplo: Script de instalación desatendida de SQL Server para Ubuntu

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este script de Bash de ejemplo instala SQL Server 2017 en Ubuntu 16.04 sin entrada interactiva. Se proporcionan ejemplos de instalación del motor de base de datos, las herramientas de línea de comandos de SQL Server, Agente SQL Server y lleva a cabo los pasos posteriores a la instalación. Opcionalmente, puede instalar la búsqueda de texto completo y crear un usuario administrativo.

> [!TIP]
> Si no necesita un script de instalación desatendida, la forma más rápida para instalar SQL Server es seguir el [inicio rápido para Ubuntu](quickstart-install-connect-ubuntu.md). Para obtener más información de configuración, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Requisitos previos

- Necesita al menos 2 GB de memoria para ejecutar SQL Server en Linux.
- El sistema de archivos debe ser **XFS** o **EXT4**. Otros sistemas de archivos como **BTRFS**, no se admiten.
- Para otros requisitos del sistema, consulte [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="sample-script"></a>Script de ejemplo

```bash
#!/bin/bash -e

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
sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
sudo add-apt-repository "${repoargs}"
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
sudo add-apt-repository "${repoargs}"

echo Running apt-get update -y...
sudo apt-get update -y

echo Installing SQL Server...
sudo apt-get install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo apt-get install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo apt-get install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring UFW to allow traffic on port 1433...
sudo ufw allow 1433/tcp
sudo ufw reload

# Optional example of post-installation configuration.
# Trace flags 1204 and 1222 are for deadlock tracing.
# echo Setting trace flags...
# sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after installing:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 3s
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

### <a name="running-the-script"></a>La ejecución del script

Para ejecutar el script

1. Pegue el ejemplo en el editor de texto y guárdelo con un nombre fácil de recordar, como `install_sql.sh`.

1. Personalizar `MSSQL_SA_PASSWORD`, `MSSQL_PID`y cualquiera de las demás variables que desea cambiar.

1. Marque el script como archivo ejecutable

   ```bash
   chmod +x install_sql.sh
   ```

1. Ejecute el script

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>Descripción de la secuencia de comandos
Lo primero que hace el script de Bash se establece algunas variables. Pueden ser variables de scripting, como en el ejemplo, o las variables de entorno. La variable ``` MSSQL_SA_PASSWORD ``` es **requiere** mediante la instalación de SQL Server, los demás son variables personalizadas creadas para la secuencia de comandos. El script de ejemplo lleva a cabo los pasos siguientes:

1. Importe las claves públicas de GPG de Microsoft.

1. Registre los repositorios de Microsoft para SQL Server y las herramientas de línea de comandos.

1. Actualice los repositorios locales

1. Instalar SQL Server

1. Configurar SQL Server con el ```MSSQL_SA_PASSWORD``` y acepte automáticamente el contrato de licencia del usuario final.

1. Automáticamente acepte el contrato de licencia del usuario final para las herramientas de línea de comandos de SQL Server, instalarlos e instalar el paquete de unixodbc-dev.

1. Agregar las herramientas de línea de comandos de SQL Server a la ruta de acceso para facilitar su uso.

1. Instalar el Agente SQL Server si la variable de scripting ```SQL_INSTALL_AGENT``` se establece, de forma predeterminada.

1. Opcionalmente, instale la búsqueda de texto completo de SQL Server, si la variable ```SQL_INSTALL_FULLTEXT``` se establece.

1. Desbloquee el puerto 1433 para TCP en el firewall del sistema, que es necesario para conectarse a SQL Server desde otro sistema.

1. Opcionalmente, establecer las marcas de seguimiento para el seguimiento de interbloqueo. (requiere el comentario de las líneas)

1. Ahora está instalado SQL Server, para que sea operativa, reinicie el proceso.

1. Compruebe que SQL Server está instalado correctamente, al tiempo que oculta los mensajes de error.

1. Crear un nuevo usuario de administrador del servidor si ```SQL_INSTALL_USER``` y ```SQL_INSTALL_USER_PASSWORD``` están establecidos.

## <a name="next-steps"></a>Pasos siguientes

Simplificar varias instalaciones desatendidas y crear un script de Bash independiente que establece las variables de entorno adecuada. Puede quitar cualquiera de las variables de la secuencia de comandos de ejemplo usa y colocarlos en su propio script de Bash.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

A continuación, ejecute el script de Bash como sigue:
```bash
. ./my_script_name.sh
```

Para obtener más información acerca de SQL Server en Linux, consulte [SQL Server en Linux overview](sql-server-linux-overview.md).
