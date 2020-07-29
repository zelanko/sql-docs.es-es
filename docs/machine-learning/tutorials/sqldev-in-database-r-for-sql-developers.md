---
title: 'Tutorial de R y T-SQL: Desarrollo del modelo'
description: Sepa cómo insertar código del lenguaje de programación R en procedimientos almacenados de SQL Server y en funciones de T-SQL.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a27bd044dbdca7a05663080be08ebaff1acb86d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785608"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>Tutorial: Análisis de datos de R para desarrolladores de SQL
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

En este tutorial para programadores de SQL se explica cómo integrar R creando e implementando una solución de aprendizaje automático basada en R mediante la base de datos [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) en SQL Server. Se usará T-SQL, SQL Server Management Studio y una instancia del motor de base de datos con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y la compatibilidad con el lenguaje R.

En este tutorial se presentan las funciones de R usadas en un flujo de trabajo de modelado de datos. Algunos de los pasos aquí descritos son la exploración de datos, la creación y el entrenamiento de un modelo de clasificación binaria y la implementación del modelo. El modelo que se va a compilar predice si es probable que un trayecto acabe en propina en función de la hora del día, la distancia recorrida y la ubicación de origen. 

Todo el código de R que se usa en este tutorial se ajusta en procedimientos almacenados que se crean y se ejecutan en Management Studio.

## <a name="background-for-sql-developers"></a>Información general para desarrolladores de SQL

El proceso de compilación de una solución de Machine Learning es una tarea compleja para la que se necesitan varias herramientas y la coordinación de expertos en la materia en distintas fases:

+ Obtención y limpieza de datos
+ Exploración de los datos y compilación de características útiles para el modelado
+ Entrenamiento y ajuste del modelo
+ Implementación en producción

La mejor manera de desarrollar y probar el código real es usar un entorno de desarrollo dedicado de R. Pero, después de haber probado completamente el script, puede implementarlo fácilmente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el entorno de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] que ya conoce.

El propósito de este tutorial dividido en varias partes es mostrar un flujo de trabajo típico para migrar "código de R final" a SQL Server. 

- [Lección 1: Explorar y visualizar la forma y la distribución de los datos llamando a funciones de R en procedimientos almacenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lección 2: Crear características de datos con R en funciones de T-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lección 3: Entrenar y guardar un modelo de R con funciones y procedimientos almacenados](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lección 4: Predecir posibles resultados mediante un modelo de R en un procedimiento almacenado](../tutorials/sqldev-operationalize-the-model.md)

Después de que el modelo se ha guardado en la base de datos, llame al modelo de predicciones desde [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.

## <a name="prerequisites"></a>Prerrequisitos

Todas las tareas se pueden realizar mediante procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

En este tutorial se supone que está familiarizado con las operaciones básicas de base de datos, como la creación de bases de datos y tablas, la importación de datos y la escritura de consultas SQL. pero no con R, de ahí que se incluya todo el código de R. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) o [SQL Server Machine Learning Services con R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Bibliotecas de R](../package-management/r-package-information.md)

+ [Permisos](../security/user-permission.md)

+ [Base de datos de demo NYC Taxi](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Exploración y visualización de datos con funciones de R en procedimientos almacenados](../tutorials/sqldev-explore-and-visualize-the-data.md)
