---
title: Sys.query_store_runtime_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8cf026cb9beff10c6570a94bdd805aa2b78c0a4d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>Sys.query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contiene información sobre la información de estadísticas de ejecución en tiempo de ejecución para la consulta.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|Identificador de la fila que representa las estadísticas de ejecución en tiempo de ejecución para la **plan_id**, **execution_type** y **runtime_stats_interval_id**. Es único solo para los intervalos de estadísticas en tiempo de ejecución anteriores. Para intervalo actualmente activo puede haber varias filas que representa las estadísticas de tiempo de ejecución para el plan al que hace referencia **plan_id**, con el tipo de ejecución representado por **execution_type**. Normalmente, una fila representa las estadísticas de tiempo de ejecución que se vacían en el disco, mientras que otras (s) representan el estado en memoria. Por tanto, para obtener el estado real para cada intervalo deberá métricas agregadas, agrupando **plan_id**, **execution_type** y **runtime_stats_interval_id**. |  
|**plan_id**|**bigint**|Clave externa. Se combina con [sys.query_store_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Clave externa. Se combina con [sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Determina el tipo de ejecución de consulta:<br /><br /> 0 – normal de ejecución (terminado correctamente)<br /><br /> 3-cliente iniciado anuló la ejecución<br /><br /> 4 - excepción anuló la ejecución|  
|**execution_type_desc**|**nvarchar (128)**|Descripción textual del campo de tipo de ejecución:<br /><br /> 0 – normal<br /><br /> 3 – anuladas<br /><br /> 4 - excepción|  
|**first_execution_time**|**datetimeoffset**|Primer tiempo de ejecución para el plan de consulta dentro del intervalo de agregación.|  
|**last_execution_time**|**datetimeoffset**|Planear la última hora de ejecución de la consulta dentro del intervalo de agregación.|  
|**count_executions**|**bigint**|Recuento total de ejecuciones del plan de consulta dentro del intervalo de agregación.|  
|**avg_duration**|**float**|Promedio de duración del plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**last_duration**|**bigint**|Planear la última duración de la consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**min_duration**|**bigint**|Duración mínima para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**max_duration**|**bigint**|Duración máxima para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**stdev_duration**|**float**|Desviación estándar de duración para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**avg_cpu_time**|**float**|Promedio de tiempo de CPU para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**last_cpu_time**|**bigint**|Último tiempo de CPU de la consulta planear dentro del intervalo de agregación (notificado en microsegundos).|  
|**min_cpu_time**|**bigint**|Tiempo mínimo de CPU para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**max_cpu_time**|**bigint**|Tiempo de CPU máximo para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**stdev_cpu_time**|**float**|Desviación de estándar de tiempo de CPU para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**avg_logical_io_reads**|**float**|Número promedio de E/S lógicas lee del plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).|  
|**last_logical_io_reads**|**bigint**|Último número de operaciones de E/S lógicas lee del plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).|  
|**min_logical_io_reads**|**bigint**|Número mínimo de E/S lógicas lee del plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).|  
|**max_logical_io_reads**|**bigint**|Número máximo de operaciones de E/S lógicas lee del plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura). |  
|**stdev_logical_io_reads**|**float**|Número de operaciones de E/S lógicas lee la desviación estándar para el plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).|  
|**avg_logical_io_writes**|**float**|Número promedio de E/S lógicas se escribe para el plan de consulta dentro del intervalo de agregación.|  
|**last_logical_io_writes**|**bigint**|Último número de operaciones de E/S lógicas se escribe para el plan de consulta dentro del intervalo de agregación.|  
|**min_logical_io_writes**|**bigint**|Número mínimo de E/S lógicas se escribe para el plan de consulta dentro del intervalo de agregación.|  
|**max_logical_io_writes**|**bigint**|Número máximo de operaciones de E/S lógicas se escribe para el plan de consulta dentro del intervalo de agregación.|  
|**stdev_logical_io_writes**|**float**|Número de operaciones de E/S lógicas escribe desviación estándar para el plan de consulta dentro del intervalo de agregación.|  
|**avg_physical_io_reads**|**float**|Número promedio de E/S física lee del plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).|  
|**last_physical_io_reads**|**bigint**|Último número de E/S física lee del plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).|  
|**min_physical_io_reads**|**bigint**|Número mínimo de E/S física lee del plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).|  
|**max_physical_io_reads**|**bigint**|Lee el número máximo de E/S física para el plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).|  
|**stdev_physical_io_reads**|**float**|Número de E/S física lee la desviación estándar para el plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).|  
|**avg_clr_time**|**float**|Tiempo medio de CLR para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**last_clr_time**|**bigint**|Planear la última hora de CLR de la consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**min_clr_time**|**bigint**|Tiempo mínimo de CLR para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**max_clr_time**|**bigint**|Tiempo máximo de CLR para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**stdev_clr_time**|**float**|CLR la desviación estándar de tiempo para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**avg_dop**|**float**|Promedio DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.|  
|**last_dop**|**bigint**|Últimos DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.|  
|**min_dop**|**bigint**|Mínimo DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.|  
|**MAX_DOP**|**bigint**|Máximo DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.|  
|**stdev_dop**|**float**|Desviación estándar DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.|  
|**avg_query_max_used_memory**|**float**|Concesión de memoria promedio (indicado que el número de páginas de 8 KB) para el plan de consulta dentro del intervalo de agregación. Siempre es 0 para las consultas que utilizan de forma nativa los con optimización para memoria procedimientos compilados.|  
|**last_query_max_used_memory**|**bigint**|Última concesión de memoria (indicado que el número de páginas de 8 KB) para el plan de consulta dentro del intervalo de agregación. Siempre es 0 para las consultas que utilizan de forma nativa los con optimización para memoria procedimientos compilados.|  
|**min_query_max_used_memory**|**bigint**|Concesión de memoria mínima (indicado que el número de páginas de 8 KB) para el plan de consulta dentro del intervalo de agregación. Siempre es 0 para las consultas que utilizan de forma nativa los con optimización para memoria procedimientos compilados.|  
|**max_query_max_used_memory**|**bigint**|Concesión de memoria máxima (indicado que el número de páginas de 8 KB) para el plan de consulta dentro del intervalo de agregación. Siempre es 0 para las consultas que utilizan de forma nativa los con optimización para memoria procedimientos compilados.|  
|**stdev_query_max_used_memory**|**float**|Desviación estándar (indica que el número de páginas de 8 KB) de concesión de memoria para el plan de consulta dentro del intervalo de agregación. Siempre es 0 para las consultas que utilizan de forma nativa los con optimización para memoria procedimientos compilados.|  
|**avg_rowcount**|**float**|Número promedio de filas devueltas para el plan de consulta dentro del intervalo de agregación.|  
|**last_rowcount**|**bigint**|Número de filas devueltas por la última ejecución del plan de consulta dentro del intervalo de agregación.|  
|**min_rowcount**|**bigint**|Número mínimo de filas devueltas de la consulta planear dentro del intervalo de agregación.|  
|**max_rowcount**|**bigint**|Número máximo de filas devueltas de la consulta planear dentro del intervalo de agregación.|  
|**stdev_rowcount**|**float**|Número de desviación estándar de filas devueltas para el plan de consulta dentro del intervalo de agregación.|
|**avg_log_bytes_used**|**float**|Número promedio de bytes en el registro de base de datos utilizado por el plan de consulta dentro del intervalo de agregación. Se aplica **sólo a la base de datos SQL Azure**.|    
|**last_log_bytes_used**|**bigint**|Número de bytes en el registro de base de datos utilizado por la última ejecución del plan de consulta, dentro del intervalo de agregación. Se aplica **sólo a la base de datos SQL Azure**.|  
|**min_log_bytes_used**|**bigint**|Número mínimo de bytes en el registro de base de datos utilizado por el plan de consulta dentro del intervalo de agregación.  Se aplica **sólo a la base de datos SQL Azure**.|  
|**max_log_bytes_used**|**bigint**|Número máximo de bytes en el registro de base de datos utilizado por el plan de consulta dentro del intervalo de agregación.  Se aplica **sólo a la base de datos SQL Azure**.| 
|**stdev_log_bytes_used**|**float**|Desviación estándar del número de bytes en el registro de base de datos utilizado por un plan de consulta dentro del intervalo de agregación.  Se aplica **sólo a la base de datos SQL Azure**.|
  
## <a name="permissions"></a>Permissions  
 Requiere la **VIEW DATABASE STATE** permiso.  
  
## <a name="see-also"></a>Vea también  
 [Sys.database_query_store_options &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Sys.query_context_settings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [Sys.query_store_plan &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [Sys.query_store_query &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [Sys.query_store_query_text &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Supervisar el rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Almacén de consultas almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
