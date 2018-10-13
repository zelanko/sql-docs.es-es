---
title: Instalar SQL Server Machine Learning Services (R, Python y Java) en Linux | Microsoft Docs
description: Este artículo describe cómo instalar SQL Server Machine Learning Services (R, Python, Java) en Red Hat y Ubuntu.
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.date: 10/09/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8433f705b41782c61950cb74f76f694d61cd548d
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100456"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-java-on-linux"></a>Instalar SQL Server 2019 Machine Learning Services (R, Python y Java) en Linux

[SQL Server Machine Learning Services](../advanced-analytics/what-is-sql-server-machine-learning.md) se ejecuta en sistemas operativos de Linux a partir de esta versión preliminar de SQL Server 2019. Siga los pasos descritos en este artículo para instalar la extensión de programación Java, o el aprendizaje automático extensiones para R y Python. 

Aprendizaje automático y las extensiones de programación es un complemento para el motor de base de datos. Aunque puede [instalar el motor de base de datos y Machine Learning Services simultáneamente](#install-all), es una práctica recomendada para instalar y configurar primero el motor de base de datos de SQL Server para que pueda resolver los problemas antes de agregar más componentes. 

Ubicación del paquete de las extensiones de R, Python y Java se encuentran en los repositorios de código fuente de SQL Server para Linux. Si ya ha configurado instalación repositorios de código fuente para el motor de base de datos, puede ejecutar comandos de instalación del paquete con el mismo registro del repositorio la mlservices mssql.

## <a name="prerequisites"></a>Requisitos previos

+ Sistema operativo Linux debe ser [compatibles con SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), ejecutándose localmente o en un contenedor de Docker.

+ Debe tener una instancia del motor de base de datos de SQL Server 2019 en: 

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ Solo, r [Microsoft R Open](#mro) mssql mlsservices para paquetes de R. 

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Instalación de Microsoft R Open (MRO)

Distribución de la base de Microsoft de R es un requisito previo para usar RevoScaleR, MicrosoftML y otros paquetes de R instalados con Machine Learning Services.

La versión necesaria es MRO 3.4.4.

Elegir entre los dos métodos siguientes para instalar MRO:

+ Descargar el paquete tarball MRO de MRAN, descomprímalo y ejecute el script install.sh. Puede seguir el [instrucciones de instalación en MRAN](https://mran.microsoft.com/releases/3.4.4) si desea que este enfoque.

+ Como alternativa, registrar el **packages.microsoft.com** repositorio como se describe a continuación para instalar los tres paquetes que componen la distribución MRO: mro-microsoft-r-abierto, microsoft-r-open-mkl y Microsoft-r-open-foreachiterators. 

Los siguientes comandos de registrar el repositorio proporcionar MRO. Después del registro, los comandos para instalar otros paquetes de R, por ejemplo, mssql-mlservices-mml-r, incluirá automáticamente MRO como una dependencia del paquete.

#### <a name="mro-on-ubuntu"></a>MRO en Ubuntu

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Add the **azure-cli** repo to your apt sources list
AZ_REPO=$(lsb_release -cs)

echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb
```

#### <a name="mro-on-rhel"></a>MRO en RHEL

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Create local `azure-cli` repository
sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'

# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
```
#### <a name="mro-on-suse"></a>MRO en SUSE

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system:
zypper update
```

## <a name="package-list"></a>Lista de paquetes

En un dispositivo conectado a internet, los paquetes se descargan e instalan independientemente el motor de base de datos mediante el instalador de paquetes para cada sistema operativo. La tabla siguiente describen todos los paquetes disponibles, pero para las instalaciones conectada a internet, solo necesita *uno* paquete de R o Python para obtener una combinación específica de características.

| Nombre del paquete | Se aplica a | Descripción |
|--------------|----------|-------------|
|MSSQL-server-extensibilidad  | Todos | Marco de extensibilidad que se utiliza para ejecutar código R, Python o Java. |
|MSSQL-server-extensibilidad-java | Java | Extensión de Java para la carga de un entorno de ejecución de Java. No hay ninguna bibliotecas adicionales o paquetes para Java. |
| Microsoft openmpi  | Python, R | Interfaz utilizada por las bibliotecas Revo * para la paralelización en Linux que pasan mensajes. |
| [Microsoft-r-abierto *](#mro) | R | Distribución de código abierto de R, que consta de tres paquetes. |
| MSSQL-mlservices-python | Python | Distribución de código abierto de Anaconda y Python. |
|MSSQL-mlservices-mlm-py  | Python | Instalación completa. Proporciona modelos para el análisis de opinión de las características y el texto de imagen de revoscalepy, microsoftml, previamente entrenados.| 
|MSSQL-mlservices-mml-py  | Python | Instalación parcial. Proporciona revoscalepy, microsoftml. <br/>Excluye los modelos previamente entrenados. | 
|MSSQL-mlservices-paquetes-py  | Python | Instalación parcial. Proporciona revoscalepy. <br/>Excluye microsoftml y modelos previamente entrenados. | 
|MSSQL-mlservices-mlm-r  | R | Instalación completa. Proporciona modelos para el análisis de opinión de las características y el texto de imagen de RevoScaleR, MicrosoftML, sqlRUtils, olapR, previamente entrenados.| 
|MSSQL-mlservices-mml-r  | R | Instalación parcial. Proporciona RevoScaleR, MicrosoftML, sqlRUtils, olapR. <br/>Excluye los modelos previamente entrenados.  |
|MSSQL-mlservices-paquetes de r  | R | Instalación parcial. Proporciona RevoScaleR, sqlRUtils, olapR. <br/>Excluye los modelos previamente entrenados y MicrosoftML. | 

<a name="RHEL"></a>

## <a name="rhel-commands"></a>Comandos RHEL

Instalar cualquier *una* paquete de R, además de cualquier *uno* paquete de Python y Java si desea que esa capacidad. Cada paquete de R y Python incluye un conjunto de características. Elija el paquete que proporciona el conjunto de características que necesita. Los paquetes dependientes se incluyen automáticamente.

> [!Tip]
> Si es posible, ejecute `yum clean all` para actualizar paquetes en el sistema antes de la instalación.

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi extensiones (R, Python, Java), con bibliotecas de aprendizaje automático y modelos previamente entrenados para R y Python. R y Python, si quiere algo bien entre la instalación completa y mínimo: como bibliotecas de aprendizaje automático, pero sin los modelos previamente entrenados - sustituir `mssql-mlservices-mml-r-9.4.5*` y `mssql-mlservices-mml-py-9.4.5*` en su lugar.

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.5* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.5*
sudo yum install mssql-mlservices-mlm-r-9.4.5* 
sudo yum install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye R y Python, marco de extensibilidad, microsoft-openmpi core Revo * bibliotecas de código abierto de R y Python, extensión de Java. Excluye los modelos previamente entrenados y bibliotecas de R y Python de aprendizaje automático. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.5* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.5*
sudo yum install mssql-mlservices-packages-r-9.4.5*
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Comandos de Ubuntu

Instalar cualquier *una* paquete de R, además de cualquier *uno* paquete de Python y Java si desea que esa capacidad. Cada paquete de R y Python incluye un conjunto de características. Elija el paquete que proporciona el conjunto de características que necesita. Los paquetes dependientes se incluyen automáticamente.

> [!Tip]
> Si es posible, ejecute `apt-get update` para actualizar paquetes en el sistema antes de la instalación. Además, algunas imágenes de docker de Ubuntu podrían no tener la opción de apt transporte https. Para instalarlo, utilice `apt-get install apt-transport-https`.

<!---
### Prerequisite for 18.04

Running mssql-mlservices R libraries on Ubuntu 18.04 requires **libpng12** from the Linux Kernel archives. This package is no longer included in the standard distribution and must be installed manually. To get this library, run the following commands:

```bash
wget https://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb
dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb
```--->

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi extensiones (R, Python, Java), con bibliotecas de aprendizaje automático y modelos previamente entrenados para R y Python. Para instala R y Python, si quiere algo bien entre completo y los valores mínimo - como bibliotecas de aprendizaje automático, pero sin los modelos previamente entrenados - sustituir mssql-mlservices-mml-r y mssql-mlservices-mml-py en su lugar.

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
sudo apt-get install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye R y Python, marco de extensibilidad, microsoft-openmpi core Revo * bibliotecas de código abierto de R y Python, extensión de Java. Excluye los modelos previamente entrenados y bibliotecas de R y Python de aprendizaje automático. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

## <a name="suse-commands"></a>Comandos SUSE

Instalar cualquier *una* paquete de R, además de cualquier *uno* paquete de Python y Java si desea que esa capacidad. Cada paquete de R y Python incluye un conjunto de características. Elija el paquete que proporciona el conjunto de características que necesita. Los paquetes dependientes se incluyen automáticamente. 

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi extensiones (R, Python, Java), con bibliotecas de aprendizaje automático y modelos previamente entrenados para R y Python. R y Python, si quiere algo bien entre la instalación completa y mínimo: como bibliotecas de aprendizaje automático, pero sin los modelos previamente entrenados - sustituir `mssql-mlservices-mml-r-9.4.5*` y `mssql-mlservices-mml-py-9.4.5*` en su lugar.

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.5* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.5*
sudo zypper install mssql-mlservices-mlm-r-9.4.5* 
sudo zypper install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye R y Python, marco de extensibilidad, microsoft-openmpi core Revo * bibliotecas de código abierto de R y Python, extensión de Java. Excluye los modelos previamente entrenados y bibliotecas de R y Python de aprendizaje automático. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.5* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.5*
sudo zypper install mssql-mlservices-packages-r-9.4.5*
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configuración posterior a la instalación (requerido)

Configuración adicional es principalmente a través del [herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Agregue la cuenta de usuario de mssql usada para ejecutar el servicio Launchpad de SQL Server.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

2. Acepte los contratos de licencia de código abierto R y Python. Hay varias maneras de hacerlo. Si acepta la licencia de SQL Server antes y ahora va a agregar las extensiones de R o Python, el siguiente comando es su consentimiento a sus términos:

  ```bash
  # Run as SUDO or root
  # Use set + EULA 
    sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
  ```

  Un flujo de trabajo alternativo es que, si todavía no ha aceptado el motor de base de datos de SQL Server contrato de licencia, el programa de instalación detecta los paquetes de mssql mlservices y solicita la aceptación del CLUF cuando `mssql-conf setup` se ejecuta. Para obtener más información acerca de los parámetros de términos de licencia, consulte [configurar SQL Server con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

3. Reinicie el servicio Launchpad de SQL Server y la instancia del motor de base de datos.

  ```bash
  systemctl restart mssql-launchpadd

  systemctl restart mssql-server.service
  ```

4. Habilitar la ejecución de scripts externos en SQL Server Management Studio u otra herramienta que se ejecuta Transact-SQL. 

  ```bash
  EXEC sp_configure 'external scripts enabled', 1 
  RECONFIGURE WITH OVERRIDE 
  ```

## <a name="verify-installation"></a>Comprobar la instalación

Bibliotecas de R (RevoScaleR, MicrosoftML y otros) pueden encontrarse en `/opt/mssql/mlservices/libraries/RServer`.

Bibliotecas de Python (microsoftml y revoscalepy) pueden encontrarse en `/opt/mssql/mlservices/libraries/PythonServer`.

Con una herramienta de consulta de SQL Server, ejecute el siguiente comando SQL para probar la ejecución de R en SQL Server. Si no se ejecuta la secuencia de comandos, pruebe un reinicio del servicio, `sudo systemctl restart mssql-server`.

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
Ejecute el siguiente comando SQL para probar la ejecución de Python en SQL Server. 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## <a name="chained-installation"></a>Instalación encadenada

Puede instalar y configurar el motor de base de datos y Machine Learning Services en un procedimiento mediante la anexión de paquetes de R, Python o Java y parámetros en un comando que instala el motor de base de datos. 

El ejemplo siguiente es una ilustración de "plantilla" de una instalación de paquete combinado aspecto mediante el Administrador de paquetes Yum. Instala el motor de base de datos y agrega la extensión del lenguaje Java, que extrae el paquete de marco de extensibilidad como una dependencia.

```bash
sudo yum install -y mssql-server mssql-server-extensibility-java 
```

Un ejemplo con todas las extensiones (Java, R, Python) expandido tiene este aspecto:

```bash
sudo yum install -y mssql-server mssql-server-extensibility-java mssql-mlservices-packages-r-9.4.5* mssql-mlservices-packages-py-9.4.5*
```

Excepto para los requisitos previos de R, todos los paquetes utilizados en este ejemplo se encuentran en la misma ruta de acceso. Agregar R requiere que se [registrar el repositorio de paquetes de microsoft-r-open](#mro) como un paso adicional para obtener MRO. MRO es un requisito previo para la extensibilidad de R. En un equipo conectado a internet, MRO se recupera y se instala automáticamente como parte de la extensión de R, suponiendo que ha configurado ambos repositorios.

Después de la instalación, recuerde que debe usar la herramienta mssql-conf para configurar toda la instalación y acepte los contratos de licencia. CLUF no aceptada para componentes de R y Python de código abierto se detecta automáticamente y se le pedirá que acepte, junto con los términos de licencia para SQL Server.

```bash
sudo /opt/mssql/bin/mssql-conf setup MSSQL_PID=Developer 
```

## <a name="unattended-installation"></a>Instalación desatendida

Mediante el [instalación desatendida](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) para el motor de base de datos, agregue los paquetes para mssql mlservices y los CLUF.

Recuerde que el programa de instalación o la herramienta mssql-conf pide aceptación del contrato de licencia. Si ya ha había configurado el motor de base de datos de SQL Server y acepta sus términos de licencia, use uno de los parámetros de CLUF mlservices específicos para las distribuciones de R y Python de código abierto:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

Todas las posibles permutaciones de aceptación de términos de licencia se documentan en [configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Instalación sin conexión

Siga el [instalación sin conexión](sql-server-linux-setup.md#offline) instrucciones para conocer los pasos sobre cómo instalar los paquetes. Busque el sitio de descarga y, a continuación, descargue los paquetes específicos mediante la siguiente lista de paquetes.

> [!Tip]
> Algunas de las herramientas de administración de paquetes proporcionan los comandos que pueden ayudarle a determinan las dependencias del paquete. Use yum, `sudo yum deplist [package]`. Para Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Sitio de descarga

Puede descargar paquetes desde [ https://packages.microsoft.com/ ](https://packages.microsoft.com/). Todos los paquetes mlservices para R, Python y Java coexisten con el paquete del motor de base de datos. Versión de base para los paquetes mlservices es 9.4.5. Los paquetes de micrososoft-r-open están en una carpeta diferente.

#### <a name="rhel7-paths"></a>Rutas de acceso RHEL/7

|||
|--|----|
| MSSQL/mlservices paquetes | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| paquetes de Microsoft-r-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Rutas de acceso de Ubuntu/16.04

|||
|--|----|
| MSSQL/mlservices paquetes | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| paquetes de Microsoft-r-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Rutas de acceso SLES/12

|||
|--|----|
| MSSQL/mlservices paquetes | [ https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| paquetes de Microsoft-r-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>Lista de paquetes

Dependiendo de las extensiones que desea usar, descargar los paquetes necesarios para un idioma específico. Los nombres de archivo exactos incluyen información de la plataforma, pero los siguientes nombres de archivo deben ser lo suficientemente cerca como para determinar qué archivos se deben obtener.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-foreachiterators-3.4.4
microsoft-r-open-mkl-3.4.4
microsoft-r-open-mro-3.4.4
mssql-mlservices-packages-r-9.4.5
mssql-mlservices-mlm-r-9.4.5
mssql-mlservices-mml-r-9.4.5

# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.5
mssql-mlservices-packages-py-9.4.5
mssql-mlservices-mlm-py-9.4.5
mssql-mlservices-mml-py-9.4.5 
```

## <a name="add-more-rpython-packages"></a>Agregar más paquetes de R o Python 
 
Puede instalar otros paquetes de R y Python y usarlos en la secuencia de comandos que se ejecuta en SQL Server 2019.

### <a name="r-packages"></a>Paquetes de R 
 
1. Inicie una sesión de R.

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. Instalar un paquete de R denominado [adherencia](https://mran.microsoft.com/package/glue) para probar la instalación del paquete.

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   Como alternativa, puede instalar un paquete de R desde la línea de comandos 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. Importar el paquete de R en [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Paquetes de Python 
 
1. Instalar un paquete de Python denominado [httpie](https://httpie.org/) con pip. 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. Importar el paquete de Python en [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-20"></a>Limitaciones en CTP 2.0

Existen las siguientes limitaciones en esta versión de CTP.

+ Autenticación implícita no está disponible en Machine Learning Services en Linux en este momento, lo que significa que no se puede conectar al servidor desde un script de R o Python en curso para obtener acceso a datos u otros recursos. 

+ [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md) (para almacenar paquetes de R en la base de datos) no está disponible en Linux y no es compatible con Python.  

### <a name="resource-governance"></a>Regulación de recursos

Hay paridad entre Linux y Windows para [regulación de recursos](../t-sql/statements/create-external-resource-pool-transact-sql.md) para grupos de recursos externos, pero las estadísticas de [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) tienen actualmente unidades diferentes en Linux. Las unidades se alinearán en una próxima versión de CTP.
 
| Nombre de columna   | Descripción | Valor en Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | La cantidad máxima de memoria usada para el grupo de recursos. | En Linux, esta estadística se origina del subsistema de memoria CGroups, donde el valor es memory.max_usage_in_bytes |
|write_io_count | El total de E/s de escritura emitidas desde que se restablecieron las estadísticas del regulador de recursos. | En Linux, esta estadística se origina desde el subsistema de blkio CGroups, donde el valor en la fila de escritura es blkio.throttle.io_serviced | 
|read_io_count | El total de E/s de lectura emitidas desde que se restablecieron las estadísticas del regulador de recursos. | En Linux, esta estadística se origina desde el subsistema de blkio CGroups, donde el valor de la fila de lectura es blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | El usuario kernel tiempo de CPU acumulado en milisegundos desde que se restablecieron las estadísticas del regulador de recursos. | En Linux, esta estadística se origina desde el subsistema de cpuacct CGroups, donde el valor en la fila del usuario es cpuacct.stat |  
|total_cpu_user_ms | El tiempo acumulado usuario de la CPU en milisegundos desde que se restablecieron las estadísticas del regulador de recursos.| En Linux, esta estadística se origina desde el subsistema de cpuacct CGroups, donde el valor en el valor de la fila del sistema es cpuacct.stat | 
|active_processes_count | El número de procesos externos que se ejecutan en el momento de la solicitud.| En Linux, esta estadística se origina desde el subsistema de PID GGroups, donde el valor es pids.current | 

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecución de R en T-SQL](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecución de Python en T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis de en bases de datos para desarrolladores de Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en escenarios del mundo real, consulte [tutoriales de aprendizaje automático](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
