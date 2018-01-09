---
title: "En bases de datos análisis de Python para desarrolladores de SQL | Documentos de Microsoft"
ms.custom: 
ms.date: 10/13/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 970298c59b7b48c5579125ef163785801db676ee
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="in-database-python-analytics-for-sql-developers"></a>Análisis de Python en bases de datos para desarrolladores de SQL

El objetivo de este tutorial es proporcionar a los programadores SQL con experiencia práctica para crear una solución con Python que se ejecuta en SQL Server de aprendizaje automático. En este tutorial, aprenderá a agregar código Python a procedimientos almacenados y ejecutar procedimientos almacenados para generar y predicción de modelos.

> [!NOTE]
> ¿Prefiere R? Vea [este tutorial](sqldev-in-database-r-for-sql-developers.md), que proporciona una solución similar pero usa R y se puede ejecutar en SQL Server 2016 o 2017 de SQL Server.

## <a name="overview"></a>Información general

El proceso de creación de una solución de aprendizaje automático es una compleja que puede incluir varias herramientas y la coordinación de expertos en la materia en varias fases:

+ obtener y limpieza de datos
+ explorar los datos y generar características útiles para el modelado
+ entrenamiento y para la optimización del modelo
+ implementación en producción

**El objetivo de este tutorial está en la creación e implementación de una solución mediante SQL Server.**

Los datos están en el conjunto de datos de Nueva York Taxi conocido. Para realizar este tutorial rápido y sencillo, el muestreo de los datos. Se creará un modelo de clasificación binaria que predice si un viaje determinado es probable que obtenga una sugerencia o no, en función de las columnas como la hora del día, la distancia y la ubicación de recogida.

Todas las tareas pueden realizarse mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados en el entorno conocido de[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

- [Paso 1: Descargar los datos de ejemplo](sqldev-py1-download-the-sample-data.md)

    Descargue el conjunto de datos de ejemplo y todos los archivos de script en un equipo local.

- [Paso 2: Importar datos a SQL Server mediante PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

    Ejecutar un script de PowerShell que crea una base de datos y una tabla en la instancia especificada y carga los datos de ejemplo a la tabla.

- [Paso 3: Explorar y visualizar los datos que se usa Python](sqldev-py3-explore-and-visualize-the-data.md)

    Realizar la exploración de datos básicos y visualización, por Python que realiza la llamada de [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados.

- [Paso 4: Crear características de datos mediante Python en T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Cree nuevas características de datos mediante funciones personalizadas de SQL.
  
- [Paso 5: Entrenar y guardar un modelo de Python mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Crear y guardar el modelo de aprendizaje automático, que se usa Python en procedimientos almacenados.
  
    En este tutorial se muestra cómo realizar una tarea de clasificación binaria; También puede usar los datos para crear modelos de regresión o clasificación multiclase.

  
-  [Paso 6: Poner el modelo de Python](sqldev-py6-operationalize-the-model.md)

    Después de que el modelo se ha guardado en la base de datos, llame al modelo de predicción utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="requirements"></a>Requisitos

### <a name="prerequisites"></a>Prerequisites

+ Instale una instancia de SQL Server 2017 con servicios de aprendizaje de máquina y Python habilitado. Para obtener más información, consulte [configurar servicios de aprendizaje de máquina de SQL Server con Python](../python/setup-python-machine-learning-services.md).
+ El inicio de sesión que use para este tutorial debe tener permisos para crear bases de datos y otros objetos, cargar datos, seleccionar datos y ejecutar procedimientos almacenados.

### <a name="experience-level"></a>Nivel de experiencia

Debe estar familiarizado con las operaciones fundamentales de la base de datos, como la creación de tablas y bases de datos, importar datos en tablas y crear consultas SQL.

Un programador experimentado de SQL debe ser capaz de completar este tutorial con [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante la ejecución de los scripts de PowerShell proporcionados.

Python: Conocimientos básicos es útil, pero no es obligatorio. Se proporciona todo el código Python.

Es útil conocer algo de PowerShell.

### <a name="tools"></a>Herramientas

Para este tutorial, estamos suponiendo que ha llegado a la fase de implementación. Se han proporcionado limpiar datos, complete el código de T-SQL de característica de ingeniería y el trabajo de código Python. Por lo tanto, puede completar este tutorial utilizando SQL Server Management Studio o cualquier otra herramienta que admite la ejecución de instrucciones SQL.

+ [Información general sobre las herramientas de SQL Server](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

Si desea desarrollar y probar su propio código Python o depurar una solución de Python, se recomienda usar un entorno de desarrollo dedicados:

+ **Visual Studio de 2017** admite ambos R y [Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/). Se recomienda la [cargas de trabajo de ciencia de datos](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/), que también es compatible con R y F #.
+ Si tiene una versión anterior de Visual Studio, [extensiones de Python para Visual Studio](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio) facilita el proceso administrar varios entornos de Python.
+ PyCharm es un IDE popular entre los desarrolladores de Python.

    > [!NOTE]
    > En general, evite escribir o probar el nuevo código de Python en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si el código que incrusta en un procedimiento almacenado tiene algún problema, la información que se devuelve desde el procedimiento almacenado es normalmente inadecuada entender la causa del error.

Use los siguientes recursos para ayudarle a planear y ejecutar un proyecto de aprendizaje de automático correcta:

+ [Proceso de ciencia de datos de equipo](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>Tiempo estimado necesario

|Paso| Tiempo (horas)|
|----|----|
|Descargar los datos de ejemplo| 0:15|
|Importar datos a SQL Server usando PowerShell|0:15|
|Explorar y visualizar los datos|0:20|
|Crear características de datos mediante T-SQL|0:30|
|Entrenar y guardar un modelo mediante T-SQL|0:15|
|Poner el modelo|0:40|

## <a name="get-started"></a>Introducción

  [Paso 1: Descargar los datos de ejemplo](sqldev-py1-download-the-sample-data.md)
