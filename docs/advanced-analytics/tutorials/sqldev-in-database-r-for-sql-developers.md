---
title: Tutorial para realizar análisis en bases de datos con R - SQL Server Machine Learning
description: Aprenda a incrustar el código de idioma en las funciones de Transact-SQL y procedimientos almacenados de SQL Server de programación R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8d3235c585d3ea56a64776fde841ccc6d71b1a4d
ms.sourcegitcommit: 2e8783e6bedd9597207180941be978f65c2c2a2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2019
ms.locfileid: "54405605"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>Tutorial: Análisis de datos de R para desarrolladores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial para programadores de SQL, obtenga información sobre la integración de R mediante la creación e implementación de una máquina basados en R de aprendizaje de la solución mediante un [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) base de datos en SQL Server. Usará una instancia del motor de base de datos con [Machine Learning Services], SQL Server Management Studio y Transact-SQL ([Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y la compatibilidad del lenguaje R

Este tutorial presentan las funciones de R que se usa en un flujo de trabajo de modelado de datos. Los pasos incluyen la exploración de datos, crear y entrenar un modelo de clasificación binaria y la implementación de modelos. El modelo que se compilará predice si un viaje es probable que produzca una propina en función de la hora del día, la distancia recorrida y la ubicación de recogida. 

Todo el código de R que se usa en este tutorial se incluye en los procedimientos almacenados que crean y ejecutan en Management Studio.

## <a name="background-for-sql-developers"></a>En segundo plano para desarrolladores de SQL

El proceso de creación de una solución de aprendizaje automático es una compleja que puede implicar varias herramientas y la coordinación de expertos a través de varias fases:

+ obtención y limpieza de datos
+ explorar los datos y generar características útiles para el modelado
+ entrenamiento y el modelo de optimización
+ implementación en producción

Desarrollo y pruebas del código real se realiza mejor mediante un entorno de desarrollo de R dedicado. Sin embargo, después de la secuencia de comandos está probado completamente, puede implementar fácilmente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados en el entorno familiar de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

El propósito de este tutorial de varias partes es una introducción a un flujo de trabajo típico para migrar "termine de código de R" para SQL Server. 

- [Lección 1: Explorar y visualizar la distribución y la forma de datos mediante una llamada a funciones de R en procedimientos almacenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lección 2: Crear características de datos mediante R en las funciones de Transact-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lección 3: Entrenar y guardar un modelo de R mediante procedimientos almacenados y funciones](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lección 4: Predecir los resultados posibles con un modelo de R en un procedimiento almacenado](../tutorials/sqldev-operationalize-the-model.md)

Después de que el modelo se ha guardado en la base de datos, llamar al modelo para las predicciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.

## <a name="prerequisites"></a>Requisitos previos

Todas las tareas que pueden hacerse mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] los procedimientos almacenados de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Este tutorial supone que está familiarizado con operaciones de base de datos básica, como la creación de tablas y bases de datos, importación de datos y escribir consultas SQL. Supone que sabe R. Por lo tanto, se proporciona todo el código de R. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) o [SQL Server 2017 Machine Learning Services con R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Bibliotecas de R](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)

+ [Permisos](../security/user-permission.md)

+ [NYC Taxi demo database](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Configurar la base de datos de taxis de Nueva York](demo-data-nyctaxi-in-sql.md)