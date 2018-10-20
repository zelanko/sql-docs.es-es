---
title: En bases de datos análisis de Python para desarrolladores de SQL | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 250d2efd6d212348083f5dc3bbc355c466f4811b
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461861"
---
# <a name="in-database-python-analytics-for-sql-developers"></a>Análisis de Python en bases de datos para desarrolladores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El objetivo de este tutorial es proporcionar a los programadores de SQL experiencia práctica para crear una solución con Python que se ejecuta en SQL Server de aprendizaje automático. En este tutorial, obtendrá información sobre cómo agregar código de Python a los procedimientos almacenados y ejecutar procedimientos almacenados para generar y predecir a partir de modelos.

> [!NOTE]
> ¿Prefiere R? Consulte [este tutorial](sqldev-in-database-r-for-sql-developers.md), que proporciona una solución similar, pero usa R y se pueden ejecutar en SQL Server 2016 o SQL Server 2017.

## <a name="overview"></a>Información general

El proceso de creación de una solución de aprendizaje automático es una compleja que puede implicar varias herramientas y la coordinación de expertos a través de varias fases:

+ obtención y limpieza de datos
+ explorar los datos y generar características útiles para el modelado
+ entrenamiento y el modelo de optimización
+ implementación en producción

**El objetivo de este tutorial se encuentra en la creación e implementación de una solución con SQL Server.**

Los datos están en el conocido conjunto de datos de taxis de Nueva York. Para realizar este tutorial rápido y sencillo, se muestrean los datos. Creará un modelo de clasificación binaria que predice si un viaje concreto es probable que reciba una propina o no, en función de las columnas como la hora del día, la distancia y la ubicación de recogida.

Todas las tareas que pueden hacerse mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados en el entorno familiar de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

- [Paso 1: Descargar los datos de ejemplo](demo-data-nyctaxi-in-sql.md)

    Descargue el conjunto de datos de ejemplo y todos los archivos de script en un equipo local.

- [Paso 2: Importar datos a SQL Server mediante PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

    Ejecutar un script de PowerShell que crea una base de datos y una tabla en la instancia especificada y carga los datos de ejemplo a la tabla.

- [Paso 3: Explorar y visualizar datos mediante Python](sqldev-py3-explore-and-visualize-the-data.md)

    Realizar la exploración de datos básicos y la visualización, que realiza la llamada de Python desde [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados.

- [Paso 4: Crear características de datos mediante Python en T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Cree nuevas características de datos mediante funciones personalizadas de SQL.
  
- [Paso 5: Entrenar y guardar un modelo de Python mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Generar y guardar el modelo de aprendizaje automático, uso de Python en procedimientos almacenados.
  
    Este tutorial muestra cómo realizar una tarea de clasificación binaria. También puede usar los datos para crear modelos de regresión o clasificación multiclase.

  
-  [Paso 6: Hacer operativo el modelo de Python](sqldev-py6-operationalize-the-model.md)

    Después de que el modelo se ha guardado en la base de datos, llamar al modelo de predicción utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="requirements"></a>Requisitos

### <a name="prerequisites"></a>Requisitos previos

+ Instale una instancia de SQL Server 2017 con Machine Learning Services y Python habilitado. Para obtener más información, consulte [instalar SQL Server 2017 Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md).
+ El inicio de sesión que use para este tutorial debe tener permisos para crear bases de datos y otros objetos, cargar datos, seleccionar datos y ejecutar procedimientos almacenados.

### <a name="experience-level"></a>Nivel de experiencia

Debe estar familiarizado con operaciones de base de datos fundamentales, como crear bases de datos y tablas, importar datos en tablas y crear consultas SQL.

Un programador experimentado de SQL debe ser capaz de completar este tutorial con [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante la ejecución de los scripts de PowerShell proporcionados.

Python: Conocimientos básicos es útil, pero no es necesario. Se proporciona todo el código Python.

Es útil conocer algo de PowerShell.

### <a name="tools"></a>Herramientas

Para este tutorial, estamos suponiendo que ha alcanzado la fase de implementación. Se han concedido limpiar datos, completar código T-SQL para la característica de ingeniería y el trabajo de código de Python. Por lo tanto, puede completar este tutorial con SQL Server Management Studio o cualquier otra herramienta que admite la ejecución de instrucciones SQL.

+ [Información general de las herramientas de SQL Server](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

Si desea desarrollar y probar su propio código Python o depurar una solución de Python, se recomienda usar un entorno de desarrollo dedicado:

+ **Visual Studio 2017** admite ambos R y [Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/). Se recomienda la [carga de trabajo de ciencia de datos](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/), que también es compatible con R y F #.
+ Si tiene una versión anterior de Visual Studio, [extensiones de Python para Visual Studio](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio) facilita la administración de varios entornos de Python.
+ PyCharm es un IDE popular entre los desarrolladores de Python.

    > [!NOTE]
    > En general, evite escribir o probar el nuevo código de Python en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si el código que se incrusta en un procedimiento almacenado tiene algún problema, la información que se devuelve desde el procedimiento almacenado es no suele ser adecuada para entender la causa del error.

Use los siguientes recursos para ayudarle a planear y ejecutar un proyecto de aprendizaje de automático correcta:

+ [Proceso de ciencia de datos](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>Tiempo estimado necesario

|Paso| Tiempo (horas)|
|----|----|
|Descargar los datos de ejemplo| 0:15|
|Importar datos a SQL Server mediante PowerShell|0:15|
|Explorar y visualizar los datos|0:20|
|Crear características de datos mediante T-SQL|0:30|
|Entrenar y guardar un modelo con T-SQL|0:15|
|Hacer operativo el modelo|0:40|

## <a name="get-started"></a>Introducción

  [Paso 1: Descargar los datos de ejemplo](demo-data-nyctaxi-in-sql.md)
