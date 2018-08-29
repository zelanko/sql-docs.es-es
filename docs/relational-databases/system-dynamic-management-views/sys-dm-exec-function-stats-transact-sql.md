---
title: Sys.dm_exec_function_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8f49103e888ecd856edfd1e467011ba96e5c998d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43066138"
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>Sys.dm_exec_function_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Devuelve estadísticas de rendimiento para las funciones en caché agregado. La vista devuelve una fila por cada plan de función almacenado en caché, y la duración de la fila está siempre y cuando la función permanece en caché. Cuando se quita una función de la memoria caché, se elimina la fila correspondiente de esta vista. En ese momento, se produce un evento de seguimiento de SQL de estadísticas de rendimiento similar a **sys.dm_exec_query_stats**. Devuelve información acerca de las funciones escalares, incluidas las funciones de en memoria y las funciones escalares de CLR. No se devuelve información acerca de las funciones con valores de tabla.  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, cada fila que contiene datos que no pertenecen al inquilino conectado se filtra.  
  
> [!NOTE]
> Una consulta inicial de **sys.dm_exec_function_stats** podría producir resultados imprecisos si hay una carga de trabajo ejecutándose actualmente en el servidor. Pueden determinarse resultados más precisos volviendo a ejecutar la consulta.  
  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Id. de base de datos en el que reside la función.|  
|**object_id**|**int**|Número de identificación de objeto de la función.|  
|**Tipo**|**char(2)**|Tipo del objeto: FN = funciones con valores escalares|  
|**type_desc**|**nvarchar(60)**|Descripción del tipo de objeto: SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary (64)**|Esto puede usarse para poner en correlación con las consultas en **sys.dm_exec_query_stats** que se ejecutaron desde dentro de esta función.|  
|**plan_handle**|**varbinary (64)**|Identificador del plan en memoria. Este identificador es transitorio y permanece constante solo mientras el plan permanece en la memoria caché. Este valor se puede usar con el **sys.dm_exec_cached_plans** vista de administración dinámica.<br /><br /> Siempre será 0 x 000 cuando una tabla de consultas optimizadas en memoria de la función compilada de forma nativa.|  
|**cached_time**|**datetime**|Hora en que se agregó la función a la memoria caché.|  
|**last_execution_time**|**datetime**|Última hora en que se ejecutó la función.|  
|**execution_count**|**bigint**|Número de veces que la función se ha ejecutado desde que se compiló por última vez.|  
|**total_worker_time**|**bigint**|Cantidad total de tiempo de CPU, en microsegundos, consumido por las ejecuciones de esta función desde que se compiló.<br /><br /> Para las funciones compiladas de forma nativa, **total_worker_time** puede no ser exacto si varias ejecuciones tardan menos de 1 milisegundo.|  
|**last_worker_time**|**bigint**|Tiempo de CPU, en microsegundos, consumido la última vez que se ejecutó la función. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Tiempo mínimo de CPU, en microsegundos, hasta que esta función se ha consumido alguna vez durante una ejecución. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Tiempo máximo de CPU, en microsegundos, hasta que esta función se ha consumido alguna vez durante una ejecución. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|Número total de lecturas físicas realizadas por las ejecuciones de esta función desde que se compiló.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**last_physical_reads**|**bigint**|Número de lecturas físicas realizadas la última vez que se ejecutó la función.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**min_physical_reads**|**bigint**|Número mínimo de lecturas físicas que ha realizado durante una ejecución de esta función.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**max_physical_reads**|**bigint**|Número máximo de lecturas físicas que ha realizado durante una ejecución de esta función.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**total_logical_writes**|**bigint**|Número total de escrituras lógicas realizadas por las ejecuciones de esta función desde que se compiló.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**last_logical_writes**|**bigint**|Número de páginas del grupo de búferes desfasadas la última vez que se ejecutó el plan. Si una página ya está desfasada (modificada) no se cuenta ninguna escritura.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**min_logical_writes**|**bigint**|Número mínimo de escrituras lógicas que ha realizado durante una ejecución de esta función.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**max_logical_writes**|**bigint**|Número máximo de escrituras lógicas que ha realizado durante una ejecución de esta función.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**total_logical_reads**|**bigint**|Número total de lecturas lógicas realizadas por las ejecuciones de esta función desde que se compiló.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**last_logical_reads**|**bigint**|Número de lecturas lógicas realizadas la última vez que se ejecutó la función.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**min_logical_reads**|**bigint**|Número mínimo de lecturas lógicas que ha realizado durante una ejecución de esta función.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**max_logical_reads**|**bigint**|Número máximo de lecturas lógicas que ha realizado durante una ejecución de esta función.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**total_elapsed_time**|**bigint**|Tiempo total transcurrido, en microsegundos para las ejecuciones completadas de esta función.|  
|**last_elapsed_time**|**bigint**|Tiempo transcurrido, en microsegundos, hasta la ejecución completada más recientemente de esta función.|  
|**min_elapsed_time**|**bigint**|Tiempo mínimo transcurrido, en microsegundos, hasta cualquier completado la ejecución de esta función.|  
|**max_elapsed_time**|**bigint**|Tiempo máximo transcurrido, en microsegundos, hasta cualquier completado la ejecución de esta función.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve información acerca de las funciones principales de diez identificado por promedio de tiempo transcurrido.  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
