---
title: Tutoriales de R
description: En este artículo se describen los tutoriales e inicios rápidos de R para SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/13/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 952a33eb5a160acae44b5d1ae674c75b8d74cca5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487307"
---
# <a name="r-tutorials-for-sql-server-machine-learning-services"></a>Tutoriales de R para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describen los tutoriales e inicios rápidos de R para [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md).

+ Aprenda a ejecutar scripts de R.
+ Compile, entrene e implemente modelos de R en SQL Server.
+ Obtenga información sobre contextos de proceso locales y remotos.
+ Explore los paquetes de Microsoft R para ciencia de datos y aprendizaje automático.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Guías de inicio rápido y tutoriales de R

| Vínculo | Descripción |
|------|-------------|
| [Inicio rápido: Creación y ejecución de scripts de R simples](quickstart-r-create-script.md) | En la primera de las guías de inicio rápido se ilustra la sintaxis básica para llamar a una función de R con un editor de consultas de T-SQL como SQL Server Management Studio. |
| [Tutorial: Análisis de R en base de datos para científicos de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Los desarrolladores de R que no conozcan SQL Server aprenderán en este tutorial a realizar tareas comunes de ciencia de datos en SQL Server. Cargue y visualice datos, entrene y guarde un modelo para SQL Server y, luego, úselo para realizar análisis predictivos. |
| [Tutorial: Análisis de R en base de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Cree e implemente una solución de R completa usando únicamente [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este tutorial se centra en el paso de una solución a producción. Aprenderá cómo ajustar el código de R en un procedimiento almacenado, guardar un modelo de R en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y realizar llamadas con parámetros al modelo de R para la predicción. |
| [Tutorial: Análisis detallado de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Aprenda a usar las funciones de los paquetes RevoScaleR. Mueva datos entre R y SQL Server, y cambie entre contextos de cálculo para adaptarse a una tarea determinada. Cree modelos y trazados y muévalos entre el entorno de desarrollo y el servidor de bases de datos. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Ejemplos de código

| Vínculo | Descripción |
|------|-------------|
| [Compilación de un modelo predictivo con R en SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Verá cómo se podría utilizar Machine Learning en una empresa de alquiler de esquís para predecir alquileres futuros, lo que resulta muy útil para el plan de negocios y para el personal a la hora de satisfacer la futura demanda. |
| [Agrupaciones en clústeres de clientes con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use el aprendizaje sin supervisión para segmentar a los clientes en función de los datos de ventas. |

## <a name="see-also"></a>Consulte también

+ [Extensión de R en SQL Server](../concepts/extension-r.md)