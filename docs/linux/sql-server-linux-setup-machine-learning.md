---
title: Instalar SQL Server Machine Learning Services (R, Python y Java) en Linux | Microsoft Docs
description: Este artículo describe cómo instalar SQL Server Machine Learning Services (R, Python, Java) en Red Hat y Ubuntu.
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15a1a411672303fc8556927bcaf218052758744d
ms.sourcegitcommit: 2f5773f4bc02bfff4f2924226ac5651eb0c00924
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53553257"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-java-on-linux"></a>Instalar SQL Server 2019 Machine Learning Services (R, Python y Java) en Linux

[SQL Server Machine Learning Services](../advanced-analytics/what-is-sql-server-machine-learning.md) se ejecuta en sistemas operativos de Linux a partir de esta versión preliminar de SQL Server 2019. Siga los pasos descritos en este artículo para instalar la extensión de programación Java, o el aprendizaje automático extensiones para R y Python. 

Aprendizaje automático y las extensiones de programación es un complemento para el motor de base de datos. Aunque puede [instalar el motor de base de datos y Machine Learning Services simultáneamente](#install-all), es una práctica recomendada para instalar y configurar primero el motor de base de datos de SQL Server para que pueda resolver los problemas antes de agregar más componentes. 

Ubicación del paquete para las extensiones de R, Python y Java se encuentran en los repositorios de código fuente de SQL Server para Linux. Si ya ha configurado los repositorios de código fuente para la instalación del motor de base de datos, puede ejecutar el **mssql mlservices** comandos de instalación con el mismo repositorio de registro del paquete.

## <a name="uninstall-previous-ctp"></a>Desinstalación de CTP anterior

Ha cambiado la lista de paquetes a través de las versiones CTP más recientes, lo que resulta en menos de paquetes. Se recomienda desinstalar el CTP 2.0 o 2.1 para quitar todos los paquetes anteriores antes de instalar la versión de CTP 2.2 o posterior. No se admite la instalación en paralelo de varias versiones.

### <a name="1-confirm-package-installation"></a>1. Confirmar la instalación del paquete

Es posible que desee comprobar la existencia de una instalación anterior como primer paso. Los siguientes archivos indican una instalación existente: checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-ctp-20-or-21-packages"></a>2. Desinstalación de CTP 2.0 o 2.1 paquetes

Desinstalar en el nivel más bajo del paquete. Cualquier paquete ascendente depende de un paquete de nivel inferior se desinstala automáticamente.

  + Para la integración de R, quitar **abierta de r de microsoft***
  + Para la integración de Python, quitar **mssql-mlservices-python**
  + Para la integración de Java, quitar **mssql-server-extensibilidad-java**

Comandos para quitar paquetes aparecen en la tabla siguiente.

| Plataforma  | Comandos de eliminación de paquete | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python`<br/>`sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python`<br/>`sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`<br/>`sudo apt-get remove msssql-server-extensibility-java`|

> [!Note]
> Microsoft R Open se compone de tres paquetes. Si cualquiera de estos paquetes permanecen después de quitar microsoft r open mro 3.4.4, debe quitarlos individualmente.
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-22-install"></a>3. Continuar con la instalación de CTP 2.2

Instalar en el nivel más alto de paquete con las instrucciones de este artículo para su sistema operativo.

Para cada conjunto de instrucciones de instalación, específicos del sistema operativo *más alto nivel de paquete* sea **ejemplo 1: instalación completa** para todo el conjunto de paquetes, o **ejemplo 2: instalación mínima**  el menor número de paquetes necesarios para realizar una instalación viable.

1. Para la integración de R, comience con [MRO](#mro) porque es un requisito previo. Integración de R no se instalará sin él.

2. Ejecute los comandos de instalación con los administradores de paquetes y la sintaxis para su sistema operativo: 

   + [Red Hat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#SUSE)

## <a name="prerequisites"></a>Requisitos previos

+ Debe ser la versión de Linux [compatibles con SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), ejecutándose localmente o en un contenedor de Docker. Las versiones admitidas incluyen:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (Solo para R) [Microsoft R Open](#mro) proporciona la distribución de R base para la característica de R en SQL Server

+ Debe tener una herramienta para ejecutar comandos de T-SQL. Un editor de consultas es necesario para la validación y configuración posterior a la instalación. Se recomienda [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), una descarga gratuita que se ejecuta en Linux.

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

# Update packages on your system (required), including MRO installation
sudo apt-get update
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

En un dispositivo conectado a internet, los paquetes se descargan e instalan independientemente el motor de base de datos mediante el instalador de paquetes para cada sistema operativo. La tabla siguiente describen todos los paquetes disponibles, pero R y Python, especificar los paquetes que proporcionan la instalación de todas las características o la instalación de características mínimo.

| Nombre del paquete | Se aplica a | Descripción |
|--------------|----------|-------------|
|MSSQL-server-extensibilidad  | All | Marco de extensibilidad que se utiliza para ejecutar código R, Python o Java. |
|MSSQL-server-extensibilidad-java | Java | Extensión de Java para la carga de un entorno de ejecución de Java. No hay ninguna bibliotecas adicionales o paquetes para Java. |
| Microsoft openmpi  | Python, R | Interfaz utilizada por las bibliotecas Revo * para la paralelización en Linux que pasan mensajes. |
| MSSQL-mlservices-python | Python | Distribución de código abierto de Anaconda y Python. |
|MSSQL-mlservices-mlm-py  | Python | *Instalación completa*. Proporciona modelos para el análisis de opinión de las características y el texto de imagen de revoscalepy, microsoftml, previamente entrenados.| 
|MSSQL-mlservices-paquetes-py  | Python | *Instalación mínima*. Proporciona microsoftml y revoscalepy. <br/>Excluye los modelos previamente entrenados. | 
| [Microsoft-r-abierto *](#mro) | R | Distribución de código abierto de R, que consta de tres paquetes. |
|MSSQL-mlservices-mlm-r  | R | *Instalación completa*. Proporciona modelos para el análisis de opinión de las características y el texto de imagen de RevoScaleR, MicrosoftML, sqlRUtils, olapR, previamente entrenados.| 
|MSSQL-mlservices-paquetes de r  | R | *Instalación mínima*. Proporciona RevoScaleR, sqlRUtils, MicrosoftML, olapR. <br/>Excluye los modelos previamente entrenados. | 
|MSSQL-mlservices-mml-py  | CTP 2.0 2.1 | Ha quedado obsoleto en CTP 2.2 debido a la consolidación de paquete de Python en mssql-mslservices-python. Proporciona revoscalepy. Excluye microsoftml y modelos previamente entrenados.| 
|MSSQL-mlservices-mml-r  | CTP 2.0 2.1 | Ha quedado obsoleto en CTP 2.2 debido a la consolidación de paquete de R en mssql-mslservices-python. Proporciona RevoScaleR, sqlRUtils, olapR. Excluye los modelos previamente entrenados y MicrosoftML.  |

<a name="RHEL"></a>

## <a name="rhel-commands"></a>Comandos RHEL

Puede instalar compatibilidad con idiomas en cualquier combinación requiere (uno o varios lenguajes). R y Python, hay dos paquetes que puede elegir. Uno proporciona todas las características disponibles, caracterizadas como el *instalación completa*. La opción alternativa excluye lo modelos de aprendizaje automático previamente entrenado y se considera el *instalación mínima*.

> [!Tip]
> Si es posible, ejecute `yum clean all` para actualizar paquetes en el sistema antes de la instalación.

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi extensiones (R, Python, Java), con bibliotecas de aprendizaje automático y modelos previamente entrenados para R y Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.6*
sudo yum install mssql-mlservices-mlm-r-9.4.6* 
sudo yum install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi, Revo * bibliotecas de core y bibliotecas de aprendizaje automático para R y Python y la extensión de Java. Excluye los modelos previamente entrenados.

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.6*
sudo yum install mssql-mlservices-packages-r-9.4.6*
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Comandos de Ubuntu

Puede instalar compatibilidad con idiomas en cualquier combinación requiere (uno o varios lenguajes). R y Python, hay dos paquetes que puede elegir. Uno proporciona todas las características disponibles, caracterizadas como el *instalación completa*. La opción alternativa excluye lo modelos de aprendizaje automático previamente entrenado y se considera el *instalación mínima*.

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

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi extensiones (R, Python, Java), con bibliotecas de aprendizaje automático y modelos previamente entrenados para R y Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
sudo apt-get install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi, Revo * bibliotecas de core y bibliotecas de aprendizaje automático para R y Python y la extensión de Java. Excluye los modelos previamente entrenados. 

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

Puede instalar compatibilidad con idiomas en cualquier combinación requiere (uno o varios lenguajes). R y Python, hay dos paquetes que puede elegir. Uno proporciona todas las características disponibles, caracterizadas como el *instalación completa*. La opción alternativa excluye lo modelos de aprendizaje automático previamente entrenado y se considera el *instalación mínima*.

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi extensiones (R, Python, Java), con bibliotecas de aprendizaje automático y modelos previamente entrenados para R y Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.6*
sudo zypper install mssql-mlservices-mlm-r-9.4.6* 
sudo zypper install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye código abierto R y Python, marco de extensibilidad, microsoft-openmpi, Revo * bibliotecas de core y bibliotecas de aprendizaje automático para R y Python y la extensión de Java. Excluye los modelos previamente entrenados. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.6*
sudo zypper install mssql-mlservices-packages-r-9.4.6*
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configuración posterior a la instalación (requerido)

Configuración adicional es principalmente a través del [herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Agregue la cuenta de usuario de mssql usada para ejecutar el servicio de SQL Server. Esto es necesario si no ha ejecutado el programa de instalación anteriormente.

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

3. Para R característica integración única, establezca el **MKL_CBWR** variable de entorno [garantizar resultados coherentes](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de cálculos de Intel Math Kernel Library (MKL).

  + Edite o cree un archivo denominado **. bash_profile** en su directorio principal de usuario, agregue la línea `export MKL_CBWR="AUTO"` al archivo.

  + Ejecute este archivo escribiendo `source .bash_profile` en un símbolo del sistema de bash.

4. Reinicie el servicio Launchpad de SQL Server y la instancia del motor de base de datos. 

  ```bash
  systemctl restart mssql-launchpadd

  systemctl restart mssql-server.service
  ```

5. Habilitar la ejecución del script externo mediante Azure Data Studio u otra herramienta como SQL Server Management Studio (solo Windows) que ejecuta Transact-SQL. 

  ```bash
  EXEC sp_configure 'external scripts enabled', 1 
  RECONFIGURE WITH OVERRIDE 
  ```

6. Vuelva a reiniciar el servicio Launchpad.

## <a name="verify-installation"></a>Comprobar la instalación

Bibliotecas de R (RevoScaleR, MicrosoftML y otros) pueden encontrarse en `/opt/mssql/mlservices/libraries/RServer`.

Bibliotecas de Python (microsoftml y revoscalepy) pueden encontrarse en `/opt/mssql/mlservices/libraries/PythonServer`.

Característica de integración de Java no incluye las bibliotecas, pero puede ejecutar `grep -r JAVA_HOME /etc` para confirmar la creación de la variable de entorno JAVA_HOME.

Para validar la instalación, ejecute un script de Transact-SQL que ejecuta un procedimiento almacenado del sistema invocar R o Python. Necesitará una herramienta de consulta para esta tarea. Azure Data Studio es una buena elección. Otras herramientas utilizadas habitualmente, como SQL Server Management Studio o PowerShell sólo Windows. Si tiene un equipo Windows con estas herramientas, puede usar para conectarse a la instalación de Linux del motor de base de datos.

Ejecute el siguiente comando SQL para probar la ejecución de R en SQL Server. Si no se ejecuta la secuencia de comandos, pruebe un reinicio del servicio, `sudo systemctl restart mssql-server.service`.

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

## <a name="chained-combo-install"></a>Instala encadenada "combinado"

Puede instalar y configurar el motor de base de datos y Machine Learning Services en un procedimiento mediante la anexión de paquetes de R, Python o Java y parámetros en un comando que instala el motor de base de datos. 

1. Para la integración de R, instale [Microsoft R Open](#mro) como requisito previo. Omita este paso si no va a instalar la característica de R.

2. Proporcionar una línea de comandos que incluye el motor de base de datos, además de características de extensión del lenguaje.

  Puede agregar una sola función, como Java, instale integración a un motor de base de datos.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

  O bien, agregue todas las extensiones (Java, R, Python).

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java mssql-mlservices-packages-r-9.4.6* mssql-mlservices-packages-py-9.4.6*
  ```

3. Acepte los contratos de licencia y completar la configuración posterior a la instalación. Use la **mssql-conf** herramienta para esta tarea.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Se le pedirá que acepte el contrato de licencia para el motor de base de datos, elija una edición y establecer la contraseña de administrador. También se le pedirá que acepte el contrato de licencia de Machine Learning Services.

4. Reinicie el servicio, si se le pide que lo haga.

  ```bash
  sudo systemctl restart mssql-server.service
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

Puede descargar paquetes desde [ https://packages.microsoft.com/ ](https://packages.microsoft.com/). Todos los paquetes mlservices para R, Python y Java coexisten con el paquete del motor de base de datos. Versión de base para los paquetes mlservices es 9.4.5 (para CTP 2.0) 9.4.6 (para CTP 2.1 y versiones posteriores). Recuerde que los paquetes de microsoft-r-open están en un [otro repositorio](#mro).

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

Dependiendo de las extensiones que desea usar, descargar los paquetes necesarios para un idioma específico. Los nombres de archivo exactos incluyen información de la plataforma en el sufijo, pero los siguientes nombres de archivo deben ser lo suficientemente cerca como para determinar qué archivos se deben obtener.

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
mssql-mlservices-packages-r-9.4.6.523
mssql-mlservices-mlm-r-9.4.6.523
mssql-mlservices-mml-r-9.4.6.523

# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.6.523
mssql-mlservices-packages-py-9.4.6.523
mssql-mlservices-mlm-py-9.4.6.523
mssql-mlservices-mml-py-9.4.6.523
```

#### <a name="package-list-for-original-ctp-20-and-21"></a>Lista de paquetes para original CTP 2.0 y 2.1

CTP 2.2 quita **mssql-mlservices-mlm-py** y **mssql-mlservices-mlm-r** mediante la consolidación de paquete en **mssql-mlservices-paquetes-py** y **mssql-mlservices-paquetes de r**, respectivamente.

Si necesita específicamente la original CTP 2.0 o 2.1 paquetes, descargue los paquetes siguientes:

* Para CTP 2.0, descargue las versiones del paquete 9.4.5

* Para CTP 2.1, descargue las versiones del paquete 9.4.6.237


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

## <a name="limitations-in-ctp-releases"></a>Limitaciones en las versiones CTP

Integración de R, Python y Java en Linux está todavía en desarrollo activo. Las siguientes características aún no están habilitadas en la versión preliminar.

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

+ [Tutorial: Ejecutar R en T-SQL](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis en bases de datos para los desarrolladores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecución de Python en T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis en bases de datos para desarrolladores de Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en escenarios del mundo real, consulte [tutoriales de aprendizaje automático](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
