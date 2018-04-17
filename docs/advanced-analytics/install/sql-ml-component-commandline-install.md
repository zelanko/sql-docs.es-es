---
title: Instalación de componentes de aprendizaje de máquina de SQL Server de línea de comandos | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1bc0cda53059b715a04d6e9a350e40d3a265d5e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-machine-learning-components-from-the-command-line"></a>Instalar componentes de aprendizaje de máquina de SQL Server desde la línea de comandos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo proporciona instrucciones para los componentes desde una línea de comandos de aprendizaje automático de SQL Server de instalar:

+ [Instancia de base de datos](#indb)
+ [Agregar a una instancia del motor de base de datos existente](#add-existing)
+ [Instalación silenciosa](#silent)
+ [Servidor independiente](#shared-feature)

Puede especificar la interacción silenciosa, básica o completa con la interfaz de usuario del programa de instalación. En este artículo complementa [instalar SQL Server desde la línea de comandos](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), que abarcan los parámetros únicos a los componentes de aprendizaje de máquina de R y Python.

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

+ Ejecute los comandos desde un símbolo del sistema con privilegios elevados. 

+ Una instancia del motor de base de datos es necesaria para las instalaciones en bases de datos. No se puede instalar sólo las características R o Python, aunque puede [agregarlos de forma incremental a una instancia existente](#add-existing). Si desea simplemente R y Python sin el motor de base de datos, instale el [servidor independiente](#shared-feature).

+ No se instale en un clúster de conmutación por error. El mecanismo de seguridad utilizado para aislar los procesos de R y Python no es compatible con un entorno de clúster de conmutación por error de Windows Server.

+ No se instale en un controlador de dominio. Se producirá un error en la parte de servicios de aprendizaje de máquina del programa de instalación.

+ Evite la instalación independiente y las instancias de base de datos en el mismo equipo. Un servidor independiente competirán por los mismos recursos, lo que puede perjudicar el rendimiento de las instalaciones.


## <a name="command-line-arguments"></a>Argumentos de línea de comandos

El argumento de características se requiere, como son contratos de términos de licencia. 

Al realizar la instalación a través del símbolo del sistema, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el modo totalmente silencioso mediante el uso del parámetro /Q o el modo silencioso sencillo mediante el parámetro /QS. El modificador /QS solamente muestra el progreso, pero no acepta ninguna entrada ni muestra mensajes de error si los encuentra. El parámetro /QS solamente se admite cuando se ha especificado /Action=install.

| Argumentos | Description |
|-----------|-------------|
| / CARACTERÍSTICAS = AdvancedAnalytics | Instala la versión de base de datos: SQL Server 2017 Machine Learning Services (In-Database) o SQL Server 2016 R Services (In-Database).  |
| / CARACTERÍSTICAS = SQL_INST_MR | Se aplica a SQL Server de 2017 únicamente. Asociarla a AdvancedAnalytics. Instala la característica (In-Database) R, incluidos Microsoft R Open y los paquetes de R propietarios. La característica de SQL Server 2016 R Services es R solo, así que no hay ningún parámetro de la versión.|
| / CARACTERÍSTICAS = SQL_INST_MPY | Se aplica a SQL Server de 2017 únicamente. Asociarla a AdvancedAnalytics. Instala la característica de Python (In-Database), incluidos Anaconda y los paquetes de Python propietarios. |
| / CARACTERÍSTICAS = SQL_SHARED_MR | Instala la característica de R para la versión independiente: servidor de aprendizaje de SQL Server de 2017 máquina (independiente) o SQL Server 2016 R Server (independiente). Un servidor independiente es una "característica compartida" no está enlazada a una instancia del motor de base de datos.|
| / CARACTERÍSTICAS = SQL_SHARED_MPY | Se aplica a SQL Server de 2017 únicamente. Instala la característica de Python para la versión independiente: servidor de aprendizaje de SQL Server de 2017 máquina (independiente). Un servidor independiente es una "característica compartida" no está enlazada a una instancia del motor de base de datos.|
| /IACCEPTROPENLICENSETERMS  | Indica que se han aceptado los términos de licencia para el uso de los componentes de R de código abierto. |
| / IACCEPTPYTHONLICENSETERMS | Indica que se han aceptado los términos de licencia para el uso de los componentes de Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que se han aceptado los términos de licencia para utilizar SQL Server.|
| / MRCACHEDIRECTORY | Para el programa de instalación sin conexión, Establece la carpeta que contiene los archivos CAB de componentes de R. |
| / MPYCACHEDIRECTORY | Para el programa de instalación sin conexión, Establece la carpeta que contiene los archivos .cab de componente de Python. |


## <a name="indb"></a> Instalaciones de instancias de base de datos

Análisis de bases de datos están disponibles para las instancias del motor de base de datos, necesarios para agregar la **AdvancedAnalytics** característica a la instalación. Puede instalar una instancia del motor de base de datos con análisis avanzados, o [agregarlo a una instancia existente](#add-existing). 

Para ver información de progreso sin interactivo en pantalla mensajes, use el argumento/QS.

> [!Important]
> Después de la instalación, siguen siendo dos pasos de configuración adicionales. Integración no está completa hasta que se llevan a cabo estas tareas. Vea [tareas de postinstalación](#post-install) para obtener instrucciones.

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server de 2017: motor de base de datos, advanced analytics con Python y R

Para una instalación simultánea de la instancia del motor de base de datos, proporcione el nombre de instancia y un inicio de sesión de administrador (Windows). Incluye características para la instalación de núcleo y los componentes del lenguaje, así como la aceptación de todos los términos de licencia.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este mismo comando, pero con un inicio de sesión de SQL Server en un motor de base de datos mediante la autenticación mixta.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

En este ejemplo es Python, que muestra que puede agregar un idioma mediante la omisión de una característica.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: motor de base de datos y análisis avanzados con R

Este comando es idéntico para SQL Server 2017, pero sin los elementos de Python, que no están disponibles en el programa de instalación de SQL Server 2016.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> Configuración posterior a la instalación (obligatorio)

Se aplica a las instalaciones solo en bases de datos.

Cuando finaliza el programa de instalación, tiene una instancia del motor de base de datos con paquetes de R y Python, Microsoft R y Python, Microsoft R Open, Anaconda, herramientas, ejemplos y scripts que forman parte de la distribución. 

Más de dos tareas son necesarias para completar la instalación:

1. Reinicie el servicio de motor de base de datos.

1. Habilitar los scripts externos para poder usar la característica. Siga las instrucciones de [instalar SQL Server de 2017 Machine Learning Services (In-Database)](sql-machine-learning-services-windows-install.md) como el siguiente paso. 

Para SQL Server 2016, use este artículo en su lugar [instalar SQL Server 2016 R Services (In-Database)](sql-r-services-windows-install.md).

## <a name="add-existing"></a> Agregar análisis avanzado a una instancia del motor de base de datos existente

Al agregar análisis avanzados en bases de datos a una instancia del motor de base de datos existente, proporcione el nombre de instancia. Por ejemplo, si instaló anteriormente un motor de base de datos de SQL Server 2017 y Python, podría utilizar este comando para agregar R.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> Instalación silenciosa

Una instalación silenciosa suprime la comprobación para las ubicaciones de archivos .cab. Por este motivo, debe especificar la ubicación donde se puede desempaquetar archivos .cab. Puede que el directorio temporal para este.
 
```  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% /MPYCACHEDIRECTORY=%temp%
```

## <a name="shared-feature"></a> Instalaciones de servidor independiente

Un servidor independiente es una "característica compartida" no está enlazada a una instancia del motor de base de datos. Los ejemplos siguientes muestran las sintaxis válidas para ambas versiones.

SQL Server 2017 admite Python y R en un servidor independiente:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 es solo para R:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Cuando finaliza el programa de instalación, tiene un servidor, los paquetes de Microsoft, distribuciones de código abierto de R y Python, herramientas, ejemplos y scripts que forman parte de la distribución. 

Para abrir una ventana de la consola de R, vaya a \Program Server\140 SQL (o 130) \R_SERVER\bin\x64 y haga doble clic en **RGui.exe**. ¿No está familiarizado con R? Pruebe este tutorial: [comandos de R básicos y funciones de RevoScaleR: 25 ejemplos comunes](https://docs.microsoft.com/en-us/machine-learning-server/r/tutorial-r-to-revoscaler).

Para abrir un comando de Python, vaya a \Program Server\140\PYTHON_SERVER\bin\x64 de SQL y haga doble clic en **python.exe**.

## <a name="get-help"></a>Obtener ayuda

¿Necesita ayuda con la instalación o actualización? Para obtener respuestas a preguntas comunes y los problemas conocidos, vea el artículo siguiente:

* [Actualización e instalación preguntas más frecuentes: servicios de aprendizaje de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para comprobar el estado de instalación de la instancia y solucionar problemas comunes, pruebe estos informes personalizados.

* [Informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en situaciones del mundo real, vea [máquina tutoriales de aprendizaje](../tutorials/machine-learning-services-tutorials.md).