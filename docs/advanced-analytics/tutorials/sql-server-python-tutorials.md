---
title: 'Tutorial introductorio de Python de SQL Server 2017: aprendizaje automático de SQL Server'
description: Introducción a los tutoriales de Python para realizar análisis en bases de datos de SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f31da296bf55b7da55a4e5a8398d411bc5a5b0ea
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510322"
---
# <a name="sql-server-2017-python-tutorials"></a>Tutoriales de Python de SQL Server 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe los tutoriales de Python para realizar análisis en bases de datos en [Machine Learning Services de SQL Server 2017](../install/sql-machine-learning-services-windows-install.md). 

+ Obtenga información sobre cómo ajustar y ejecutar código de Python en los procedimientos almacenados.
+ Serialice y guardar los modelos basados en Python en las bases de datos de SQL Server.
+ Obtenga información sobre los contextos de cálculo locales y remotos y cuándo utilizarlas.
+ Explore los módulos de Python de Microsoft para tareas de aprendizaje automático y ciencia de datos.

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Tutoriales y guías de inicio rápido de Python

| Vínculo | Descripción |
|------|-------------|
| [Inicio rápido: Script de Python "Hello world" en SQL Server](quickstart-python-run-using-t-sql.md) | Obtenga información sobre los conceptos básicos de cómo llamar a Python en T-SQL. |
| [Inicio rápido: Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server](quickstart-python-train-score-in-tsql.md) | Explica los mecanismos de incrustación de código de Python en un procedimiento almacenado, que proporciona las entradas y ejecución del procedimiento almacenado. |
| [Tutorial: Crear un modelo mediante revoscalepy](use-python-revoscalepy-to-create-model.md) | Muestra cómo ejecutar código desde un terminal de Python remoto, utilizando el contexto de proceso de SQL Server. Debe estar un poco familiarizado con los entornos y herramientas de Python. Código de ejemplo es que crea un modelo con **rxLinMod**, desde el nuevo **revoscalepy** biblioteca. |
| [Tutorial: Obtenga información sobre análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md) | En este tutorial de extremo a extremo muestra el proceso de creación de una solución completa de Python mediante procedimientos almacenado de Transact-SQL. Se incluye todo el código Python.|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Ejemplos de código

Estos ejemplos y demostraciones proporcionadas por el equipo de desarrollo de SQL Server resaltan formas en que puede usar análisis insertados en aplicaciones del mundo real.

| Vínculo | Descripción |
|------|-------------|
| [Crear un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Obtenga información sobre cómo una empresa de alquiler de esquís puede usar el aprendizaje automático para predecir alquileres futuros, que permite el plan de negocio y personal para satisfacer la demanda futura. |
| [Realizar el cliente agrupación en clústeres con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Obtenga información sobre cómo usar el algoritmo de Kmeans para realizar una agrupación en clústeres no supervisado de los clientes. |

## <a name="see-also"></a>Vea también

+ [Extensión de Python para SQL Server](../concepts/extension-python.md)
+ [Tutoriales de SQL Server Machine Learning Services](machine-learning-services-tutorials.md)
