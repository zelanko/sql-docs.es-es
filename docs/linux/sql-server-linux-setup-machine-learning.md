---
title: Instalación de SQL Server Machine Learning Services (Python, R) en Linux
description: 'Obtenga información sobre cómo instalar SQL Server Machine Learning Services (Python y R) en Linux: Red Hat, Ubuntu y SUSE.'
author: cawrites
ms.author: chadam
ms.reviewer: vanto
manager: cgronlun
ms.date: 03/05/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bf474ff8a7587c916591e6d7ba4dc82052b516f7
ms.sourcegitcommit: fc99fdd586eabc2d60f33056123398f263d5913d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2020
ms.locfileid: "78937650"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>Instalación de SQL Server Machine Learning Services (Python y R) en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se le guiará por la instalación de [SQL Server Machine Learning Services](../advanced-analytics/index.yml) en Linux. Se pueden ejecutar scripts de Python y R en la base de datos mediante Machine Learning Services.

[!NOTE]
> Machine Learning Services se instala de forma predeterminada en los clústeres de macrodatos de SQL Server. Para más información, vea [Uso de Machine Learning Services (Python y R) en Clústeres de macrodatos](../big-data-cluster/machine-learning-services.md)

## <a name="what-are-machine-learning-services"></a>¿Qué es Machine Learning Services?

Machine Learning Services es un complemento de características para el motor de base de datos.

Instale y configure el motor de base de datos de SQL Server primero para poder resolver los problemas antes de agregar más componentes.

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

[Instale SQL Server en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup) y compruebe la instalación.

* Compruebe en los repositorios de SQL Server para Linux si están las extensiones de Python y R. 
* Si ya ha configurado repositorios de origen para la instalación del motor de base de datos, puede ejecutar los comandos de instalación de paquetes **mssql-mlservices** usando el mismo registro de repositorio.

