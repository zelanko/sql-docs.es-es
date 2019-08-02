---
title: Información general del tutorial de SQL Server R
description: Introducción a los tutoriales de lenguaje R para SQL Server análisis de base de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ff1027a3a791ef0151e61982445cafff7be40329
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715422"
---
# <a name="sql-server-r-language-tutorials"></a>Tutoriales del lenguaje SQL Server R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describen los tutoriales del lenguaje R para el análisis en bases de datos en [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

+ Obtenga información sobre cómo ajustar y ejecutar código R en procedimientos almacenados.
+ Serialice y guarde modelos basados en r en bases de datos de SQL Server.
+ Obtenga información acerca de los contextos de cálculo remotos y locales, y cuándo usarlos.
+ Explore las bibliotecas de Microsoft R para las tareas de ciencia de datos y aprendizaje automático.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Guías de inicio rápido y tutoriales de R

| Vínculo | Descripción |
|------|-------------|
| [Inicio rápido: Uso de R en T-SQL](rtsql-using-r-code-in-transact-sql-quickstart.md) | En la primera de las guías de inicio rápido se ilustra la sintaxis básica para llamar a una función de R mediante un editor de consultas de T-SQL, como SQL Server Management Studio. |
| [Tutorial: Obtenga información sobre análisis de R en base de datos para científicos de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Para los desarrolladores de R nuevos en SQL Server, en este tutorial se explica cómo realizar tareas comunes de ciencia de datos en SQL Server. Cargar y visualizar datos, entrenar y guardar un modelo para SQL Server y usar el modelo para el análisis predictivo. |
| [Tutorial: Obtenga información sobre análisis de R en base de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Cree e implemente una solución completa de R, [!INCLUDE[tsql](../../includes/tsql-md.md)] con solo herramientas. Se centra en mover una solución a producción. Aprenderá cómo ajustar el código de R en un procedimiento almacenado, guardar un modelo de R en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y realizar llamadas con parámetros al modelo de R para la predicción. |
| [Tutorial: Análisis detallado de RevoScalepR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Obtenga información sobre cómo usar las funciones de los paquetes RevoScaleR. Mueva los datos entre R y SQL Server, y cambie los contextos de cálculo para adaptarse a una tarea determinada. Cree modelos y trazados, y muévalos entre el entorno de desarrollo y el servidor de base de datos. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Ejemplos de código

| Vínculo | Descripción |
|------|-------------|
| [Crear un modelo predictivo con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Obtenga información sobre cómo una empresa de alquiler de esquí podría usar el aprendizaje automático para predecir alquileres futuros, lo que ayuda al plan empresarial y al personal a satisfacer la demanda futura. |
| [Realice la agrupación en clústeres de clientes con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use el aprendizaje sin supervisión para segmentar a los clientes en función de los datos de ventas. |

## <a name="see-also"></a>Vea también

+ [Extensión de R a SQL Server](../concepts/extension-r.md)
+ [Tutoriales de Machine Learning Services de SQL Server](machine-learning-services-tutorials.md)

