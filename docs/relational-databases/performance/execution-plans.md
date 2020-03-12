---
title: Planes de ejecución | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- execution plan [SQL Server]
- query plan [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 81a9f0e52c061ec494143eb4f61158546f5e57f9
ms.sourcegitcommit: 58c25f47cfd701c61022a0adfc012e6afb9ce6e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/03/2020
ms.locfileid: "78256953"
---
# <a name="execution-plans"></a>Planes de ejecución
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Para poder ejecutar consultas, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] debe analizar la instrucción para determinar la manera más eficaz para tener acceso a los datos necesarios. Este análisis se controla mediante un componente denominado Optimizador de consultas. La entrada al Optimizador de consultas consta de la consulta, el esquema de la base de datos (definiciones de tabla e índice) y las estadísticas de base de datos. La salida del Optimizador de consultas es un plan de ejecución de consultas, en ocasiones denominado plan de consulta o simplemente plan de ejecución.   

Un plan de ejecución de consulta es una definición de los siguientes elementos: 

- **La secuencia en la que se tiene acceso a las tablas de origen.**  
  Normalmente, hay muchas secuencias diferentes en las que el servidor de la base de datos puede tener acceso a las tablas base para generar el conjunto de resultados. Por ejemplo, si una instrucción `SELECT` hace referencia a tres tablas, el servidor de la base de datos podría tener acceso primero a `TableA`, utilizar los datos de `TableA` para extraer las filas que coincidan con las de `TableB`y, finalmente, utilizar los datos de `TableB` para extraer datos de `TableC`. Las demás secuencias en las que el servidor de base de datos podría tener acceso a las tablas son:  
  `TableC`, `TableB`, `TableA`o  
  `TableB`, `TableA`, `TableC`o  
  `TableB`, `TableC`, `TableA`o  
  `TableC`, `TableA`, `TableB`  

- **Los métodos que se usan para extraer los datos de cada tabla.**  
  Por lo general, hay métodos diferentes para tener acceso a los datos de cada tabla. Si solo se necesitan unas cuantas filas con valores de clave específicos, el servidor de la base de datos puede utilizar un índice. Si se necesitan todas las filas de una tabla, el servidor de la base de datos puede omitir los índices y realizar un recorrido de la tabla. Si se necesitan todas las filas de la tabla, pero hay un índice cuyas columnas de clave están ordenadas con `ORDER BY`, realizar un recorrido del índice en lugar de un recorrido de la tabla puede evitar otra ordenación del conjunto de resultados. Si la tabla es muy pequeña, el recorrido de la misma puede ser el método más eficaz para la mayoría de los accesos a la tabla.
  
- **Los métodos que se usan para realizar cálculos, y cómo filtrar, agregar y ordenar los datos de cada tabla.**  
  A medida que se tiene acceso a los datos desde las tablas, existen distintos métodos para realizar cálculos sobre ellos (por ejemplo, calcular valores escalares), para agregarlos y ordenarlos tal como se define en el texto de la consulta, por ejemplo, cuando se usa una cláusula `GROUP BY` o `ORDER BY`, y cómo filtrarlos, por ejemplo, cuando se usa una cláusula `WHERE` o `HAVING`.

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tiene tres opciones para mostrar los planes de ejecución:        
> -  El ***[plan de ejecución estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md)***, que es el plan compilado, generado por el optimizador de consultas en función de las estimaciones.        
> -  El ***[plan de ejecución real](../../relational-databases/performance/display-an-actual-execution-plan.md)***, que es el mismo que el plan compilado más su [contexto de ejecución](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse). Esto incluye la información del entorno de ejecución real disponible una vez completada la ejecución, como advertencias de ejecución o, en versiones más recientes del [!INCLUDE[ssde_md](../../includes/ssde_md.md)], el tiempo transcurrido y el tiempo de CPU usado durante la ejecución.        
> -  Las ***[Estadísticas de consulta activa](../../relational-databases/performance/live-query-statistics.md)***, que es lo mismo que el plan compilado más su contexto de ejecución. Esto incluye información en tiempo de ejecución durante el progreso de la ejecución y se actualiza cada segundo. La información en tiempo de ejecución incluye, por ejemplo, el número real de filas que fluyen a través de los operadores.       

> [!TIP]
> Para más información sobre el procesamiento de consultas y los planes de ejecución de consultas, consulte las secciones [Optimización de las instrucciones SELECT](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements) y [Almacenar en caché y volver a utilizar un plan de ejecución](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse) de la Guía de arquitectura de procesamiento de consultas.

## <a name="in-this-section"></a>En esta sección  
[Infraestructura de generación de perfiles de consultas](../../relational-databases/performance/query-profiling-infrastructure.md)     
[Mostrar y guardar planes de ejecución](../../relational-databases/performance/display-and-save-execution-plans.md)     
[Comparación y análisis de los planes de ejecución](../../relational-databases/performance/compare-and-analyze-execution-plans.md)     
[Guías de plan](../../relational-databases/performance/plan-guides.md)     

## <a name="see-also"></a>Consulte también  
[Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
[Herramientas de supervisión y optimización del rendimiento](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
[Query Processing Architecture Guide](../../relational-databases/query-processing-architecture-guide.md)   (Guía de arquitectura de procesamiento de consultas)  
[Estadísticas de consultas activas](../../relational-databases/performance/live-query-statistics.md)     
[Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md)     
[Supervisión del rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
[sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
[Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
[Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
