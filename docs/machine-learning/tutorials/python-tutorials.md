---
title: Tutoriales de Python
description: En este artículo se describen los tutoriales de Python para SQL Server Machine Learning Services. Obtenga información sobre cómo ejecutar scripts y crear modelos de aprendizaje automático en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e3733f12ed93d7c84a86259742b6996333c3900f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487358"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>Tutoriales de Python para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describen los tutoriales e inicios rápidos de Python para [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

+ Aprenda a ejecutar scripts de Python.
+ Compile, entrene e implemente modelos de Python en SQL Server.
+ Obtenga información sobre contextos de proceso locales y remotos.
+ Explore los paquetes de Microsoft Python para ciencia de datos y aprendizaje automático.

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Tutoriales de Python

| Tutorial | Descripción |
|-|-|
| [Predicción de alquiler de esquís con regresión lineal](python-ski-rental-linear-regression.md) | Utilice Python con regresión lineal para predecir el número de alquileres de esquí. Use cuadernos en Azure Data Studio para preparar los datos y entrenar el modelo y T-SQL para la implementación de modelo. |
| [Categorización de clientes con agrupación en clústeres k-means](python-clustering-model.md) | Utilice Python para desarrollar e implementar un modelo de agrupación en clústeres K-means para clasificar a los clientes. Use cuadernos en Azure Data Studio para preparar los datos y entrenar el modelo y T-SQL para la implementación de modelo. |
| [Creación de un modelo mediante revoscalepy](use-python-revoscalepy-to-create-model.md) | Muestra cómo ejecutar código desde un cliente de Python remoto mediante SQL Server como contexto de proceso. En el tutorial se crea un modelo con la función **rxLinMod** de la biblioteca **revoscalepy**. |
| [Análisis de datos de Python para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md) | En este tutorial integral se muestra el proceso de compilación de una solución completa de Python mediante T-SQL. |

## <a name="python-quickstarts"></a>Inicios rápidos de Python

Si no está familiarizado con SQL Server Machine Learning Services, puede probar también los inicios rápidos de Python.

| Guía de inicio rápido | Descripción |
|-|-|
| [Hola mundo en Python y SQL Server](quickstart-python-create-script.md) | Conozca los conceptos básicos sobre cómo llamar a Python en T-SQL con [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Control de tipos de datos y objetos mediante Python en SQL Server](quickstart-python-data-structures.md) | Muestra cómo SQL Server usa el paquete pandas de Python para administrar estructuras de datos. |
| [Creación y puntuación de un modelo predictivo en Python](quickstart-python-train-score-model.md) | Explica cómo crear, entrenar y usar un modelo de Python para hacer predicciones a partir de nuevos datos. |

## <a name="next-steps"></a>Pasos siguientes

+ [¿Qué es SQL Server Machine Learning Services (Python y R)?](../sql-server-machine-learning-services.md)
+ [Extensión de Python en SQL Server](../concepts/extension-python.md)