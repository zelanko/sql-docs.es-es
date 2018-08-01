---
title: Procesamiento de consultas inteligente en bases de datos de Microsoft SQL | Microsoft Docs
description: Características de procesamiento de consultas inteligente para mejorar el rendimiento de las consultas en SQL Server y Azure SQL Database.
ms.custom: ''
ms.date: 07/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6f1b215e95b7cc911cd2815493eabbbd53a47424
ms.sourcegitcommit: a162a8f02d66c13b32d0b6255b0b52fc80e2187e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2018
ms.locfileid: "39250453"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Procesamiento de consultas inteligente en bases de datos SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

La familia de características de **procesamiento de consultas inteligente** incluye características con un gran impacto que mejoran el rendimiento de las cargas de trabajo existentes con un esfuerzo de implementación mínimo.

![Características de procesamiento de consultas inteligentes](./media/1_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>Procesamiento de consultas adaptable
La familia de características de procesamiento de consultas adaptable incluye mejoras en el procesamiento de consultas que adaptan las estrategias de optimización a las condiciones de tiempo de ejecución de la carga de trabajo de la aplicación. Estas mejoras incluyen combinaciones adaptables del modo de proceso por lotes, comentarios de concesión de memoria y la ejecución intercalada de funciones con valores de tabla de múltiples instrucciones.

### <a name="batch-mode-adaptive-joins"></a>Combinaciones adaptables de modo de proceso por lotes
Esta característica permite cambiar su plan de forma dinámica a una mejor estrategia de combinación durante la ejecución mediante un único plan almacenado en caché.

### <a name="row-and-batch-mode-memory-grant-feedback"></a>Comentarios de concesión de memoria del modo de fila y el modo de proceso por lotes
Esta característica recalcula la memoria real necesaria para una consulta y actualiza el valor de la concesión del plan almacenado en caché, con lo que se reducen las concesiones de memoria excesivas que afectan a la simultaneidad y se corrigen concesiones de memoria subestimadas que provocan desbordamientos costosos en el disco.

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones (MSTVF)
Con la ejecución intercalada se usan los recuentos de filas reales de la función para tomar decisiones fundamentadas sobre los planes de consulta descendentes. 

Para más información, consulte [Procesamiento de consultas adaptable en bases de datos SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="table-variable-deferred-compilation"></a>Compilación diferida de variables de tabla
La compilación diferida de variables de tabla mejora la calidad del plan y el rendimiento general de las consultas que hacen referencia a las variables de tabla. Durante la optimización y la compilación inicial, esta característica propagará las estimaciones de cardinalidad que se basan en los recuentos de filas de variables de tabla reales.  Con la compilación diferida de variables de tabla, la compilación de una instrucción que hace referencia a una variable de tabla se difiere hasta la primera ejecución real de la instrucción.

Con la compilación aplazada variable de tabla, la compilación de una instrucción que hace referencia a una variable de tabla se aplaza hasta que la primera ejecución real de la instrucción. El comportamiento de esta compilación diferida es idéntico al comportamiento de las tablas temporales y este cambio genera el uso de la cardinalidad real en lugar de la estimación de una fila original. Para habilitar la versión preliminar pública de la compilación diferida de variables de tabla en Azure SQL Database, habilite el nivel 150 de compatibilidad de la base de datos para la base de datos a la que se conecta cuando ejecuta la consulta.

Para obtener más información, consulte [Compilación diferida de variables de tabla](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation ).

## <a name="approximate-query-processing"></a>Procesamiento de consultas aproximado
El procesamiento de consultas aproximado es una nueva familia de características diseñadas para proporcionar agregaciones de conjuntos de datos de gran tamaño en los que la capacidad de respuesta resulta más fundamental que la precisión absoluta.  Un ejemplo podría ser calcular el valor COUNT(DISTINCT()) entre 10 mil millones de filas para mostrar en un panel.  En este caso, la precisión absoluta no es importante, pero la capacidad de respuesta es fundamental. La función de agregado APPROX_COUNT_DISTINCT nueva devuelve el número aproximado de valores no nulos únicos de un grupo.

Para más información, consulte [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="see-also"></a>Vea también
[Performance Center for SQL Server Database Engine and Azure SQL Database](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)    (Centro de rendimiento para el motor de base de datos SQL Server y Azure SQL Database)  
[Query Processing Architecture Guide](../../relational-databases/query-processing-architecture-guide.md)   (Guía de arquitectura de procesamiento de consultas)  
[Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Combinaciones](../../relational-databases/performance/joins.md)    
[Demostración del procesamiento de consultas adaptable](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)        
