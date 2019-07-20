---
title: Tutorial de análisis de Python en base de datos para desarrolladores de SQL
description: Obtenga información sobre cómo insertar código de Python en SQL Server procedimientos almacenados y funciones de T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: ed8008bbda76bfc8a194897e9389c9d5dc6bb031
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345936"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>Tutorial: Análisis de datos de Python para desarrolladores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial para programadores de SQL, obtenga información sobre la integración de Python mediante la creación e implementación de una solución de aprendizaje automático basada en Python mediante una base de datos de [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) en SQL Server. Usará T-SQL, SQL Server Management Studio y una instancia del motor de base de datos con compatibilidad con el lenguaje [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y Python.

En este tutorial se presentan las funciones de Python usadas en un flujo de trabajo de modelado de datos. Los pasos incluyen la exploración de datos, la compilación y el entrenamiento de un modelo de clasificación binaria y la implementación de modelos. Usará datos de ejemplo de la Comisión de taxis de Nueva York y LIMOSINE, y el modelo que se va a crear predice si es probable que un viaje dé como resultado una propina basada en la hora del día, la distancia recorrida y la ubicación de la recogida. 

Todo el código de Python que se usa en este tutorial está incluido en procedimientos almacenados que se crean y ejecutan en Management Studio.

> [!NOTE]
> Este tutorial está disponible en R y Python. Para la versión de R, consulte [análisis de base de datos para desarrolladores de r](sqldev-in-database-r-for-sql-developers.md).

## <a name="overview"></a>Información general

El proceso de creación de una solución de aprendizaje automático es una compleja que puede implicar varias herramientas y la coordinación de expertos en la materia en varias fases:

+ obtención y limpieza de datos
+ exploración de los datos y creación de características útiles para el modelado
+ entrenamiento y ajuste del modelo
+ implementación en producción

El desarrollo y las pruebas del código real se realizan mejor con un entorno de desarrollo dedicado. Sin embargo, una vez que el script se ha probado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] completo, puede implementarlo fácilmente con procedimientos almacenados en el [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]entorno conocido de. El encapsulado de código externo en procedimientos almacenados es el mecanismo principal para la puesta en operación del código en SQL Server.

Si es un programador de SQL nuevo en Python o un desarrollador de Python nuevo en SQL, este tutorial de varias partes presenta un flujo de trabajo típico para realizar análisis en base de datos con Python y SQL Server. 

+ [Lección 1: Explore y visualice los datos mediante Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [Lección 2: Crear características de datos mediante funciones SQL personalizadas](sqldev-py4-create-data-features-using-t-sql.md)

+ [Lección 3: Entrenar y guardar un modelo de Python mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [Lección 4: Predecir posibles resultados mediante un modelo de Python en un procedimiento almacenado](sqldev-py6-operationalize-the-model.md)

Una vez guardado el modelo en la base de datos, puede llamar al modelo para las predicciones [!INCLUDE[tsql](../../includes/tsql-md.md)] desde mediante procedimientos almacenados.

## <a name="prerequisites"></a>Requisitos previos

+ [SQL Server 2017 Machine Learning Services con Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Permisos](../security/user-permission.md)

+ [Base de datos de demostración de taxi de Nueva York](demo-data-nyctaxi-in-sql.md)

Todas las tareas se pueden realizar [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]en.

En este tutorial se supone que está familiarizado con las operaciones básicas de base de datos, como la creación de bases de datos y tablas, la importación de datos y la escritura de consultas SQL. No supone que conoce Python. Como tal, se proporciona todo el código de Python. 

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Explore y visualice los datos mediante Python](sqldev-py3-explore-and-visualize-the-data.md)
