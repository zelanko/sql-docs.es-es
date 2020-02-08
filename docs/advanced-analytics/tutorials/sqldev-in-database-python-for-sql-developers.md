---
title: 'Python + T-SQL: Desarrollo del modelo'
description: Conozca cómo insertar código de Python en procedimientos almacenados de SQL Server y en funciones de T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3bafc3a524ec854dc9bf1669660827d5a6bc80f7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "74901892"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>Tutorial: Análisis de datos de Python para desarrolladores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este tutorial para programadores de SQL se explica cómo integrar Python mediante la creación y la implementación de una solución de aprendizaje automático basada en Python mediante la base de datos [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) en SQL Server. Se usará T-SQL, SQL Server Management Studio y una instancia del motor de base de datos con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y la compatibilidad con el lenguaje Python.

En este tutorial se presentan las funciones de Python usadas en un flujo de trabajo de modelado de datos. Algunos de los pasos aquí descritos son la exploración de datos, la creación y el entrenamiento de un modelo de clasificación binaria y la implementación del modelo. Se usarán datos de ejemplo de la Comisión de taxis y limusinas de Nueva York. Con ellos, se creará un modelo capaz de predecir si es probable que un cliente dé una propina por una carrera en función de la hora del día, la distancia recorrida y el punto de recogida. 

Todo el código de Python que se usa en este tutorial se ajusta en procedimientos almacenados que se crean y se ejecutan en Management Studio.

> [!NOTE]
> Este tutorial está disponible tanto en R como en Python. Para la versión de R, vea [Análisis en base de datos para desarrolladores de R](sqldev-in-database-r-for-sql-developers.md).

## <a name="overview"></a>Información general

El proceso de compilación de una solución de Machine Learning es una tarea compleja para la que se necesitan varias herramientas y la coordinación de expertos en la materia en distintas fases:

+ Obtención y limpieza de datos
+ Exploración de los datos y compilación de características útiles para el modelado
+ Entrenamiento y ajuste del modelo
+ Implementación en producción

La mejor manera de desarrollar y probar el código actual es usar un entorno de desarrollo dedicado. Pero, después de haber probado completamente el script, puede implementarlo fácilmente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el entorno de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] que ya conoce. El mecanismo principal para poner operativo el código en SQL Server consiste en ajustar el código externo en procedimientos almacenados.

Tanto si es un programador de SQL que no está familiarizado con Python como si es un desarrollador de Python que no está familiarizado con SQL, este tutorial de varias partes presenta un flujo de trabajo típico para realizar análisis en base de datos con Python y SQL Server. 

+ [Lección 1: Explorar y visualizar los datos mediante Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [Lección 2: Crear nuevas características de datos mediante funciones personalizadas de SQL](sqldev-py4-create-data-features-using-t-sql.md)

+ [Lección 3: Entrenar y guardar un modelo de Python mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [Lección 4: Predecir posibles resultados mediante un modelo de Python en un procedimiento almacenado](sqldev-py6-operationalize-the-model.md)

Después de guardar el modelo en la base de datos, llame al modelo de predicción desde [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.

## <a name="prerequisites"></a>Prerequisites

+ [SQL Server Machine Learning Services con Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Permisos](../security/user-permission.md)

+ [Base de datos de demo NYC Taxi](demo-data-nyctaxi-in-sql.md)

Todas las tareas se pueden realizar mediante procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

En este tutorial se supone que está familiarizado con las operaciones básicas de base de datos, como la creación de bases de datos y tablas, la importación de datos y la escritura de consultas SQL. Como no se presupone que conoce Python, se proporciona todo el código de Python. 

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Explorar y visualizar los datos mediante Python](sqldev-py3-explore-and-visualize-the-data.md)
