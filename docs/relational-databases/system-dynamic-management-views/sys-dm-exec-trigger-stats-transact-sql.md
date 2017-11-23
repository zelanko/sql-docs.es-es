---
title: Sys.dm_exec_trigger_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67c6d5765ee5259134f6d9985a88bf94768490cf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve estadísticas de rendimiento de agregado para los desencadenadores en memoria caché. La vista contiene una fila por cada desencadenador y la duración de la fila corresponde al tiempo que el desencadenador permanece en memoria caché. Cuando se quita un desencadenador de la memoria caché, la fila correspondiente se elimina de esta vista. En ese momento, se provoca un evento de seguimiento de SQL de estadísticas de rendimiento similar a **sys.dm_exec_query_stats**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Identificador de base de datos en que reside el desencadenador.|  
|**object_id**|**int**|Número de identificación del objeto del desencadenador.|  
|**tipo**|**Char(2)**|Tipo del objeto:<br /><br /> TA = Desencadenador de ensamblado (CLR)<br /><br /> TR = Desencadenador SQL|  
|**Type_desc**|**nvarchar (60)**|Descripción del tipo de objeto:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|Esto puede usarse para poner en correlación con las consultas en **sys.dm_exec_query_stats** que se ejecutaron desde dentro de este desencadenador.|  
|**plan_handle**|**varbinary(64)**|Identificador del plan en memoria. Este identificador es transitorio y permanece constante solo mientras el plan permanece en la memoria caché. Este valor se puede usar con el **sys.dm_exec_cached_plans** vista de administración dinámica.|  
|**cached_time**|**datetime**|Momento en que el desencadenador se agregó a la caché.|  
|**last_execution_time**|**datetime**|Última vez que se ejecutó el desencadenador vez.|  
|**entre execution_count**|**bigint**|Número de veces que se ha ejecutado el desencadenador desde que se compiló por última vez.|  
|**total_worker_time**|**bigint**|Tiempo total de CPU, en microsegundos, consumido por las ejecuciones de este desencadenador desde que se compiló.|  
|**last_worker_time**|**bigint**|Tiempo de CPU, en microsegundos, consumido la última vez que se ejecutó el desencadenador.|  
|**min_worker_time**|**bigint**|Tiempo máximo de CPU, en microsegundos, consumido por este desencadenador durante una ejecución.|  
|**max_worker_time**|**bigint**|Tiempo máximo de CPU, en microsegundos, consumido por este desencadenador durante una ejecución.|  
|**número**|**bigint**|Número total de lecturas físicas realizadas por las ejecuciones de este desencadenador desde que se compiló.|  
|**last_physical_reads**|**bigint**|Número de lecturas físicas realizadas la última vez que se ejecutó el desencadenador.|  
|**min_physical_reads**|**bigint**|Número mínimo de lecturas físicas realizadas por este desencadenador durante una ejecución.|  
|**max_physical_reads**|**bigint**|Número máximo de lecturas físicas realizadas por este desencadenador durante una ejecución.|  
|**total_logical_writes**|**bigint**|Número total de escrituras lógicas realizadas por las ejecuciones de este desencadenador desde que se compiló.|  
|**last_logical_writes**|**bigint**|**número**número de escrituras lógicas realizadas la última vez que se ejecutó el desencadenador.|  
|**min_logical_writes**|**bigint**|Número mínimo de escrituras lógicas realizadas por este desencadenador durante una ejecución.|  
|**max_logical_writes**|**bigint**|Número máximo de escrituras lógicas realizadas por este desencadenador durante una ejecución.|  
|**total_logical_reads**|**bigint**|Número total de lecturas lógicas realizadas por las ejecuciones de este desencadenador desde que se compiló.|  
|**last_logical_reads**|**bigint**|Número de lecturas lógicas realizadas la última vez que se ejecutó el desencadenador.|  
|**min_logical_reads**|**bigint**|Número mínimo de lecturas lógicas realizadas por este desencadenador durante una ejecución.|  
|**max_logical_reads**|**bigint**|Número máximo de lecturas lógicas realizadas por este desencadenador durante una ejecución.|  
|**total_elapsed_time**|**bigint**|Tiempo total transcurrido, en microsegundos, hasta la finalización de las ejecuciones de este desencadenador.|  
|**last_elapsed_time**|**bigint**|Tiempo transcurrido, en microsegundos, hasta la finalización de la ejecución más reciente de este desencadenador.|  
|**min_elapsed_time**|**bigint**|Tiempo mínimo transcurrido, en microsegundos, hasta la finalización de cualquier ejecución de este desencadenador.|  
|**max_elapsed_time**|**bigint**|Tiempo máximo transcurrido, en microsegundos, hasta la finalización de cualquier ejecución de este desencadenador.|  
  
## <a name="remarks"></a>Comentarios  
 En SQL Database de Microsoft Azure, las vistas de administración dinámica no pueden mostrar información que afecte a la contención de la base de datos o que exponga datos acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, cada fila que contiene datos que no pertenecen al inquilino conectado se filtra.  

Cuando se completa una consulta, se actualizan las estadísticas en la vista.  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.
  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve información acerca de los cinco principales desencadenadores identificados por el promedio de tiempo transcurrido.  
  
```sql  
PRINT '--top 5 CPU consuming triggers '  
  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40; relacionada con la ejecución Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sys.dm_exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [Sys.dm_exec_query_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
  [Sys.dm_exec_procedure_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
 [Sys.dm_exec_cached_plans &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
