---
title: sys.query_store_runtime_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ba19045d0184e498b559da0b97b3cd4d95d30c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067927"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contiene información sobre la información de estadísticas de ejecución en tiempo de ejecución para la consulta.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|Identificador de la fila que representa las estadísticas de ejecución en tiempo de ejecución el **plan_id**, **execution_type** y **runtime_stats_interval_id**. Es único solo para los últimos intervalos de estadísticas en tiempo de ejecución. Intervalo activo puede haber varias filas que representa las estadísticas de tiempo de ejecución para el plan al que hace referencia **plan_id**, con el tipo de ejecución representado por **execution_type**. Normalmente, una fila representa las estadísticas de tiempo de ejecución que se vacían en disco, mientras que otros (s) representan el estado en memoria. Por lo tanto, para obtener el estado real para cada intervalo deberá métricas agregadas, agrupando **plan_id**, **execution_type** y **runtime_stats_interval_id**.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**plan_id**|**bigint**|Clave externa. Se une a [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Clave externa. Se une a [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Determina el tipo de ejecución de la consulta:<br /><br /> 0 - ejecución normal (finalizada correctamente)<br /><br /> 3 - cliente iniciada anulada ejecución<br /><br /> 4 - excepción anula la ejecución|  
|**execution_type_desc**|**nvarchar(128)**|Descripción textual del campo de tipo de ejecución:<br /><br /> 0 - normal<br /><br /> 3: anulada<br /><br /> 4 - excepción|  
|**first_execution_time**|**datetimeoffset**|Primera hora de ejecución del plan de consulta dentro del intervalo de agregación. Se refiere a la hora de finalización de la ejecución de consultas.|  
|**last_execution_time**|**datetimeoffset**|Planee la última hora de ejecución para la consulta dentro del intervalo de agregación. Se refiere a la hora de finalización de la ejecución de consultas.|  
|**count_executions**|**bigint**|Recuento total de ejecuciones del plan de consulta dentro del intervalo de agregación.|  
|**avg_duration**|**float**|Promedio de duración para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**last_duration**|**bigint**|Planee la última duración de la consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**min_duration**|**bigint**|Duración mínima para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**max_duration**|**bigint**|Duración máxima para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**stdev_duration**|**float**|Desviación estándar de duración para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).|  
|**avg_cpu_time**|**float**|Promedio de tiempo de CPU para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_cpu_time**|**bigint**|Último tiempo de CPU de la consulta plan dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_cpu_time**|**bigint**|Tiempo de CPU mínimo para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_cpu_time**|**bigint**|Tiempo de CPU máximo para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**stdev_cpu_time**|**float**|Desviación de estándar de tiempo de CPU para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**avg_logical_io_reads**|**float**|Número promedio de E/S lógicas lee del plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_logical_io_reads**|**bigint**|Último número de E/S lógicas lee del plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_logical_io_reads**|**bigint**|Lee el número mínimo de E/S lógicas para el plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_logical_io_reads**|**bigint**|Lee el número máximo de E/S lógicas para el plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**stdev_logical_io_reads**|**float**|Número de E/S lógicas lee la desviación estándar para el plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**avg_logical_io_writes**|**float**|Número promedio de E/S lógicas se escribe para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_logical_io_writes**|**bigint**|Escribe en el último número de E/S lógicas para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_logical_io_writes**|**bigint**|Número mínimo de E/S lógicas se escribe para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_logical_io_writes**|**bigint**|Número máximo de E/S lógicas se escribe para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**stdev_logical_io_writes**|**float**|Número de E/S lógicas escribe la desviación estándar para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**avg_physical_io_reads**|**float**|Lee el número promedio de E/S física para el plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_physical_io_reads**|**bigint**|Último número de E/S física se lee del plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_physical_io_reads**|**bigint**|Lee el número mínimo de E/S física para el plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_physical_io_reads**|**bigint**|Lee el número máximo de E/S física para el plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**stdev_physical_io_reads**|**float**|Número de E/S física lee la desviación estándar para el plan de consulta dentro del intervalo de agregación (expresado como un número de páginas de 8KB de lectura).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**avg_clr_time**|**float**|Promedio de tiempo de CLR para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_clr_time**|**bigint**|Planee la última hora CLR de la consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_clr_time**|**bigint**|Tiempo mínimo de CLR para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_clr_time**|**bigint**|Tiempo máximo de CLR para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**stdev_clr_time**|**float**|CLR la desviación estándar de tiempo para el plan de consulta dentro del intervalo de agregación (notificado en microsegundos).<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**avg_dop**|**float**|Promedio DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_dop**|**bigint**|Último DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_dop**|**bigint**|Mínimo DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_dop**|**bigint**|Máximo DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**stdev_dop**|**float**|Desviación estándar DOP (grado de paralelismo) para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**avg_query_max_used_memory**|**float**|Concesión de memoria promedio (identificado como el número de páginas de 8 KB) para el plan de consulta dentro del intervalo de agregación. Siempre en 0 para las consultas que utilizan de forma nativa se compilan procedimientos con optimización para memoria.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_query_max_used_memory**|**bigint**|Última concesión de memoria (identificado como el número de páginas de 8 KB) para el plan de consulta dentro del intervalo de agregación. Siempre en 0 para las consultas que utilizan de forma nativa se compilan procedimientos con optimización para memoria.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_query_max_used_memory**|**bigint**|Concesión de memoria mínima (identificado como el número de páginas de 8 KB) para el plan de consulta dentro del intervalo de agregación. Siempre en 0 para las consultas que utilizan de forma nativa se compilan procedimientos con optimización para memoria.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_query_max_used_memory**|**bigint**|Concesión de memoria máxima (identificado como el número de páginas de 8 KB) para el plan de consulta dentro del intervalo de agregación. Siempre en 0 para las consultas que utilizan de forma nativa se compilan procedimientos con optimización para memoria.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**stdev_query_max_used_memory**|**float**|Desviación estándar (identificado como el número de páginas de 8 KB) de concesión de memoria para el plan de consulta dentro del intervalo de agregación. Siempre en 0 para las consultas que utilizan de forma nativa se compilan procedimientos con optimización para memoria.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**avg_rowcount**|**float**|Número promedio de filas devueltas para el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_rowcount**|**bigint**|Número de filas devueltas por la última ejecución del plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_rowcount**|**bigint**|Planee el número mínimo de filas devueltas de la consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_rowcount**|**bigint**|Planee el número máximo de filas devueltas de la consulta dentro del intervalo de agregación.|  
|**stdev_rowcount**|**float**|Número de filas devueltas de desviación del plan de consulta dentro del intervalo de agregación.|
|**avg_log_bytes_used**|**float**|Número promedio de bytes en el registro de base de datos utilizado el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**last_log_bytes_used**|**bigint**|Número de bytes en el registro de base de datos utilizado por la última ejecución del plan de consulta, en el intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**min_log_bytes_used**|**bigint**|Número mínimo de bytes en el registro de base de datos utilizado el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**max_log_bytes_used**|**bigint**|Número máximo de bytes en el registro de base de datos utilizado el plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|
|**stdev_log_bytes_used**|**float**|Desviación estándar del número de bytes en el registro de base de datos utilizado por un plan de consulta dentro del intervalo de agregación.<br/>**Nota:** Azure SQL Data Warehouse siempre devolverá cero (0).|  
|**avg_page_server_io_reads**|**float**|Número medio de la página de lecturas de E/S de servidor para el plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br><br/>**Nota:** Se aplica a: Base de datos SQL Azure a gran escala</br> Azure SQL Data Warehouse, Azure SQL DB, MI (que no sean de hiperescala) siempre devolverá cero (0).|
|**last_page_server_io_reads**|**bigint**|Último número de E/S de servidor de página se lee del plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br><br/>**Nota:** Se aplica a: Base de datos SQL Azure a gran escala </br> Azure SQL Data Warehouse, Azure SQL DB, MI (que no sean de hiperescala) siempre devolverá cero (0).|
|**min_page_server_io_reads**|**bigint**|Número mínimo de la página de lecturas de E/S de servidor para el plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br><br/>**Nota:** Se aplica a: Base de datos SQL Azure a gran escala </br> Azure SQL Data Warehouse, Azure SQL DB, MI (que no sean de hiperescala) siempre devolverá cero (0).|
|**max_page_server_io_reads**|**bigint**|Número máximo de página lecturas de E/S de servidor para el plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br><br/>**Nota:** Se aplica a: Base de datos SQL Azure a gran escala </br> Azure SQL Data Warehouse, Azure SQL DB, MI (que no sean de hiperescala) siempre devolverá cero (0).|
|**stdev_page_server_io_reads**|**float**|Número de página servidor E/S lee la desviación estándar para el plan de consulta dentro del intervalo de agregación. (expresado como un número de páginas de 8KB de lectura).<br><br/>**Nota:** Se aplica a: Base de datos SQL Azure a gran escala </br> Azure SQL Data Warehouse, Azure SQL DB, MI (que no sean de hiperescala) siempre devolverá cero (0).|
  
## <a name="permissions"></a>Permisos  
 Requiere el **VIEW DATABASE STATE** permiso.  
  
## <a name="see-also"></a>Vea también  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimientos almacenados de Query Store &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
