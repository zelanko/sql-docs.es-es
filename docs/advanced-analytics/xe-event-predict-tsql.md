---
title: Eventos extendidos para la supervisión de instrucciones PREDICT
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 283e128285fc50b9109d7950b171e30224fb9692
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714643"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>Eventos extendidos para la supervisión de instrucciones PREDICT

En este artículo se describen los eventos extendidos proporcionados en SQL Server que puede usar para supervisar y analizar los trabajos que usan [predicción](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para realizar puntuaciones en tiempo real en SQL Server.

La puntuación en tiempo real genera puntuaciones de un modelo de aprendizaje automático que se ha almacenado en SQL Server. La función PREDICT no requiere un tiempo de ejecución externo como R o Python, solo un modelo que se ha creado con un formato binario específico. Para obtener más información, vea [puntuación en tiempo real](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="prerequisites"></a>Requisitos previos

Para obtener información general sobre los eventos extendidos (a veces denominados XEvents) y cómo realizar un seguimiento de los eventos de una sesión, consulte estos artículos:

+ [Conceptos y arquitectura de Extended Events](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configuración de la captura de eventos en SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Administrar sesiones de eventos en el Explorador de objetos](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>Tabla de eventos extendidos

Los siguientes eventos extendidos están disponibles en todas las versiones de SQL Server que admiten la instrucción de [predicción de T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) , incluidos SQL Server en Linux y Azure SQL Database. 

La instrucción de predicción de T-SQL se presentó en SQL Server 2017. 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |event  |Desglose del tiempo de ejecución integrado|
|predict_model_cache_hit |event|Se produce cuando se recupera un modelo de la caché del modelo de la función PREDICT. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché del modelo de la función PREDICT.|
|predict_model_cache_insert |event  |   Se produce cuando se inserta un modelo en la caché del modelo de la función PREDICT. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché del modelo de la función PREDICT.    |
|predict_model_cache_miss   |event|Se produce cuando no se encuentra un modelo en la caché del modelo de la función PREDICT. Las apariciones frecuentes de este evento podrían indicar que SQL Server necesita más memoria. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché del modelo de la función PREDICT.|
|predict_model_cache_remove |event| Se produce cuando se quita un modelo de la caché del modelo para la función de predicción. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché del modelo de la función PREDICT.|

## <a name="query-for-related-events"></a>Consultar eventos relacionados

Para ver una lista de todas las columnas devueltas para estos eventos, ejecute la siguiente consulta en SQL Server Management Studio:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Ejemplos

Para capturar información sobre el rendimiento de una sesión de puntuación mediante predicción:

1. Cree una nueva sesión de eventos extendidos con Management Studio u otra [herramienta](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)compatible.
2. Agregue los eventos `predict_function_completed` y `predict_model_cache_hit` a la sesión.
3. Inicie la sesión de eventos extendidos.
4. Ejecute la consulta que usa predicción.

En los resultados, revise estas columnas:

+ El valor de `predict_function_completed` muestra cuánto tiempo tardó la consulta en cargar el modelo y la puntuación.
+ El valor booleano para `predict_model_cache_hit` indica si la consulta usó o no un modelo almacenado en caché. 

### <a name="native-scoring-model-cache"></a>Caché del modelo de puntuación nativo

Además de los eventos específicos de la predicción, puede utilizar las siguientes consultas para obtener más información sobre el uso de la caché y el modelo en caché:

Ver la memoria caché del modelo de puntuación nativa:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

Ver los objetos en la memoria caché del modelo:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

