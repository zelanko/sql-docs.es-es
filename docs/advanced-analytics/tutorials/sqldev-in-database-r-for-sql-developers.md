---
title: Tutorial para realizar análisis en bases de datos con R y SQL Server Machine Learning | Microsoft Docs
description: Aprenda a incrustar el código de idioma en las funciones de Transact-SQL y procedimientos almacenados de SQL Server de programación R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80c4d39e87984b022340079be4d944ed6ad963e3
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030652"
---
# <a name="tutorial-in-database-r-analytics-for-sql-developers"></a>Tutorial: Análisis de R en bases de datos para desarrolladores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial para programadores de SQL, obtenga información sobre la integración de R mediante la creación e implementación de una máquina basados en R de aprendizaje de la solución mediante un [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) base de datos en SQL Server. 

Este tutorial presentan las funciones de R que se usa en un flujo de trabajo de modelado de datos. Los pasos incluyen la exploración de datos, crear y entrenar un modelo de clasificación binaria y la implementación de modelos. Va a usar datos de ejemplo de los taxis de Nueva York y Limosine Comisión y el modelo que se compilará predice si un viaje es probable que produzca una propina en función de la hora del día, la distancia recorrida y la ubicación de recogida. Todo el código de R que se usa en este tutorial se incluye en los procedimientos almacenados que crean y ejecutan en Management Studio.


> [!NOTE]
> 
> Este tutorial está disponible en R y Python. Para la versión de Python, consulte [en análisis base de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md).

## <a name="overview"></a>Información general

El proceso de creación de una solución de aprendizaje automático es una compleja que puede implicar varias herramientas y la coordinación de expertos a través de varias fases:

+ obtención y limpieza de datos
+ explorar los datos y generar características útiles para el modelado
+ entrenamiento y el modelo de optimización
+ implementación en producción

Desarrollo y pruebas del código real se realiza mejor mediante un entorno de desarrollo dedicado. Sin embargo, después de la secuencia de comandos está probado completamente, puede implementar fácilmente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados en el entorno familiar de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Si es un programador SQL que está familiarizado con R, o es un desarrollador de R es nuevo en SQL, este tutorial de varias partes presentan un flujo de trabajo típico para llevar a cabo análisis en bases de datos con R y SQL Server. 

- [Lección 1: Explorar y visualizar la distribución y la forma de datos mediante una llamada a funciones de R en procedimientos almacenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lección 2: Crear características de datos mediante R en las funciones de Transact-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lección 3: Entrenar y guardar un modelo de R mediante procedimientos almacenados y funciones](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lección 4: Predecir resultados posibles con un modelo de R en un procedimiento almacenado](../tutorials/sqldev-operationalize-the-model.md)

Después de que el modelo se ha guardado en la base de datos, llamar al modelo para las predicciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.

## <a name="prerequisites"></a>Requisitos previos

Todas las tareas que pueden hacerse mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] los procedimientos almacenados de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Este tutorial supone que está familiarizado con operaciones de base de datos básica, como la creación de tablas y bases de datos, importación de datos y escribir consultas SQL. Supone que sabe R. Por lo tanto, se proporciona todo el código de R. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) o [SQL Server 2017 Machine Learning Services con R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Bibliotecas de R](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)

+ [Permisos](../security/user-permission.md)

+ [Base de datos de demostración de taxis de Nueva York](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Configurar la base de datos de taxis de Nueva York](demo-data-nyctaxi-in-sql.md)