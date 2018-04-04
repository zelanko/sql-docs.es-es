---
title: Eventos extendidos para supervisar las instrucciones de PREDICCIÓN | Documentos de Microsoft
titleSuffix: SQL Server
ms.custom: ''
ms.date: 03/01/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: d517da44f989620003fef35d2e4721eead15d5d5
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="extended-events-for-monitoring-predict-statements"></a>Eventos extendidos para la supervisión de las instrucciones de PREDICCIÓN

Este artículo describen los eventos extendidos proporcionados en SQL Server que puede utilizar para supervisar y analizar los trabajos que utilizan [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para realizar la puntuación en tiempo real en SQL Server.

La puntuación en tiempo real genera las puntuaciones de un modelo que se ha almacenado en SQL Server de aprendizaje automático. La función de PREDICCIÓN no requiere un tiempo de ejecución externo, como R o Python, solo un modelo que se ha creado mediante un formato binario específico. Para obtener más información, consulte [en tiempo real de puntuación](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="prerequisites"></a>Requisitos previos

Para obtener información general sobre eventos extendidos (a veces denominados XEvents) y cómo realizar el seguimiento de eventos en una sesión, vea estos artículos:

+ [Arquitectura y conceptos de eventos extendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurar la captura de eventos en SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Administrar sesiones de eventos en el Explorador de objetos](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>Tabla de eventos extendidos

Eventos extendidos siguientes están disponibles en todas las versiones de SQL Server que admiten la [T-SQL PREDECIR](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) instrucción, incluido SQL Server en Linux y base de datos de SQL Azure. 

La instrucción T-SQL PREDECIR se introdujo en SQL Server 2017. 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |event  |Desglose de tiempo de ejecución de Builtin|
|predict_model_cache_hit |event|Se produce cuando un modelo se recupera de la caché de modelos de la función de PREDICCIÓN. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché de modelos de la función de PREDICCIÓN.|
|predict_model_cache_insert |event  |   Se produce cuando un modelo de inserción en la caché de modelos de la función de PREDICCIÓN. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché de modelos de la función de PREDICCIÓN.    |
|predict_model_cache_miss   |event|Se produce cuando un modelo no se encuentra en la caché de modelos de la función de PREDICCIÓN. Frecuentes repeticiones de este evento pudieron indicar que SQL Server necesita más memoria. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché de modelos de la función de PREDICCIÓN.|
|predict_model_cache_remove |event| Se produce cuando se quita un modelo de memoria caché de modelos para la función de PREDICCIÓN. Use este evento junto con otros eventos predict_model_cache_ * para solucionar problemas causados por la caché de modelos de la función de PREDICCIÓN.|

## <a name="query-for-related-events"></a>Permite consultar los eventos relacionados

Para ver una lista de todas las columnas devueltas para estos eventos, ejecute la siguiente consulta en SQL Server Management Studio:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Ejemplos

Para capturar información sobre el rendimiento de una sesión de puntuación con PREDICCIÓN:

1. Crear un nuevo extendidos sesión de eventos, mediante Management Studio o en otro admite [herramienta](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).
2. Agregue los eventos `predict_function_completed` y `predict_model_cache_hit` a la sesión.
3. Inicie la sesión de eventos extendidos.
4. Ejecute la consulta que usa la PREDICCIÓN.

En los resultados, revise estas columnas:

+ El valor de `predict_function_completed` muestra cuánto tiempo la consulta invertida en cargar el modelo y la puntuación.
+ El valor booleano de `predict_model_cache_hit` indica si la consulta utiliza un modelo en memoria caché o no. 

### <a name="native-scoring-model-cache"></a>Caché de modelos de puntuación nativo

Además de los eventos específicos de PREDICCIÓN, puede usar las consultas siguientes para obtener más información sobre el modelo en memoria caché y el uso de caché:

Ver la caché de modelos de puntuación nativo:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

Ver los objetos en la memoria caché de modelos:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

