---
title: 'Eventos extendidos para la supervisión de instrucciones PREDICT: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e680da7485069e6838edff260a505461a22c472b
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432248"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>Eventos extendidos para la supervisión de instrucciones PREDICT

En este artículo se describe los eventos extendidos proporcionados en SQL Server que puede usar para supervisar y analizar los trabajos que usan [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para realizar la puntuación en tiempo real en SQL Server.

Puntuación en tiempo real genera las puntuaciones de un modelo de machine learning que se ha almacenado en SQL Server. La función PREDICT no requiere un tiempo de ejecución externo como R o Python, solo un modelo que se ha creado utilizando un formato binario concreto. Para obtener más información, consulte [de puntuación en tiempo real](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="prerequisites"></a>Requisitos previos

Para obtener información general sobre eventos extendidos (a veces denominados XEvents) y cómo realizar el seguimiento de eventos en una sesión, consulte estos artículos:

+ [Arquitectura y conceptos de eventos extendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurar la captura de eventos en SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Administrar sesiones de eventos en el Explorador de objetos](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>Tabla de eventos extendidos

Los siguientes eventos extendidos están disponibles en todas las versiones de SQL Server que admiten la [T-SQL PREDECIR](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) instrucción, incluido SQL Server en Linux y Azure SQL Database. 

La instrucción T-SQL PREDECIR se introdujo en SQL Server 2017. 

|NAME |object_type|description| 
|----|----|----|
|predict_function_completed |event  |Desglose de tiempo de ejecución de Builtin|
|predict_model_cache_hit |event|Se produce cuando un modelo se recupera de la caché del modelo de función PREDICT. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché del modelo de función PREDICT.|
|predict_model_cache_insert |event  |   Se produce cuando un modelo se inserta en la caché del modelo de función PREDICT. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché del modelo de función PREDICT.    |
|predict_model_cache_miss   |event|Se produce cuando un modelo no se encuentra en la caché del modelo de función PREDICT. La aparición frecuente de este evento podría indicar que SQL Server necesita más memoria. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché del modelo de función PREDICT.|
|predict_model_cache_remove |event| Se produce cuando se quita un modelo de memoria caché de modelos para la función PREDICT. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché del modelo de función PREDICT.|

## <a name="query-for-related-events"></a>Consulta los eventos relacionados

Para ver una lista de todas las columnas devueltas para estos eventos, ejecute la siguiente consulta en SQL Server Management Studio:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Ejemplos

Para capturar información sobre el rendimiento de una sesión de puntuación mediante PREDICT:

1. Cree un nuevo extendidos de la sesión de eventos, mediante Management Studio u otra admite [herramienta](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).
2. Agregue los eventos `predict_function_completed` y `predict_model_cache_hit` a la sesión.
3. Inicie la sesión de eventos extendidos.
4. Ejecute la consulta que usa la PREDICCIÓN.

En los resultados, revise estas columnas:

+ El valor de `predict_function_completed` muestra cuánto tiempo la consulta dedicada a cargar el modelo y la puntuación.
+ El valor booleano para `predict_model_cache_hit` indica si la consulta utiliza un modelo en caché o no. 

### <a name="native-scoring-model-cache"></a>Caché del modelo de puntuación nativa

Además de los eventos específicos de PREDICCIÓN, puede usar las siguientes consultas para obtener más información sobre el modelo en caché y el uso de memoria caché:

Vista de la caché del modelo de puntuación nativa:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

Ver los objetos de la caché del modelo:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

