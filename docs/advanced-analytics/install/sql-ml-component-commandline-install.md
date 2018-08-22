---
title: Línea de comandos de instalación de componentes de R y Python de aprendizaje de automático de SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 77b68c6206e069a29821549998714a671239ca56
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2018
ms.locfileid: "40434875"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>Instalar componentes de R y Python desde la línea de comandos de aprendizaje de automático de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se proporciona instrucciones para los componentes de una línea de comandos de aprendizaje automático de SQL Server de instalar:

+ [Instancia nueva de base de datos](#indb)
+ [Agregar a una instancia del motor de base de datos existente](#add-existing)
+ [Instalación silenciosa](#silent)
+ [Nuevo servidor independiente](#shared-feature)

Puede especificar la interacción silenciosa, básica o completa con la interfaz de usuario del programa de instalación. En este artículo complementa [instalar SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), que abarcan los parámetros únicos para los componentes de aprendizaje automático R y Python.

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

+ Ejecute los comandos desde un símbolo del sistema con privilegios elevados. 

+ Una instancia del motor de base de datos es necesaria para las instalaciones de base de datos. No se puede instalar solo las características de R o Python, aunque puede [agregarlos de forma incremental a una instancia existente](#add-existing). Si desea simplemente R y Python sin el motor de base de datos, instale el [servidor independiente](#shared-feature).

+ No se instale en un clúster de conmutación por error. El mecanismo de seguridad que se usa para aislar los procesos de R y Python no es compatible con un entorno de clúster de conmutación por error de Windows Server.

+ No instale un controlador de dominio. Se producirá un error en la parte de Machine Learning Services del programa de instalación.

+ Evite la instalación independiente y las instancias de base de datos en el mismo equipo. Un servidor independiente competirán por los mismos recursos, lo cual puede perjudicar el rendimiento de ambas instalaciones.


## <a name="command-line-arguments"></a>Argumentos de línea de comandos

El argumento de características es necesario, como son contratos de términos de licencia. 

Al realizar la instalación a través del símbolo del sistema, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el modo totalmente silencioso mediante el uso del parámetro /Q o el modo silencioso sencillo mediante el parámetro /QS. El modificador /QS solamente muestra el progreso, pero no acepta ninguna entrada ni muestra mensajes de error si los encuentra. El parámetro /QS solamente se admite cuando se ha especificado /Action=install.

| Argumentos | Descripción |
|-----------|-------------|
| /Features = AdvancedAnalytics | Instala la versión de base de datos: SQL Server 2017 Machine Learning Services (In-Database) o SQL Server 2016 R Services (In-Database).  |
| /FEATURES = SQL_INST_MR | Se aplica a SQL Server 2017 únicamente. Asócielo a AdvancedAnalytics. Instala la característica (en bases de datos) R, incluidos Microsoft R Open y los paquetes de R propietarios. La característica de SQL Server 2016 R Services está R solo, por lo que no hay ningún parámetro para esa versión.|
| /FEATURES = SQL_INST_MPY | Se aplica a SQL Server 2017 únicamente. Asócielo a AdvancedAnalytics. Instala la característica de Python (In-Database), incluida Anaconda y paquetes Python propiedad. |
| /FEATURES = SQL_SHARED_MR | Instala la característica de R para la versión independiente: Machine Learning Server (independiente) de SQL Server 2017 o SQL Server 2016 R Server (independiente). Un servidor independiente es una "característica" no está enlazada a una instancia del motor de base de datos.|
| /FEATURES = SQL_SHARED_MPY | Se aplica a SQL Server 2017 únicamente. Instala la característica de Python para la versión independiente: Machine Learning Server (independiente) de SQL Server 2017. Un servidor independiente es una "característica" no está enlazada a una instancia del motor de base de datos.|
| /IACCEPTROPENLICENSETERMS  | Indica que ha aceptado los términos de licencia para usar los componentes de R de código abierto. |
| /IACCEPTPYTHONLICENSETERMS | Indica que ha aceptado los términos de licencia para usar los componentes de Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que ha aceptado los términos de licencia para el uso de SQL Server.|
| /MRCACHEDIRECTORY | Para la instalación sin conexión, Establece la carpeta que contiene los archivos CAB de componentes de R. |
| / MPYCACHEDIRECTORY | Para la instalación sin conexión, Establece la carpeta que contiene los archivos CAB de componentes de Python. |


## <a name="indb"></a> Instalaciones de instancias de base de datos

Análisis en bases de datos están disponibles para las instancias de motor de base de datos, necesarias para agregar la **AdvancedAnalytics** característica a la instalación. Puede instalar una instancia del motor de base de datos con análisis avanzado, o [agregarlo a una instancia existente](#add-existing). 

Para ver información de progreso sin interactivo pantalla indicaciones, use el argumento/QS.

> [!IMPORTANT]
> Después de la instalación, siguen siendo dos pasos de configuración adicionales. Integración no está completa hasta que se llevan a cabo estas tareas. Consulte [tareas posteriores a la instalación](#post-install) para obtener instrucciones.

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017: motor de base de datos, analítica avanzada con Python y R

Para una instalación simultánea de la instancia del motor de base de datos, proporcione el nombre de instancia y un inicio de sesión de administrador (Windows). Incluye características para instalar core y los componentes del lenguaje, así como la aceptación de todos los términos de licencias.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este el mismo comando, pero con un inicio de sesión de SQL Server en un motor de base de datos mediante la autenticación mixta.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

En este ejemplo es Python, que muestra que puede agregar un idioma si se omite una característica.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: el motor de base de datos y análisis avanzado con R

Este comando es idéntico a SQL Server 2017, pero sin los elementos de Python, que no están disponibles en el programa de instalación de SQL Server 2016.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> Configuración posterior a la instalación (obligatorio)

Se aplica a las instalaciones solo en bases de datos.

Cuando finalice la instalación, tiene una instancia del motor de base de datos con los paquetes de R y Python, Microsoft R y Python, Microsoft R Open, Anaconda, herramientas, ejemplos y scripts que forman parte de la distribución. 

Para completar la instalación, se requieren más de dos tareas:

1. Reinicie el servicio de motor de base de datos.

1. Habilitar los scripts externos para poder usar la característica. Siga las instrucciones de [instalar SQL Server 2017 Machine Learning Services (In-Database)](sql-machine-learning-services-windows-install.md) en el paso siguiente. 

Para SQL Server 2016, use este artículo en su lugar [instalar SQL Server 2016 R Services (In-Database)](sql-r-services-windows-install.md).

## <a name="add-existing"></a> Agregar análisis avanzado a una instancia del motor de base de datos existente

Al agregar análisis avanzado en base de datos a una instancia del motor de base de datos existente, proporcione el nombre de instancia. Por ejemplo, si instaló anteriormente un motor de base de datos de SQL Server 2017 y Python, podría utilizar este comando para agregar R.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> Instalación silenciosa

Una instalación silenciosa suprime la comprobación de ubicaciones de archivos .cab. Por este motivo, debe especificar la ubicación donde se puede desempaquetar los archivos .cab. Puede el directorio temporal para este.
 
```  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% /MPYCACHEDIRECTORY=%temp%
```

## <a name="shared-feature"></a> Instalaciones de servidor independiente

Un servidor independiente es una "característica" no está enlazada a una instancia del motor de base de datos. Los ejemplos siguientes muestran las sintaxis válidas para ambas versiones.

SQL Server 2017 es compatible con Python y R en un servidor independiente:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 es sólo R:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Cuando finalice la instalación, tiene un servidor, los paquetes de Microsoft, distribuciones de código abierto de R y Python, herramientas, ejemplos y scripts que forman parte de la distribución. 

Para abrir una ventana de consola de R, vaya a \Program files\Microsoft SQL Server\140 (o 130) \R_SERVER\bin\x64 y haga doble clic en **RGui.exe**. ¿No está familiarizado con R? Pruebe este tutorial: [comandos de R básicas y las funciones de RevoScaleR: 25 ejemplos comunes](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler).

Para abrir un comando de Python, vaya a \Program files\Microsoft Server\140\PYTHON_SERVER\bin\x64 SQL y haga doble clic en **python.exe**.

## <a name="get-help"></a>Obtener ayuda

¿Necesita ayuda con la instalación o actualización? Para obtener respuestas a preguntas comunes y problemas conocidos, consulte el artículo siguiente:

* [Actualización e instalación preguntas más frecuentes - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para comprobar el estado de instalación de la instancia y solucionar problemas habituales, pruebe estos informes personalizados.

* [Informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecución de R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecución de Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis de en bases de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en escenarios del mundo real, consulte [tutoriales de aprendizaje automático](../tutorials/machine-learning-services-tutorials.md).