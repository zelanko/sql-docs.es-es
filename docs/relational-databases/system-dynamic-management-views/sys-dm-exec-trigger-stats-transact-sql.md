---
title: Sys. dm_exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 65e54b90fa036e738f2e1e6a28498559051011a5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68262213"
---
# <a name="sysdm_exec_trigger_stats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve estadísticas de rendimiento de agregado para los desencadenadores en memoria caché. La vista contiene una fila por cada desencadenador y la duración de la fila corresponde al tiempo que el desencadenador permanece en memoria caché. Cuando se quita un desencadenador de la memoria caché, la fila correspondiente se elimina de esta vista. En ese momento, se genera un evento de Seguimiento de SQL de Estadísticas de rendimiento similar a **sys.dm_exec_query_stats**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Identificador de base de datos en que reside el desencadenador.|  
|**object_id**|**int**|Número de identificación del objeto del desencadenador.|  
|**type**|**char(2)**|Tipo del objeto:<br /><br /> TA = Desencadenador de ensamblado (CLR)<br /><br /> TR = Desencadenador SQL|  
|**Type_desc**|**nvarchar(60)**|Descripción del tipo de objeto:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary (64)**|Se puede utilizar para correlacionar con las consultas de **Sys. dm_exec_query_stats** que se ejecutaron desde dentro de este desencadenador.|  
|**plan_handle**|**varbinary (64)**|Identificador del plan en memoria. Este identificador es transitorio y permanece constante solo mientras el plan permanece en la memoria caché. Este valor se puede usar con la vista de administración dinámica **Sys. dm_exec_cached_plans** .|  
|**cached_time**|**datetime**|Momento en que el desencadenador se agregó a la caché.|  
|**last_execution_time**|**datetime**|Última vez que se ejecutó el desencadenador vez.|  
|**execution_count**|**bigint**|Número de veces que se ha ejecutado el desencadenador desde que se compiló por última vez.|  
|**total_worker_time**|**bigint**|Cantidad total de tiempo de CPU, en microsegundos, consumido por las ejecuciones de este desencadenador desde que se compiló.|  
|**last_worker_time**|**bigint**|Tiempo de CPU, en microsegundos, consumido la última vez que se ejecutó el desencadenador.|  
|**min_worker_time**|**bigint**|Tiempo máximo de CPU, en microsegundos, que ha consumido este desencadenador durante una ejecución.|  
|**max_worker_time**|**bigint**|Tiempo máximo de CPU, en microsegundos, que ha consumido este desencadenador durante una ejecución.|  
|**total_physical_reads**|**bigint**|Número total de lecturas físicas realizadas por las ejecuciones de este desencadenador desde que se compiló.|  
|**last_physical_reads**|**bigint**|Número de lecturas físicas realizadas la última vez que se ejecutó el desencadenador.|  
|**min_physical_reads**|**bigint**|Número mínimo de lecturas físicas que ha realizado este desencadenador durante una ejecución.|  
|**max_physical_reads**|**bigint**|Número máximo de lecturas físicas que ha realizado este desencadenador durante una ejecución.|  
|**total_logical_writes**|**bigint**|Número total de escrituras lógicas realizadas por las ejecuciones de este desencadenador desde que se compiló.|  
|**last_logical_writes**|**bigint**|El número de escrituras lógicas realizadas la última vez que se ejecutó el desencadenador.|  
|**min_logical_writes**|**bigint**|Número mínimo de escrituras lógicas realizadas por este desencadenador durante una ejecución.|  
|**max_logical_writes**|**bigint**|Número máximo de escrituras lógicas realizadas por este desencadenador durante una ejecución.|  
|**total_logical_reads**|**bigint**|Número total de lecturas lógicas realizadas por las ejecuciones de este desencadenador desde que se compiló.|  
|**last_logical_reads**|**bigint**|Número de lecturas lógicas realizadas la última vez que se ejecutó el desencadenador.|  
|**min_logical_reads**|**bigint**|Número mínimo de lecturas lógicas realizadas por este desencadenador durante una ejecución.|  
|**max_logical_reads**|**bigint**|Número máximo de lecturas lógicas realizadas por este desencadenador durante una ejecución.|  
|**total_elapsed_time**|**bigint**|Tiempo total transcurrido, en microsegundos, para las ejecuciones completadas de este desencadenador.|  
|**last_elapsed_time**|**bigint**|Tiempo transcurrido, en microsegundos, hasta la finalización de la ejecución más reciente de este desencadenador.|  
|**min_elapsed_time**|**bigint**|Tiempo mínimo transcurrido, en microsegundos, para cualquier ejecución completada de este desencadenador.|  
|**max_elapsed_time**|**bigint**|Tiempo máximo transcurrido, en microsegundos, para cualquier ejecución completada de este desencadenador.| 
|**total_spills**|**bigint**|Número total de páginas desbordadas por la ejecución de este desencadenador desde que se compiló.<br /><br /> **Se aplica a**: a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] partir de CU3|  
|**last_spills**|**bigint**|Número de páginas desbordadas la última vez que se ejecutó el desencadenador.<br /><br /> **Se aplica a**: a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] partir de CU3|  
|**min_spills**|**bigint**|Número mínimo de páginas que este desencadenador ha sobrevertido durante una ejecución.<br /><br /> **Se aplica a**: a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] partir de CU3|  
|**max_spills**|**bigint**|Número máximo de páginas que este desencadenador ha sobrevertido durante una ejecución.<br /><br /> **Se aplica a**: a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] partir de CU3|  
|**total_page_server_reads**|**bigint**|Número total de lecturas del servidor de páginas realizadas por las ejecuciones de este desencadenador desde que se compiló.<br /><br /> **Se aplica a**: hiperescala Azure SQL Database|  
|**last_page_server_reads**|**bigint**|Número de lecturas del servidor de páginas realizadas la última vez que se ejecutó el desencadenador.<br /><br /> **Se aplica a**: hiperescala Azure SQL Database|  
|**min_page_server_reads**|**bigint**|Número mínimo de lecturas del servidor de páginas que ha realizado este desencadenador durante una ejecución.<br /><br /> **Se aplica a**: hiperescala Azure SQL Database|  
|**max_page_server_reads**|**bigint**|Número máximo de lecturas del servidor de páginas que ha realizado este desencadenador durante una ejecución.<br /><br /> **Se aplica a**: hiperescala Azure SQL Database|  

  
## <a name="remarks"></a>Observaciones  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, se filtran todas las filas que contienen datos que no pertenecen al inquilino conectado.  

Cuando se completa una consulta, se actualizan las estadísticas en la vista.  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve información acerca de los cinco principales desencadenadores identificados por el promedio de tiempo transcurrido.  
  
```sql  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Consulte también  
[Funciones y vistas de administración dinámica relacionadas con la ejecución &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[Sys. dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[Sys. dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[Sys. dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
