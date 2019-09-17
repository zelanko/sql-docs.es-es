---
title: Instalación de SQL Server Machine Learning Services (R, Python) en Linux
description: Aprenda a instalar SQL Server Machine Learning Services (R, Python) en Red Hat, Ubuntu y SUSE.
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 91bacc4ab4c8876ac49a09b58d1821f1c2853a3c
ms.sourcegitcommit: 3bd813ab2c56b415a952e5fbd5cfd96b361c72a2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70913560"
---
# <a name="install-sql-server-machine-learning-services-r-python-on-linux"></a>Instalación de SQL Server Machine Learning Services (R, Python) en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

A partir de esta versión preliminar de SQL Server 2019, [SQL Server Machine Learning Services](../advanced-analytics/index.yml) se puede ejecutar en sistemas operativos Linux. Siga los pasos de este artículo para instalar las extensiones de Machine Learning correspondientes a R y Python.

Machine Learning y las extensiones de programación son un complemento del motor de base de datos. Aunque puede [instalar el motor de base de datos y Machine Learning Services simultáneamente](#install-all), lo mejor es instalar y configurar el motor de base de datos de SQL Server primero para poder resolver cualquier problema antes de agregar más componentes. 

La ubicación del paquete de las extensiones de R y Python está en los repositorios de origen de SQL Server Linux. Si ya ha configurado repositorios de origen para la instalación del motor de base de datos, puede ejecutar los comandos de instalación de paquetes **mssql-mlservices** usando el mismo registro de repositorio.

Machine Learning Services también se admite en contenedores de Linux. No proporcionamos contenedores pregenerados con Machine Learning Services, pero puede crear uno a partir de los contenedores de SQL Server mediante [una plantilla de ejemplo disponible en GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="uninstall-previous-ctp"></a>Desinstalación de CTP anteriores

La lista de paquetes ha cambiado con las últimas versiones CTP, lo que ha dado lugar a menos paquetes. Antes de instalar CTP 3.2, se recomienda desinstalar CTP 2.x para quitar todos los paquetes anteriores. La instalación en paralelo de varias versiones no se admite.

### <a name="1-confirm-package-installation"></a>1. Confirmación de la instalación del paquete

Es posible que quiera comprobar la existencia de una instalación anterior como primer paso. Los archivos siguientes indican una instalación existente: checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. Desinstalación de paquetes anteriores de CTP 2.x

Realice la desinstalación en el nivel de paquete más bajo. Los paquetes ascendentes que dependan de un paquete de nivel inferior se desinstalarán automáticamente.

  + Para la integración de R, quite **microsoft-r-open***.
  + Para la integración de Python, quite **mssql-mlservices-python**.

Los comandos para quitar paquetes aparecen recogidos en la siguiente tabla.

| Plataforma  | Comandos de eliminación de paquetes | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> Microsoft R Open 3.4.4 se compone de dos o tres paquetes, según cuál sea la versión de CTP que haya instalado anteriormente. (El paquete foreachiterators se combinó en el paquete de MRO principal en CTP 2.2). Si alguno de estos paquetes sigue apareciendo después de quitar microsoft-r-open-mro-3.4.4, deberá quitarlo de forma individual.
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-32-install"></a>3. Proceder con la instalación de CTP 3.2

Realice la instalación en el nivel de paquete más alto, siguiendo las instrucciones de este artículo correspondientes a su sistema operativo.

En cada conjunto de instrucciones de instalación específico del sistema operativo, el *nivel de paquete más alto* será o **Ejemplo 1: instalación completa** en el caso del conjunto completo de paquetes o **Ejemplo 2: instalación mínima** si se trata del número mínimo de paquetes necesarios para una instalación viable.

1. Para la integración de R, empiece con [MRO](#mro), ya que es un requisito previo. La integración de R no se instalará sin MRO.

2. Ejecute los comandos de instalación mediante los administradores de paquetes y la sintaxis del sistema operativo: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisites

+ La versión de Linux debe ser [compatible con SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), pero no incluye el motor de Docker. Las versiones admitidas son:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (Solo R) [Microsoft R Open](#mro) proporciona la distribución de R base para la característica de R en SQL Server.

+ Debe tener una herramienta para ejecutar comandos de T-SQL. Se necesita un editor de consultas para la configuración y la validación posteriores a la instalación. Recomendamos [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), una descarga gratuita que se ejecuta en Linux.

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Instalación de Microsoft R Open (MRO)

La distribución base de R de Microsoft es un requisito previo para usar RevoScaleR, MicrosoftML y otros paquetes de R instalados con Machine Learning Services.

La versión necesaria es MRO 3.5.2.

Elija entre los dos métodos siguientes para instalar MRO:

+ Descargue el tarball de MRO desde MRAN, desempaquételo y ejecute el script install.sh. Si quiere usar este método, puede seguir las [instrucciones de instalación en MRAN](https://mran.microsoft.com/releases/3.5.2).

+ También puede registrar el repositorio **packages.microsoft.com** como se describe a continuación para instalar los dos paquetes que componen la distribución de MRO: microsoft-r-open-mro y microsoft-r-open-mkl. 

Los siguientes comandos registran el repositorio que proporciona MRO. Tras el registro, los comandos para instalar otros paquetes de R (como mssql-mlservices-mml-r) incluirán automáticamente MRO como una dependencia de paquete.

#### <a name="mro-on-ubuntu"></a>MRO en Ubuntu

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-rhel"></a>MRO en RHEL

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```
#### <a name="mro-on-suse"></a>MRO en SUSE

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

## <a name="package-list"></a>Lista de paquetes

En un dispositivo conectado a Internet, los paquetes se descargan e instalan de forma independiente del motor de base de datos mediante el instalador de paquetes de cada sistema operativo. En la siguiente tabla se describen todos los paquetes disponibles, pero para R y Python hay que especificar paquetes que proporcionen la instalación completa de características o la instalación mínima de características.

| Nombre del paquete | Válido para | Descripción |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | Marco de extensibilidad que se usa para ejecutar código de R y Python. |
| microsoft-openmpi  | Python, R | Interfaz de paso de mensajes usada por las bibliotecas Revo* para la paralelización en Linux. |
| mssql-mlservices-python | Python | Distribución de código abierto de Anaconda y Python. |
|mssql-mlservices-mlm-py  | Python | *Instalación completa*. Proporciona revoscalepy, microsoftml, modelos entrenados previamente para las características de imágenes y análisis de opiniones de texto.| 
|mssql-mlservices-packages-py  | Python | *Instalación mínima*. Proporciona revoscalepy y microsoftml. <br/>Excluye los modelos previamente entrenados. | 
| [microsoft-r-open*](#mro) | R | Distribución de código abierto de R, formada por tres paquetes. |
|mssql-mlservices-mlm-r  | R | *Instalación completa*. Proporciona RevoScaleR, MicrosoftML, sqlRUtils, olapR, modelos entrenados previamente para las características de imágenes y análisis de opiniones de texto.| 
|mssql-mlservices-packages-r  | R | *Instalación mínima*. Proporciona RevoScaleR, sqlRUtils, MicrosoftML, olapr. <br/>Excluye los modelos previamente entrenados. | 
|mssql-mlservices-mml-py  | Solo CTP 2.0-2.1 | Obsoleto en CTP 2.2 debido a la consolidación de paquetes de Python en mssql-mslservices-python. Proporciona revoscalepy. Excluye los modelos previamente entrenados y microsoftml.| 
|mssql-mlservices-mml-r  | Solo CTP 2.0-2.1 | Obsoleto en CTP 2.2 debido a la consolidación de paquetes de R en mssql-mslservices-python. Proporciona RevoScaleR, sqlRUtils, olapr. Excluye los modelos previamente entrenados y MicrosoftML.  |

<a name="RHEL"></a>

## <a name="redhat-commands"></a>Comandos de RedHat

Puede instalar la compatibilidad con idiomas en cualquier combinación que necesite (uno o varios idiomas). Para R y Python, hay dos paquetes entre los que elegir. Uno proporciona todas las características disponibles, presentado como *instalación completa*. La opción alternativa excluye los modelos de Machine Learning previamente entrenados y se presenta como *instalación mínima*.

> [!Tip]
> Si es posible, ejecute `yum clean all` para actualizar los paquetes en el sistema antes de la instalación.

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye R y Python de código abierto, Extensibility Framework, microsoft-openmpi, extensiones (R, Python), con bibliotecas de Machine Learning y modelos previamente entrenados para R y Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye R y Python de código abierto, Extensibility Framework, microsoft-openmpi, bibliotecas Revo* básicas y bibliotecas de Machine Learning para R y Python. Excluye los modelos previamente entrenados.

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Comandos de Ubuntu

Puede instalar la compatibilidad con idiomas en cualquier combinación que necesite (uno o varios idiomas). Para R y Python, hay dos paquetes entre los que elegir. Uno proporciona todas las características disponibles, presentado como *instalación completa*. La opción alternativa excluye los modelos de Machine Learning previamente entrenados y se presenta como *instalación mínima*.

> [!Tip]
> Si es posible, ejecute `apt-get update` para actualizar los paquetes en el sistema antes de la instalación. Además, algunas imágenes de Docker de Ubuntu podrían no tener la opción https apt transport. Para instalarla, use `apt-get install apt-transport-https`.

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye R y Python de código abierto, Extensibility Framework, microsoft-openmpi, extensiones (R, Python), con bibliotecas de Machine Learning y modelos previamente entrenados para R y Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye R y Python de código abierto, Extensibility Framework, microsoft-openmpi, bibliotecas Revo* básicas y bibliotecas de Machine Learning para R y Python. Excluye los modelos previamente entrenados. 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>Comandos de SUSE

Puede instalar la compatibilidad con idiomas en cualquier combinación que necesite (uno o varios idiomas). Para R y Python, hay dos paquetes entre los que elegir. Uno proporciona todas las características disponibles, presentado como *instalación completa*. La opción alternativa excluye los modelos de Machine Learning previamente entrenados y se presenta como *instalación mínima*.

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye R y Python de código abierto, Extensibility Framework, microsoft-openmpi, extensiones (R, Python), con bibliotecas de Machine Learning y modelos previamente entrenados para R y Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye R y Python de código abierto, Extensibility Framework, microsoft-openmpi, bibliotecas Revo* básicas y bibliotecas de Machine Learning para R y Python. Excluye los modelos previamente entrenados. 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>Configuración posterior a la instalación (obligatoria)

La configuración adicional se realiza principalmente a través de la [herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Agregue la cuenta de usuario de mssql usada para ejecutar el servicio SQL Server. Esto es necesario si no ha ejecutado la instalación previamente.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Acepte los contratos de licencia de R y Python de código abierto. Existen varias formas de hacerlo: Si anteriormente aceptó licencias de SQL Server y ahora está agregando las extensiones de R o Python, el siguiente comando constituye la aceptación por su parte de los términos:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   Un flujo de trabajo alternativo es que, si aún no ha aceptado el contrato de licencia del motor de base de datos de SQL Server, el programa de instalación detecte los paquetes mssql-mlservices y solicite la aceptación del contrato de licencia cuando `mssql-conf setup` se ejecute. Para más información sobre los parámetros EULA, vea [Configuración de SQL Server con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

3. Habilite el acceso de red saliente. El acceso de red saliente está deshabilitado de forma predeterminada. Para habilitar las solicitudes salientes, establezca la propiedad booleana "outboundnetworkaccess" con la herramienta mssql-conf. Para más información, vea [Configuración de SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Solo de cara a la integración de características de R, establezca la variable de entorno **MKL_CBWR** para [garantizar una salida coherente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de los cálculos de la biblioteca Math Kernel Library (MKL) de Intel.

   + Edite o cree un archivo llamado **.bash_profile** en su directorio principal de usuario, agregando la línea `export MKL_CBWR="AUTO"` al archivo.

   + Ejecute este archivo escribiendo `source .bash_profile` en un símbolo del sistema de Bash.

5. Reinicie el servicio SQL Server Launchpad y la instancia del motor de base de datos para leer los valores actualizados del archivo INI. En un mensaje de reinicio se le recuerda si se ha modificado un valor relacionado con la extensibilidad.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. Habilite la ejecución de scripts externos con Azure Data Studio u otra herramienta como SQL Server Management Studio (solo Windows) que ejecute Transact-SQL. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Vuelva a reiniciar el servicio Launchpad.

## <a name="verify-installation"></a>Comprobar la instalación

Las bibliotecas de R (MicrosoftML, RevoScaleR y otras) se encuentran en `/opt/mssql/mlservices/libraries/RServer`.

Las bibliotecas de Python (microsoftml y revoscalepy) se encuentran en `/opt/mssql/mlservices/libraries/PythonServer`.

Para validar la instalación, ejecute un script de T-SQL que ejecute un procedimiento almacenado del sistema que invoque a R o Python. Necesita una herramienta de consulta para esta tarea. Azure Data Studio es una buena elección. Otras herramientas que se usan con frecuencia, como SQL Server Management Studio o PowerShell, son solo para Windows. Si tiene un equipo Windows con estas herramientas, úselo para conectarse a la instalación de Linux del motor de base de datos.

Ejecute el siguiente comando SQL para probar la ejecución de R en SQL Server. Si el script no se ejecuta, pruebe a reiniciar el servicio, `sudo systemctl restart mssql-server.service`.

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

## <a name="chained-combo-install"></a>Instalación "combinada" encadenada

Puede instalar y configurar el motor de base de datos y Machine Learning Services en un procedimiento si anexa paquetes y parámetros de R o Python en un comando que instala el motor de base de datos. 

1. Para la integración de R, instale [Microsoft R Open](#mro) como requisito previo. Omita este paso si no va a instalar la característica de R.

2. Proporcione una línea de comandos que incluya el motor de base de datos, además de las características de la extensión de lenguaje.

  Puede agregar una única característica, como la integración de Python, a una instalación del motor de base de datos.

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  También puede agregar ambas (R y Python).

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. Acepte los contratos de licencia y complete la configuración posterior a la instalación. Use la herramienta **mssql-conf** para esta tarea.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Se le pedirá que acepte el contrato de licencia del motor de base de datos, que elija una edición y que establezca la contraseña de administrador. También se le pedirá que acepte el contrato de licencia de Machine Learning Services.

4. Reinicie el servicio, si se le pide.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>Instalación desatendida

Mediante la [instalación desatendida](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) del motor de base de datos, agregue los paquetes de mssql-mlservices y los contratos de licencia.

Recuerde que el programa de instalación o la herramienta mssql-conf le pedirán que acepte el contrato de licencia. Si ya configuró el motor de base de datos de SQL Server y aceptó el contrato de licencia correspondiente, use uno de los parámetros EULA específicos de mlservices para las distribuciones de R y Python de código abierto:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

Todas las permutaciones posibles de aceptación del contrato de licencia se documentan en [Configuración de SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Instalación sin conexión

Siga las instrucciones de [instalación sin conexión](sql-server-linux-setup.md#offline) para ver los pasos para instalar los paquetes. Busque el sitio de descarga y luego descargue paquetes específicos mediante la lista de paquetes siguiente.

> [!Tip]
> Varias de las herramientas de administración de paquetes proporcionan comandos que pueden ayudar a determinar las dependencias de los paquetes. En yum, use `sudo yum deplist [package]`. En Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido de `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Sitio de descarga

Puede descargar paquetes desde [https://packages.microsoft.com/](https://packages.microsoft.com/). Todos los paquetes mlservices de R y Python se colocan con el paquete del motor de base de datos. La versión base de los paquetes mlservices es 9.4.5 (para CTP 2.0) o 9.4.6 (para CTP 2.1 y versiones posteriores). Recuerde que los paquetes microsoft-r-open están en un [repositorio diferente](#mro).

#### <a name="rhel7-paths"></a>Rutas de acceso de RHEL/7

|||
|--|----|
| Paquetes mssql/mlservices | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| Paquetes microsoft-r-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Rutas de acceso de Ubuntu/16.04

|||
|--|----|
| Paquetes mssql/mlservices | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| Paquetes microsoft-r-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Rutas de acceso de SLES/12

|||
|--|----|
| Paquetes mssql/mlservices | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| Paquetes microsoft-r-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>Lista de paquetes

En función de las extensiones que quiera usar, descargue los paquetes necesarios relativos a un lenguaje específico. Los nombres de archivo exactos incluyen información de la plataforma en el sufijo, pero los nombres de archivo siguientes deben ser lo suficientemente cercanos para que pueda determinar qué archivos va a obtener.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="add-more-rpython-packages"></a>Agregar más paquetes de R/Python 
 
Puede instalar otros paquetes de R y Python y usarlos en un script que se ejecute en SQL Server 2019.

### <a name="r-packages"></a>Paquetes de R 
 
1. Inicie una sesión de R.

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. Instale un paquete de R denominado [glue](https://mran.microsoft.com/package/glue) para comprobar la instalación del paquete.

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   Otra alternativa consiste en instalar un paquete de R desde la línea de comandos. 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. Importe el paquete de R en [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Paquetes de Python 
 
1. Instale un paquete de Python llamado [httpie](https://httpie.org/) mediante pip. 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. Importe el paquete de Python en [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>Limitaciones de las versiones de CTP

La integración de R y Python en Linux sigue estando en desarrollo activo. Las siguientes características aún no están habilitadas en la versión preliminar.

+ En este momento, la autenticación implícita no está disponible en Machine Learning Services, lo que significa que no se puede volver a conectar al servidor desde un script de R y Python en curso para acceder a datos u otros recursos. 

### <a name="resource-governance"></a>Regulación de recursos

Existe paridad entre Linux y Windows para la [regulación de recursos](../t-sql/statements/create-external-resource-pool-transact-sql.md) de los grupos de recursos externos, pero las estadísticas de [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) tienen actualmente unidades diferentes en Linux. Las unidades se van a alinear en una próxima versión de CTP.
 
| Nombre de columna   | Descripción | Valor en Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | Cantidad máxima de memoria usada con el grupo de recursos | En Linux, esta estadística tiene como origen el subsistema CGroups memory, donde el valor es memory.max_usage_in_bytes. |
|write_io_count | Total de operaciones de E/S de escritura emitidas desde el restablecimiento de las estadísticas de Resource Governor | En Linux, esta estadística tiene como origen el subsistema CGroups blkio, donde el valor de la fila de escritura es blkio.throttle.io_serviced. | 
|read_io_count | Total de operaciones de E/S de lectura emitidas desde el restablecimiento de las estadísticas de Resource Governor | En Linux, esta estadística tiene como origen el subsistema CGroups blkio, donde el valor de la fila de lectura es blkio.throttle.io_serviced. | 
|total_cpu_kernel_ms | Tiempo del kernel de usuario de CPU acumulativo en milisegundos desde el restablecimiento de las estadísticas de Resource Governor | En Linux, esta estadística tiene como origen el subsistema CGroups cpuacct, donde el valor de la fila de usuario es cpuacct.stat. |  
|total_cpu_user_ms | Tiempo de usuario de CPU acumulativo en milisegundos desde el restablecimiento de las estadísticas de Resource Governor| En Linux, esta estadística tiene como origen el subsistema CGroups cpuacct, donde el valor de la fila de sistema es cpuacct.stat. | 
|active_processes_count | Número de procesos externos que se ejecutan en el momento de la solicitud| En Linux, esta estadística tiene como origen el subsistema GGroups pids, donde el valor es pids.current. | 

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar con algunos ejemplos sencillos y conocer los aspectos básicos del funcionamiento de R con SQL Server. Para conocer el siguiente paso, vea los vínculos siguientes:

+ [Tutorial: Ejecutar R en T-SQL](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server con estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para obtener ejemplos de Machine Learning basados en escenarios del mundo real, vea los [tutoriales sobre Machine Learning](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
