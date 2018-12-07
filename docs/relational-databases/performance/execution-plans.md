---
title: Planes de ejecución | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 9bf75c2d176c4ea2c596f29f1ddda910e794ae12
ms.sourcegitcommit: ba7fb4b9b4f0dbfe77a7c6906a1fde574e5a8e1e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303238"
---
# <a name="execution-plans"></a>Planes de ejecución
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Para poder ejecutar consultas, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] debe analizar la instrucción para determinar la manera más eficaz para tener acceso a los datos necesarios. Este análisis se controla mediante un componente denominado Optimizador de consultas. La entrada al Optimizador de consultas consta de la consulta, el esquema de la base de datos (definiciones de tabla e índice) y las estadísticas de base de datos. La salida del Optimizador de consultas es un plan de ejecución de consultas, en ocasiones denominado plan de consulta o simplemente plan de ejecución.   

Un plan de ejecución de consulta es una definición de los siguientes elementos: 

* La secuencia en la que se tiene acceso a las tablas de origen.  
  Normalmente, hay muchas secuencias diferentes en las que el servidor de la base de datos puede tener acceso a las tablas base para generar el conjunto de resultados. Por ejemplo, si una instrucción `SELECT` hace referencia a tres tablas, el servidor de la base de datos podría tener acceso primero a `TableA`, utilizar los datos de `TableA` para extraer las filas que coincidan con las de `TableB`y, finalmente, utilizar los datos de `TableB` para extraer datos de `TableC`. Las demás secuencias en las que el servidor de base de datos podría tener acceso a las tablas son:  
  `TableC`, `TableB`, `TableA`o  
  `TableB`, `TableA`, `TableC`o  
  `TableB`, `TableC`, `TableA`o  
  `TableC`, `TableA`, `TableB`  

* Los métodos que se utilizan para extraer los datos de cada tabla.  
  Por lo general, hay métodos diferentes para tener acceso a los datos de cada tabla. Si solo se necesitan unas cuantas filas con valores de clave específicos, el servidor de la base de datos puede utilizar un índice. Si se necesitan todas las filas de una tabla, el servidor de la base de datos puede omitir los índices y realizar un recorrido de la tabla. Si se necesitan todas las filas de la tabla, pero hay un índice cuyas columnas de clave están ordenadas con `ORDER BY`, realizar un recorrido del índice en lugar de un recorrido de la tabla puede evitar otra ordenación del conjunto de resultados. Si la tabla es muy pequeña, el recorrido de la misma puede ser el método más eficaz para la mayoría de los accesos a la tabla.

> [!TIP]
> Para obtener más información sobre los planes de ejecución y procesamiento de consultas, vea la [Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md).

## <a name="in-this-section"></a>En esta sección  
  
-   [Query Profiling Infrastructure](../../relational-databases/performance/query-profiling-infrastructure.md) (Infraestructura de generación de perfiles de consultas)  
  
-   [Mostrar y guardar planes de ejecución](../../relational-databases/performance/display-and-save-execution-plans.md)  
  
-   [Comparación y análisis de los planes de ejecución](../../relational-databases/performance/compare-and-analyze-execution-plans.md)  

-   [Guías de plan](../../relational-databases/performance/plan-guides.md)  

## <a name="see-also"></a>Ver también  
 [Supervisar y optimizar el rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Herramientas de supervisión y optimización del rendimiento](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Query Processing Architecture Guide](../../relational-databases/query-processing-architecture-guide.md)   (Guía de arquitectura de procesamiento de consultas)  
 [Estadísticas de consultas activas](../../relational-databases/performance/live-query-statistics.md)     
 [Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md)     
 [Supervisión del rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
