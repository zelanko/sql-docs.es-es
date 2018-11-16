---
title: En bases de datos análisis de Python para desarrolladores de SQL | Microsoft Docs
description: Obtenga información sobre cómo insertar código de Python en las funciones de Transact-SQL y procedimientos almacenados de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 728ab56a844a6c7a14f5de7e39abc5d38146c85a
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560388"
---
# <a name="tutorial-in-database-python-analytics-for-sql-developers"></a>Tutorial: Análisis de Python en bases de datos para desarrolladores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial para programadores de SQL, obtenga información sobre la integración de Python mediante la creación e implementación de una máquina basada en Python y aprendizaje de la solución mediante un [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) base de datos en SQL Server. 

Este tutorial presenta funciones de Python que se usan en un flujo de trabajo de modelado de datos. Los pasos incluyen la exploración de datos, crear y entrenar un modelo de clasificación binaria y la implementación de modelos. Va a usar datos de ejemplo de los taxis de Nueva York y Limosine Comisión y el modelo que se compilará predice si un viaje es probable que produzca una propina en función de la hora del día, la distancia recorrida y la ubicación de recogida. Todo el código de Python que se usa en este tutorial se incluye en los procedimientos almacenados que crean y ejecutan en Management Studio.

> [!NOTE]
> Este tutorial está disponible en R y Python. Para la versión de R, consulte [en análisis base de datos para los desarrolladores de R](sqldev-in-database-r-for-sql-developers.md).

## <a name="overview"></a>Información general

El proceso de creación de una solución de aprendizaje automático es una compleja que puede implicar varias herramientas y la coordinación de expertos a través de varias fases:

+ obtención y limpieza de datos
+ explorar los datos y generar características útiles para el modelado
+ entrenamiento y el modelo de optimización
+ implementación en producción

Desarrollo y pruebas del código real se realiza mejor mediante un entorno de desarrollo dedicado. Sin embargo, después de la secuencia de comandos está probado completamente, puede implementar fácilmente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados en el entorno familiar de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Ajuste el código externo en los procedimientos almacenados es el mecanismo principal para el código de puesta en marcha en SQL Server.

Tanto si es un programador SQL nuevo para Python, o un desarrollador de Python es nuevo en SQL, este tutorial de varias partes presenta un flujo de trabajo típico para llevar a cabo análisis en bases de datos con Python y SQL Server. 

+ [Lección 1: Explorar y visualizar datos mediante Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [Lección 2: Crear características de datos mediante funciones SQL personalizadas](sqldev-py4-create-data-features-using-t-sql.md)

+ [Lección 3: Entrenar y guardar un modelo de Python mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [Lección 4: Predecir resultados posibles con un modelo de Python en un procedimiento almacenado](sqldev-py6-operationalize-the-model.md)

Después de que el modelo se ha guardado en la base de datos, puede llamar el modelo para las predicciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.

## <a name="prerequisites"></a>Requisitos previos

+ [Servicios SQL Server 2017 Machine Learning con Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Permisos](../security/user-permission.md)

+ [Base de datos de demostración de taxis de Nueva York](demo-data-nyctaxi-in-sql.md)

Todas las tareas que pueden hacerse mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] los procedimientos almacenados de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Este tutorial supone que está familiarizado con operaciones de base de datos básica, como la creación de tablas y bases de datos, importación de datos y escribir consultas SQL. Supone que sabe Python. Por lo tanto, se proporciona todo el código Python. 

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Explorar y visualizar datos mediante Python](sqldev-py3-explore-and-visualize-the-data.md)
