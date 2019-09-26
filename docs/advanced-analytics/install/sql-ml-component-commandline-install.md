---
title: Instalación del símbolo del sistema de los componentes de R y Python
description: Ejecute SQL Server instalación de la línea de comandos para agregar el lenguaje R y la integración de Python a una instancia del motor de base de datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f60aa3684778a7347b1ffd613a924c3bf0b7b94a
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271945"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>Instalar SQL Server componentes de R y Python de machine learning desde la línea de comandos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se proporcionan instrucciones para instalar SQL Server componentes de machine learning desde una línea de comandos:

+ [Nueva instancia de en la base de datos](#indb)
+ [Agregar a una instancia existente del motor de base de datos](#add-existing)
+ [Instalación silenciosa](#silent)
+ [Nuevo servidor independiente](#shared-feature)

Puede especificar la interacción silenciosa, básica o completa con la interfaz de usuario del programa de instalación. En este artículo se complementa la [instalación de SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), que abarca los parámetros exclusivos de los componentes de aprendizaje automático de R y Python.

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

+ Ejecutar comandos desde un símbolo del sistema con privilegios elevados. 

+ Se requiere una instancia del motor de base de datos para las instalaciones en la base de datos. No se pueden instalar solo las características de R o Python, aunque se pueden [Agregar incrementalmente a una instancia existente](#add-existing). Si solo quiere R y Python sin el motor de base de datos, instale el [servidor independiente](#shared-feature).

+ No instale en un clúster de conmutación por error. El mecanismo de seguridad que se usa para aislar los procesos de R y Python no es compatible con un entorno de clústeres de conmutación por error de Windows Server.

+ No instale en un controlador de dominio. Se producirá un error en la parte Machine Learning Services del programa de instalación.

+ Evite instalar instancias independientes y en la base de datos en el mismo equipo. Un servidor independiente competirá por los mismos recursos, con lo que se descargará el rendimiento de ambas instalaciones.


## <a name="command-line-arguments"></a>Argumentos de la línea de comandos

El argumento Features es obligatorio, al igual que los contratos de términos de licencia. 

Al realizar la instalación a través del símbolo del sistema, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el modo totalmente silencioso mediante el uso del parámetro /Q o el modo silencioso sencillo mediante el parámetro /QS. El modificador /QS solamente muestra el progreso, pero no acepta ninguna entrada ni muestra mensajes de error si los encuentra. El parámetro /QS solamente se admite cuando se ha especificado /Action=install.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
| Argumentos | Descripción |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Instala la versión en la base de datos: SQL Server R Services (in-Database).  |
| /FEATURES = SQL_SHARED_MR | Instala la característica de R para la versión independiente: SQL Server R Server (independiente). Un servidor independiente es una "característica compartida" que no está enlazada a una instancia del motor de base de datos.|
| /IACCEPTROPENLICENSETERMS  | Indica que ha aceptado los términos de licencia para usar los componentes de R de código abierto. |
| /IACCEPTPYTHONLICENSETERMS | Indica que ha aceptado los términos de licencia para usar los componentes de Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que ha aceptado los términos de licencia para usar SQL Server.|
| /MRCACHEDIRECTORY | Para la instalación sin conexión, establece la carpeta que contiene los archivos CAB del componente de R. |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
| Argumentos | Descripción |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Instala la versión en la base de datos: SQL Server Machine Learning Services (in-Database).  |
| /FEATURES = SQL_INST_MR | Empareje este con AdvancedAnalytics. Instala la característica de R (en la base de datos), incluidos los paquetes de Microsoft R Open y de su propiedad. |
| /FEATURES = SQL_INST_MPY | Empareje este con AdvancedAnalytics. Instala la característica de Python (en la base de datos), incluidos los paquetes de Python de Anaconda y de propiedad. |
| /FEATURES = SQL_SHARED_MR | Instala la característica de R para la versión independiente: SQL Server Machine Learning Server (independiente). Un servidor independiente es una "característica compartida" que no está enlazada a una instancia del motor de base de datos.|
| /FEATURES = SQL_SHARED_MPY | Instala la característica de Python para la versión independiente: SQL Server Machine Learning Server (independiente). Un servidor independiente es una "característica compartida" que no está enlazada a una instancia del motor de base de datos.|
| /IACCEPTROPENLICENSETERMS  | Indica que ha aceptado los términos de licencia para usar los componentes de R de código abierto. |
| /IACCEPTPYTHONLICENSETERMS | Indica que ha aceptado los términos de licencia para usar los componentes de Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que ha aceptado los términos de licencia para usar SQL Server.|
| /MRCACHEDIRECTORY | Para la instalación sin conexión, establece la carpeta que contiene los archivos CAB del componente de R. |
| /MPYCACHEDIRECTORY | Reservado para uso futuro. Use% TEMP% para almacenar los archivos CAB de componentes de Python para su instalación en equipos que no tienen una conexión a Internet. |
::: moniker-end

## <a name="indb"></a>Instalaciones de instancias en la base de datos

El análisis en base de datos está disponible para las instancias del motor de base de datos, necesario para agregar la característica **AdvancedAnalytics** a la instalación. Puede instalar una instancia del motor de base de datos con análisis avanzado o [agregarla a una instancia existente](#add-existing). 

Para ver la información de progreso sin las solicitudes interactivas en pantalla, use el argumento/QS.

> [!IMPORTANT]
> Después de la instalación, quedan dos pasos de configuración adicionales. La integración no se completa hasta que se realicen estas tareas. Consulte [las tareas posteriores a la instalación](#post-install) para obtener instrucciones.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
### <a name="sql-server-machine-learning-services-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server Machine Learning Services: motor de base de datos, análisis avanzado con Python y R

Para una instalación simultánea de la instancia del motor de base de datos, proporcione el nombre de instancia y un inicio de sesión de administrador (Windows). Incluye características para la instalación de componentes principales y de idioma, así como la aceptación de todos los términos de licencia.

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este mismo comando, pero con un inicio de sesión SQL Server en un motor de base de datos mediante la autenticación mixta.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este ejemplo es solo Python, que muestra que puede Agregar un idioma omitiendo una característica.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
### <a name="sql-server-r-services-database-engine-and-advanced-analytics-with-r"></a>SQL Server R Services: motor de base de datos y análisis avanzado con R

Para una instalación simultánea de la instancia del motor de base de datos, proporcione el nombre de instancia y un inicio de sesión de administrador (Windows). Incluye características para la instalación de componentes principales y de idioma, así como la aceptación de todos los términos de licencia.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```
::: moniker-end

## <a name="post-install"></a>Configuración posterior a la instalación (obligatorio)

Solo se aplica a las instalaciones en la base de datos.

Una vez finalizada la instalación, tiene una instancia del motor de base de datos con R y Python, los paquetes de Microsoft R y Python, Microsoft R Open, Anaconda, Tools, samples y scripts que forman parte de la distribución. 

Se requieren dos tareas más para completar la instalación:


::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. Reinicie el servicio motor de base de datos.

1. SQL Server Machine Learning Services: Habilite los scripts externos antes de poder usar la característica. Siga las instrucciones de [Install SQL Server Machine Learning Services (in-Database)](sql-machine-learning-services-windows-install.md) como paso siguiente. 
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. Reinicie el servicio motor de base de datos.

1. SQL Server R Services: Habilite los scripts externos antes de poder usar la característica. Siga las instrucciones de [instalar SQL Server R Services (en base de datos)](sql-r-services-windows-install.md) como paso siguiente. 
::: moniker-end

## <a name="add-existing"></a>Agregar análisis avanzado a una instancia existente del motor de base de datos

Cuando agregue análisis avanzado en base de datos a una instancia existente del motor de base de datos, proporcione el nombre de la instancia. Por ejemplo, si instaló anteriormente un motor de base de datos de SQL Server 2017 y Python, podría usar este comando para agregar R.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```

## <a name="silent"></a>Instalación silenciosa

Una instalación silenciosa suprime la comprobación de las ubicaciones de los archivos. cab. Por esta razón, debe especificar la ubicación donde se van a desempaquetar los archivos. cab. En el caso de Python, los archivos. CAB deben encontrarse en% TEMP *. Para R, puede establecer la ruta de acceso de la carpeta con el directorio temporal para este.
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a>Instalaciones de servidor independiente

Un servidor independiente es una "característica compartida" que no está enlazada a una instancia del motor de base de datos. En los siguientes ejemplos se muestra la sintaxis válida para la instalación del servidor independiente.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server Machine Learning Server admite Python y R en un servidor independiente:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server R Server es solo R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end

Una vez finalizada la instalación, tiene un servidor, paquetes de Microsoft, distribuciones de código abierto de R y Python, herramientas, muestras y scripts que forman parte de la distribución. 

Para abrir una ventana de la consola de R `\Program files\Microsoft SQL Server\150 (or 140/130)\R_SERVER\bin\x64` , vaya a y haga doble clic en **RGui. exe**. ¿No está familiarizado con R? Pruebe este tutorial: [Funciones de R y comandos de RevoScaleR básicos: 25 ejemplos](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)comunes.

Para abrir un comando de Python, vaya `\Program files\Microsoft SQL Server\150 (or 140)\PYTHON_SERVER\bin\x64` a y haga doble clic en **Python. exe**.

## <a name="get-help"></a>Obtener ayuda

¿Necesita ayuda con la instalación o la actualización? Para obtener respuestas a preguntas comunes y problemas conocidos, vea el siguiente artículo:

* [Preguntas más frecuentes sobre actualización e instalación: Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para comprobar el estado de la instalación de la instancia y corregir los problemas comunes, pruebe estos informes personalizados.

* [Informes personalizados para SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar con algunos ejemplos sencillos y conocer los aspectos básicos del funcionamiento de R con SQL Server. Para conocer el siguiente paso, vea los vínculos siguientes:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server con estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para obtener ejemplos de Machine Learning basados en escenarios del mundo real, vea los [tutoriales sobre Machine Learning](../tutorials/machine-learning-services-tutorials.md).