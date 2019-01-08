---
title: Sys.query_store_query (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_QUERY
- SYS.QUERY_STORE_QUERY_TSQL
- SYS.QUERY_STORE_QUERY
- QUERY_STORE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_query catalog view
- sys.query_store_query catalog view
ms.assetid: bdee149e-7556-4fc3-8242-925dd4b7b6ac
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ff4b428c87da7180869cb3b0c51f4a8fb118a351
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2018
ms.locfileid: "52711856"
---
# <a name="sysquerystorequery-transact-sql"></a>Sys.query_store_query (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contiene información acerca de la consulta y sus estadísticas de ejecución en tiempo de ejecución agregados asociados total.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|Clave principal.|  
|**query_text_id**|**bigint**|Clave externa. Se une a [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|Clave externa. Se une a [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md).|  
|**object_id**|**bigint**|Identificador del objeto de base de datos que forma parte de la consulta (procedimiento almacenado, desencadenador, UDF de CLR/UDAgg, etcetera.). 0 si no se ejecuta la consulta como parte de un objeto de base de datos (consulta ad hoc).|  
|**batch_sql_handle**|**varbinary (64)**|Id. del lote de instrucciones de la consulta forma parte de. Rellena solo si la consulta hace referencia a tablas temporales o variables de tabla.|  
|**query_hash**|**binary (8)**|Hash MD5 de la consulta individual, basándose en el árbol de consulta lógica. Incluye las sugerencias del optimizador.|  
|**is_internal_query**|**bit**|La consulta se ha generado internamente.|  
|**query_parameterization_type**|**tinyint**|Tipo de parametrización:<br /><br /> 0: ninguno<br /><br /> 1 - usuario<br /><br /> 2 - simple<br /><br /> 3 - forzada|  
|**query_parameterization_type_desc**|**nvarchar(60)**|Descripción textual del tipo de parametrización.|  
|**initial_compile_start_time**|**datetimeoffset**|Compile la hora de inicio.|  
|**last_compile_start_time**|**datetimeoffset**|Compile la hora de inicio.|  
|**last_execution_time**|**datetimeoffset**|Último tiempo de ejecución hace referencia a la última hora de finalización del plan de consulta.|  
|**last_compile_batch_sql_handle**|**varbinary (64)**|Identificador del último lote SQL en el que consulta se usó la última vez. Se puede proporcionar como entrada para [sys.dm_exec_sql_text &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) para obtener el texto del lote completo.|  
|**last_compile_batch_offset_start**|**bigint**|Información que puede proporcionarse a sys.dm_exec_sql_text junto con last_compile_batch_sql_handle.|  
|**last_compile_batch_offset_end**|**bigint**|Información que puede proporcionarse a sys.dm_exec_sql_text junto con last_compile_batch_sql_handle.|  
|**count_compiles**|**bigint**|Estadísticas de compilación.|  
|**avg_compile_duration**|**float**|Estadísticas de compilación en microsegundos.|  
|**last_compile_duration**|**bigint**|Estadísticas de compilación en microsegundos.|  
|**avg_bind_duration**|**float**|Estadísticas de enlace en microsegundos.|  
|**last_bind_duration**|**bigint**|Estadísticas de enlace.|  
|**avg_bind_cpu_time**|**float**|Estadísticas de enlace.|  
|**last_bind_cpu_time**|**bigint**|Estadísticas de enlace.|  
|**avg_optimize_duration**|**float**|Estadísticas de optimización en microsegundos.|  
|**last_optimize_duration**|**bigint**|Estadísticas de optimización.|  
|**avg_optimize_cpu_time**|**float**|Estadísticas de optimización en microsegundos.|  
|**last_optimize_cpu_time**|**bigint**|Estadísticas de optimización.|  
|**avg_compile_memory_kb**|**float**|Recopilar estadísticas de memoria.|  
|**last_compile_memory_kb**|**bigint**|Recopilar estadísticas de memoria.|  
|**max_compile_memory_kb**|**bigint**|Recopilar estadísticas de memoria.|  
|**is_clouddb_internal_query**|**bit**|Siempre es 0 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el entorno local.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el **VIEW DATABASE STATE** permiso.  
  
## <a name="see-also"></a>Vea también  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del Almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