* [Microsoft R Open](#mro) proporciona la distribución de R base para la característica de R en SQL Server

* Debe tener una herramienta para ejecutar comandos de T-SQL. 
* Se necesita un editor de consultas para la configuración y la validación posteriores a la instalación. 
* Recomendamos [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), una descarga gratuita que se ejecuta en Linux.


<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Instalación de Microsoft R Open (MRO)

La distribución base de R de Microsoft es un requisito previo para usar RevoScaleR, MicrosoftML y otros paquetes de R instalados con Machine Learning Services.

La versión necesaria es MRO 3.5.2.

Elija entre los dos métodos siguientes para instalar MRO:

+ Descargue el tarball de MRO desde MRAN, desempaquételo y ejecute el script install.sh. Si quiere usar este método, puede seguir las [instrucciones de instalación en MRAN](https://mran.microsoft.com/releases/3.5.2).

+ Registre el repositorio **packages.microsoft.com** como se describe a continuación para instalar la distribución de MRO: microsoft-r-open-mro y microsoft-r-open-mkl. 

<a name="RHEL"></a>

## <a name="install-on-redhat"></a>Instalación en RedHat

### <a name="install-mro-on-red-hat"></a>Instalación (MRO) en Red Hat

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

Opciones de instalación para Python y R:

*  Instale la compatibilidad de lenguaje según los requisitos (uno o varios lenguajes).
*  En la *instalación completa* se proporcionan todas las características disponibles, incluidos los modelos de aprendizaje automático entrenados previamente.
*  La *instalación mínima* excluye los modelos pero todavía mantiene toda la funcionalidad.

> [!Tip]
> Si es posible, ejecute `yum clean all` para actualizar los paquetes en el sistema antes de la instalación.

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa

Incluye:
*  Python de código abierto
*  R de código abierto
*  Plataforma de extensibilidad
*  microsoft-openmpi
*  Extensiones (Python, R)
*  Bibliotecas de aprendizaje automático
*  Modelos entrenados previamente para Python y R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7*
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima

Incluye:
*  Python de código abierto
*  R de código abierto
*  Plataforma de extensibilidad
*  microsoft-openmpi
*  Bibliotecas Revo* básicas
*  Bibliotecas de aprendizaje automático

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```
<a name="ubuntu"></a>

## <a name="install-on-ubuntu"></a>Instalación en Ubuntu

### <a name="install-mro-on-ubuntu"></a>Instalación (MRO) en Ubuntu

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

Opciones de instalación para Python y R:

*  Instale la compatibilidad de lenguaje según los requisitos (uno o varios lenguajes).
*  En la *instalación completa* se proporcionan todas las características disponibles, incluidos los modelos de aprendizaje automático entrenados previamente.
*  La *instalación mínima* excluye los modelos pero todavía mantiene toda la funcionalidad.

> [!Tip]
> Si es posible, ejecute `apt-get update` para actualizar los paquetes en el sistema antes de la instalación. 

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye:
*  Python de código abierto
*  R de código abierto
*  Plataforma de extensibilidad
*  microsoft-openmpi
*  Extensiones de Python
*  Extensiones de R
*  Bibliotecas de aprendizaje automático
*  Modelos entrenados previamente para Python y R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye:
*  Python de código abierto
*  R de código abierto
*  Plataforma de extensibilidad
*  microsoft-openmpi
*  Bibliotecas Revo* básicas
*  Bibliotecas de aprendizaje automático

```bash
# Install as root or sudo
# Minimum install of R, Python
# No asterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="SLES"></a>

## <a name="install-on-suse"></a>Instalación en SUSE

### <a name="install-mro-on-susesles"></a>Instalación (MRO) en SUSE (SLES)

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Opciones de instalación para Python y R:

*  Instale la compatibilidad de lenguaje según los requisitos (uno o varios lenguajes).
*  En la *instalación completa* se proporcionan todas las características disponibles, incluidos los modelos de aprendizaje automático entrenados previamente.
*  La *instalación mínima* excluye los modelos pero todavía mantiene toda la funcionalidad.

### <a name="example-1----full-installation"></a>Ejemplo 1: instalación completa 

Incluye:
*  Python de código abierto
*  R de código abierto
*  Plataforma de extensibilidad
*  microsoft-openmpi
*  Extensiones para Python y R
*  Bibliotecas de aprendizaje automático
*  Modelos entrenados previamente para Python y R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Ejemplo 2: instalación mínima 

Incluye:
*  Python de código abierto
*  R de código abierto
*  Plataforma de extensibilidad
*  microsoft-openmpi
*  Bibliotecas Revo* básicas
*  Bibliotecas de aprendizaje automático 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>Configuración posterior a la instalación (obligatoria)

La configuración adicional se realiza principalmente a través de la [herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Agregue la cuenta de usuario de mssql usada para ejecutar el servicio SQL Server.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Acepte los contratos de licencia de las extensiones de R y Python de código abierto. Use el comando siguiente:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
3. El programa de instalación detecta los paquetes mssql-mlservices y solicita la aceptación del CLUF (si no se ha aceptado antes) cuando se ejecuta `mssql-conf setup`. Para más información sobre los parámetros EULA, vea [Configuración de SQL Server con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

4. Habilite el acceso de red saliente. El acceso de red saliente está deshabilitado de forma predeterminada. Para habilitar las solicitudes salientes, establezca la propiedad booleana "outboundnetworkaccess" con la herramienta mssql-conf. Para más información, vea [Configuración de SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

5. Solo de cara a la integración de características de R, establezca la variable de entorno **MKL_CBWR** para [garantizar una salida coherente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de los cálculos de la biblioteca Math Kernel Library (MKL) de Intel.

   + Edite o cree un archivo llamado `named.bash_profile` en el directorio principal de usuario, mediante la adición de la línea `export MKL_CBWR="AUTO"` al archivo.

   + Ejecute este archivo escribiendo `source.bash_profile` en un símbolo del sistema de Bash.

6. Reinicie el servicio SQL Server Launchpad y la instancia del motor de base de datos para leer los valores actualizados del archivo INI. Cuando se modifica una configuración relacionada con la extensibilidad, se muestra un mensaje de notificación.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

7. Habilite la ejecución de scripts externos con Azure Data Studio u otra herramienta como SQL Server Management Studio (solo Windows) que ejecute Transact-SQL. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Vuelva a reiniciar el servicio Launchpad.

## <a name="verify-installation"></a>Comprobar la instalación

Las bibliotecas de R (MicrosoftML, RevoScaleR y otras) se encuentran en `/opt/mssql/mlservices/libraries/RServer`.

Las bibliotecas de Python (microsoftml y revoscalepy) se encuentran en `/opt/mssql/mlservices/libraries/PythonServer`.

Para validar la instalación:

- Ejecute un script de T-SQL que ejecute un procedimiento almacenado del sistema que invoque Python o R mediante una herramienta de consulta. 

Para Windows, use lo siguiente: 
*  Azure Data Studio
*  SQL Server Management Studio o PowerShell

Si tiene un equipo Windows con estas herramientas, úselo para conectarse a la instalación de Linux del motor de base de datos.

Ejecute el siguiente comando SQL para probar la ejecución de R en SQL Server. ¿Errores? Pruebe el reinicio del servicio, `sudo systemctl restart mssql-server.service`.

```
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

## <a name="unattended-installation"></a>Instalación desatendida

Mediante la [instalación desatendida](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) del motor de base de datos, agregue los paquetes de mssql-mlservices y los contratos de licencia.

 Use uno de los parámetros de CLUF específicos de mlservices para las distribuciones de R y Python de código abierto:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

El CLUF completo se documenta en [Configuración de SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Instalación sin conexión

Siga las instrucciones de [instalación sin conexión](sql-server-linux-setup.md#offline) para ver los pasos para instalar los paquetes. Descargue paquetes específicos mediante la lista de paquetes siguiente.

> [!Tip]
> Varias de las herramientas de administración de paquetes proporcionan comandos que pueden ayudar a determinar las dependencias de los paquetes. En yum, use `sudo yum deplist [package]`. En Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido de `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Sitio de descarga

Descargue los paquetes desde [https://packages.microsoft.com/](https://packages.microsoft.com/). Todos los paquetes mlservices de Python y R se colocan con el paquete del motor de base de datos. La versión base de los paquetes mlservices es 9.4.6. Recuerde que los paquetes microsoft-r-open están en un [repositorio diferente](#mro).

#### <a name="rhel7-paths"></a>Rutas de acceso de RHEL/7

|||
|--|----|
| Paquetes mssql/mlservices | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| Paquetes microsoft-r-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Rutas de acceso de Ubuntu/16.04

|||
|--|----|
| Paquetes mssql/mlservices | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| Paquetes microsoft-r-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Rutas de acceso de SLES/12

|||
|--|----|
| Paquetes mssql/mlservices | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| Paquetes microsoft-r-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) |

## <a name="package-list"></a>Lista de paquetes

Paquetes de instalación disponibles:

| Nombre del paquete | Válido para | Descripción |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | Marco de extensibilidad que se usa para ejecutar Python y R. |
| microsoft-openmpi  | Python, R | Interfaz de paso de mensajes usada por las bibliotecas Rev* para la paralelización en Linux. |
| mssql-mlservices-python | Python | Distribución de código abierto de Anaconda y Python. |
|mssql-mlservices-mlm-py  | Python | *Instalación completa*. Proporciona revoscalepy, microsoftml, modelos entrenados previamente para las características de imágenes y análisis de opiniones de texto.| 
|mssql-mlservices-packages-py  | Python | *Instalación mínima*. Proporciona revoscalepy y microsoftml. <br/>Excluye los modelos previamente entrenados. | 
| [microsoft-r-open*](#mro) | R | Distribución de código abierto de R, formada por tres paquetes. |
|mssql-mlservices-mlm-r  | R | *Instalación completa*. Proporciona: RevoScaleR, MicrosoftML, sqlRUtils, olapR, modelos entrenados previamente para las características de imágenes y análisis de opiniones de texto.| 
|mssql-mlservices-packages-r  | R | *Instalación mínima*. Proporciona RevoScaleR, sqlRUtils, MicrosoftML, olapr. <br/>Excluye los modelos previamente entrenados. |

Seleccione las extensiones que quiera usar y descargue los paquetes necesarios para un lenguaje específico. Los nombres de archivo incluyen información de la plataforma en el sufijo.

Lista de archivos:

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

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar con algunos ejemplos sencillos y conocer los aspectos básicos del funcionamiento de R con SQL Server. Para conocer el siguiente paso, vea los vínculos siguientes:

+ [Tutorial: Ejecutar R en T-SQL](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server con estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para obtener ejemplos de Machine Learning basados en escenarios del mundo real, vea los [tutoriales sobre Machine Learning](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
