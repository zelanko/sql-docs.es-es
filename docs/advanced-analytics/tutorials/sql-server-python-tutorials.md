---
title: Información general sobre el tutorial de Python de SQL Server 2017
description: Introducción a los tutoriales de Python para SQL Server 2017 análisis en base de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86c5eaa600da0dbe9106278dd36b21eba322e2b7
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345965"
---
# <a name="sql-server-2017-python-tutorials"></a>Tutoriales de Python SQL Server 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describen los tutoriales de Python para el análisis en bases de datos en [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). 

+ Obtenga información sobre cómo ajustar y ejecutar el código de Python en procedimientos almacenados.
+ Serialice y guarde modelos basados en Python en bases de datos de SQL Server.
+ Obtenga información acerca de los contextos de cálculo remotos y locales, y cuándo usarlos.
+ Explore los módulos de Microsoft Python para las tareas de ciencia de datos y aprendizaje automático.

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Inicios rápidos y tutoriales de Python

| Vínculo | Descripción |
|------|-------------|
| [Inicio rápido: Script de Python "Hello World" en SQL Server](quickstart-python-run-using-t-sql.md) | Conozca los aspectos básicos de cómo llamar a Python en T-SQL. |
| [Inicio rápido: Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server](quickstart-python-train-score-in-tsql.md) | Explica los mecanismos para insertar código Python en un procedimiento almacenado, proporcionar entradas y ejecutar procedimientos almacenados. |
| [Tutorial: Creación de un modelo con revoscalepy](use-python-revoscalepy-to-create-model.md) | Muestra cómo ejecutar código desde un terminal de Python remoto, utilizando SQL Server contexto de proceso. Debe estar familiarizado con las herramientas y los entornos de Python. Se proporciona código de ejemplo que crea un modelo mediante **rxLinMod**, desde la nueva biblioteca **revoscalepy** . |
| [Tutorial: Aprenda análisis de Python en base de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md) | En este tutorial de un extremo a otro se muestra el proceso de creación de una solución completa de Python mediante procedimientos almacenados de T-SQL. Se incluye todo el código de Python.|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Ejemplos de código

Estos ejemplos y demostraciones proporcionados por el equipo de desarrollo de SQL Server resaltan las formas en que puede usar análisis insertados en aplicaciones reales.

| Vínculo | Descripción |
|------|-------------|
| [Creación de un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Obtenga información sobre cómo una empresa de alquiler de esquí podría usar el aprendizaje automático para predecir alquileres futuros, lo que ayuda al plan empresarial y al personal a satisfacer la demanda futura. |
| [Realice la agrupación en clústeres de clientes con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Obtenga información acerca de cómo usar el algoritmo Kmeans para realizar clústeres sin supervisión de clientes. |

## <a name="see-also"></a>Vea también

+ [Extensión de Python para SQL Server](../concepts/extension-python.md)
+ [Tutoriales de Machine Learning Services de SQL Server](machine-learning-services-tutorials.md)
