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
ms.openlocfilehash: cd458727fad637414d7c71865b2633f3caf80175
ms.sourcegitcommit: 949e55b32eff6610087819a93160a35af0c5f1c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70383559"
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

| Guía de inicio rápido | Descripción |
|-|-|
| [Hola mundo en Python y SQL Server](quickstart-python-run-using-t-sql.md) | Conozca los aspectos básicos de cómo llamar a Python en T-SQL. |
| [Control de entradas y salidas mediante Python en SQL Server](quickstart-python-inputs-and-outputs.md) | Obtenga información sobre cómo controlar las entradas y salidas de Python en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Estructuras de datos de Python en SQL Server](quickstart-python-data-structures.md) | Muestra cómo SQL Server usa el paquete pandas de Python para administrar estructuras de datos. |
| [Entrenar y usar el primer modelo](quickstart-python-train-score-in-tsql.md) | Explica cómo crear, entrenar y usar un modelo de Python para predecir datos nuevos. |

## <a name="next-steps"></a>Pasos siguientes

+ [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
+ [Extensión de Python para SQL Server](../concepts/extension-python.md)