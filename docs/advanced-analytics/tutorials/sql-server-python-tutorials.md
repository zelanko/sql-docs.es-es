---
title: Tutoriales de Python
description: En este artículo se describen los tutoriales de Python para SQL Server Machine Learning Services. Obtenga información sobre cómo ejecutar scripts de Python. Compilar, entrenar e implementar modelos de Python en SQL Server. Más información sobre los contextos de cálculo remotos y locales. Explore los paquetes de Microsoft Python para ciencia de datos y aprendizaje automático.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 80f714810acd8c04c80fe0b8abe5214a456f6dd6
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199407"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>Tutoriales de Python para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describen los tutoriales de Python y las guías de inicio rápido para [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

+ Obtenga información sobre cómo ejecutar scripts de Python.
+ Compilar, entrenar e implementar modelos de Python en SQL Server.
+ Más información sobre los contextos de cálculo remotos y locales.
+ Explore los paquetes de Microsoft Python para ciencia de datos y aprendizaje automático.

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Tutoriales de Python

| Tutorial | Descripción |
|-|-|
| [Predecir Alquiler de esquí con regresión lineal](python-ski-rental-linear-regression.md) | Use Python y la regresión lineal para predecir el número de alquileres de esquí. Use cuadernos en Azure Data Studio para preparar los datos y entrenar el modelo y T-SQL para la implementación del modelo. |
| [Categorización de clientes mediante la agrupación en clústeres k-means](python-clustering-model.md) | Use Python para desarrollar e implementar un modelo de agrupación en clústeres K-means para clasificar a los clientes. Use cuadernos en Azure Data Studio para preparar los datos y entrenar el modelo y T-SQL para la implementación del modelo. |
| [Creación de un modelo con revoscalepy](use-python-revoscalepy-to-create-model.md) | Muestra cómo ejecutar código desde un cliente de Python remoto mediante SQL Server como contexto de proceso. En el tutorial se crea un modelo con **rxLinMod** desde la biblioteca de **revoscalepy** . |
| [Análisis de datos de Python para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md) | En este tutorial completo se muestra el proceso de creación de una solución de Python completa mediante T-SQL. |

## <a name="python-quickstarts"></a>Inicios rápidos de Python

Si no está familiarizado con SQL Server Machine Learning Services, también puede probar las guías de inicio rápido de Python.

| Inicio rápido | Descripción |
|-|-|
| [Hola mundo en Python y SQL Server](quickstart-python-create-script.md) | Conozca los aspectos básicos de cómo llamar a Python en T-SQL con [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Control de tipos de datos y objetos mediante Python en SQL Server](quickstart-python-data-structures.md) | Muestra cómo SQL Server usa el paquete pandas de Python para administrar estructuras de datos. |
| [Crear y puntuar un modelo predictivo en Python](quickstart-python-train-score-model.md) | Explica cómo crear, entrenar y usar un modelo de Python para hacer predicciones a partir de nuevos datos. |

## <a name="next-steps"></a>Pasos siguientes

+ [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
+ [Extensión de Python para SQL Server](../concepts/extension-python.md)