---
title: Tutorial para análisis en base de datos con R
description: Obtenga información sobre cómo insertar código de lenguaje de programación R en SQL Server procedimientos almacenados y funciones de T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5b2629a50a73208181cc14fd843cd9ab9c0b05df
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633605"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>Tutorial: Análisis de datos de R para desarrolladores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este tutorial para programadores de SQL, obtenga información sobre la integración de R mediante la creación e implementación de una solución de aprendizaje automático basada en R mediante una base de datos de [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) en SQL Server. Usará T-SQL, SQL Server Management Studio y una instancia del motor de base de datos con [Machine Learning Services] ([Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y la compatibilidad con el lenguaje R

En este tutorial se presentan las funciones de R que se usan en un flujo de trabajo de modelado de datos. Los pasos incluyen la exploración de datos, la compilación y el entrenamiento de un modelo de clasificación binaria y la implementación de modelos. El modelo que se va a compilar predice si es probable que un viaje genere una propina en función de la hora del día, la distancia recorrida y la ubicación de la recogida. 

Todo el código de R que se usa en este tutorial está incluido en procedimientos almacenados que se crean y ejecutan en Management Studio.

## <a name="background-for-sql-developers"></a>Información general para desarrolladores de SQL

El proceso de creación de una solución de aprendizaje automático es una compleja que puede implicar varias herramientas y la coordinación de expertos en la materia en varias fases:

+ obtención y limpieza de datos
+ exploración de los datos y creación de características útiles para el modelado
+ entrenamiento y ajuste del modelo
+ implementación en producción

El desarrollo y las pruebas del código real se realizan mejor con un entorno de desarrollo de R dedicado. Sin embargo, una vez que el script se ha probado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] completo, puede implementarlo fácilmente con procedimientos almacenados en el [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]entorno conocido de.

El propósito de este tutorial de varias partes es una introducción a un flujo de trabajo típico para migrar el "código de R terminado" a SQL Server. 

- [Lección 1: Explorar y visualizar la forma y la distribución de datos mediante una llamada a funciones de R en procedimientos almacenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lección 2: Crear características de datos mediante R en funciones de T-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lección 3: Entrenar y guardar un modelo de R con funciones y procedimientos almacenados](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lección 4: Predecir los resultados potenciales mediante un modelo de R en un procedimiento almacenado](../tutorials/sqldev-operationalize-the-model.md)

Una vez que el modelo se haya guardado en la base de datos, llame al modelo [!INCLUDE[tsql](../../includes/tsql-md.md)] para las predicciones desde mediante procedimientos almacenados.

## <a name="prerequisites"></a>Requisitos previos

Todas las tareas se pueden realizar [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]en.

En este tutorial se supone que está familiarizado con las operaciones básicas de base de datos, como la creación de bases de datos y tablas, la importación de datos y la escritura de consultas SQL. No supone que conoce R. Como tal, se proporciona todo el código de R. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) o [SQL Server Machine Learning Services con R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Bibliotecas de R](../package-management/r-package-information.md)

+ [Permisos](../security/user-permission.md)

+ [Base de datos de demostración de taxi de Nueva York](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Explorar y visualizar datos mediante funciones de R en procedimientos almacenados](../tutorials/sqldev-explore-and-visualize-the-data.md)
