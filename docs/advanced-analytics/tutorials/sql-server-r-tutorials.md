---
title: 'SQL Server R información general del tutorial: SQL Server Machine Learning'
description: Introducción a los tutoriales de lenguaje R para realizar análisis en bases de datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 467c9320880f1b113cecd36101345f6ee99f7b75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961937"
---
# <a name="sql-server-r-language-tutorials"></a>Tutoriales del lenguaje R de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describe en los tutoriales del lenguaje R para realizar análisis en bases de datos [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [Machine Learning Services de SQL Server 2017](../install/sql-machine-learning-services-windows-install.md).

+ Obtenga información sobre cómo ajustar y ejecutar código R en procedimientos almacenados.
+ Serialice y guardar los modelos basados en r en bases de datos de SQL Server.
+ Obtenga información sobre los contextos de cálculo locales y remotos y cuándo utilizarlas.
+ Explore las bibliotecas de Microsoft R para tareas de aprendizaje automático y ciencia de datos.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Tutoriales y guías de inicio rápido de R

| Vínculo | Descripción |
|------|-------------|
| [Inicio rápido: Uso de R en Transact-SQL](rtsql-using-r-code-in-transact-sql-quickstart.md) | En primer lugar de varias guías de inicio rápido, con ésta que ilustra la sintaxis básica para llamar a una función de R mediante un editor de consultas de Transact-SQL como SQL Server Management Studio. |
| [Tutorial: Obtenga información sobre análisis de R en bases de datos para los científicos de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Para los desarrolladores de R contactos SQL Server, este tutorial se explica cómo se lleve a cabo tareas de ciencia de datos comunes en SQL Server. Cargar y visualizar datos, entrenar y guardar un modelo en SQL Server y utilizar el modelo para realizar análisis predictivos. |
| [Tutorial: Obtenga información sobre análisis de R en bases de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Compilar e implementar una solución completa de R, con solo [!INCLUDE[tsql](../../includes/tsql-md.md)] herramientas. Se centra en pasar de una solución a producción. Aprenderá cómo ajustar el código de R en un procedimiento almacenado, guardar un modelo de R en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y realizar llamadas con parámetros al modelo de R para la predicción. |
| [Tutorial: Profundización RevoScalepR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Obtenga información sobre cómo usar las funciones de los paquetes de RevoScaleR. Mover datos entre R y SQL Server y cambiar los contextos para adaptarse a una determinada tarea de proceso. Cree modelos y trazados y moverlos entre el entorno de desarrollo y el servidor de base de datos. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Ejemplos de código

| Vínculo | Descripción |
|------|-------------|
| [Crear un modelo predictivo con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Obtenga información sobre cómo una empresa de alquiler de esquís puede usar el aprendizaje automático para predecir alquileres futuros, que permite el plan de negocio y personal para satisfacer la demanda futura. |
| [Realizar el cliente clústeres que usan R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Usar aprendizaje no supervisado para segmentar los clientes en función de los datos de ventas. |

## <a name="see-also"></a>Vea también

+ [Extensión de R a SQL Server](../concepts/extension-r.md)
+ [Tutoriales de SQL Server Machine Learning Services](machine-learning-services-tutorials.md)

