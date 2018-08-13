---
title: Sys.dm_exec_query_memory_grants (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_memory_grants_TSQL
- sys.dm_exec_query_memory_grants
- sys.dm_exec_query_memory_grants_TSQL
- dm_exec_query_memory_grants
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_memory_grants dynamic management view
ms.assetid: 2c417747-2edd-4e0d-8a9c-e5f445985c1a
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 0c0d13ebbda9f8031987b5545715de96fc37c12a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559595"
---
# <a name="sysdmexecquerymemorygrants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre todas las consultas que han solicitado y están esperando una concesión de memoria o que haya concedido una concesión de memoria. Las consultas que no requieren una concesión de memoria no aparecerán en esta vista. Por ejemplo, ordenar y operaciones de combinación hash tienen concesiones de memoria para la ejecución de consulta, mientras que las consultas sin un **ORDER BY** cláusula no tendrá una memoria conceder.  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, cada fila que contiene datos que no pertenecen al inquilino conectado se filtra. Además, los valores de las columnas **scheduler_id**, **wait_order**, **pool_id**, **group_id** se filtran; se establece el valor de columna en NULL.  
  
> [!NOTE]  
> Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_exec_query_memory_grants**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|Id. (SPID) de la sesión en la que se está ejecutando esta consulta.|  
|**request_id**|**int**|Identificador de la solicitud. Es único en el contexto de la sesión.|  
|**scheduler_id**|**int**|Id. del programador que programa esta consulta.|  
|**grado de paralelismo**|**smallint**|Grado de paralelismo de esta consulta.|  
|**request_time**|**datetime**|Fecha y hora a la que esta consulta solicitó la concesión de memoria.|  
|**grant_time**|**datetime**|Fecha y hora a la que se concedió la memoria para esta consulta. Es NULL si aún no se ha concedido la memoria.|  
|**requested_memory_kb**|**bigint**|Memoria solicitada total en kilobytes.|  
|**granted_memory_kb**|**bigint**|Memoria total realmente otorgada en kilobytes. Puede ser NULL si aún no se ha concedido la memoria. Una situación típica, este valor debe ser el mismo que **requested_memory_kb**. En la creación de índices, el servidor puede permitir memoria adicional a petición además de la memoria concedida inicialmente.|  
|**required_memory_kb**|**bigint**|Memoria mínima necesaria para ejecutar esta consulta en kilobytes. **requested_memory_kb** es igual o mayor que esta cantidad.|  
|**used_memory_kb**|**bigint**|Memoria física usada en este momento en kilobytes.|  
|**max_used_memory_kb**|**bigint**|Memoria física máxima usada hasta este momento en kilobytes.|  
|**query_cost**|**float**|Costo estimado de la consulta.|  
|**timeout_sec**|**int**|Tiempo de espera en segundos antes de que esta consulta abandone la solicitud de concesión de memoria.|  
|**resource_semaphore_id**|**smallint**|Identificador no único del semáforo de recursos al que está esperando esta consulta.<br /><br /> **Nota:** este identificador es único en las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que sean anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Este cambio puede afectar a la solución de problemas de ejecución de consultas. Para obtener más información, vea la sección “Comentarios” más adelante en este tema.|  
|**queue_id**|**smallint**|Id. de la cola de espera en la que esta consulta espera las concesiones de memoria. Es NULL si ya se ha concedido la memoria.|  
|**wait_order**|**int**|Orden secuencial de las consultas de espera especificado dentro de **queue_id**. Este valor puede cambiar para una determinada consulta si otras consultas obtienen concesiones de memoria o tiempos de espera. Es NULL si ya se ha concedido la memoria.|  
|**is_next_candidate**|**bit**|Candidata para la siguiente concesión de memoria.<br /><br /> 1 = Sí<br /><br /> 0 = No<br /><br /> NULL = Ya se ha concedido la memoria.|  
|**wait_time_ms**|**bigint**|Tiempo de espera en milisegundos. Es NULL si ya se ha concedido la memoria.|  
|**plan_handle**|**varbinary (64)**|Identificador de este plan de consulta. Use **sys.dm_exec_query_plan** para extraer el plan XML real.|  
|**sql_handle**|**varbinary (64)**|Identificador del texto de [!INCLUDE[tsql](../../includes/tsql-md.md)] de esta consulta. Use **sys.dm_exec_sql_text** para obtener los datos reales [!INCLUDE[tsql](../../includes/tsql-md.md)] texto.|  
|**group_id**|**int**|Id. para el grupo de cargas de trabajo donde se está ejecutando la consulta.|  
|**pool_id**|**int**|Id. del grupo de recursos de servidor al que pertenece este grupo de cargas de trabajo.|  
|**is_small**|**tinyint**|Cuando se establece en 1, indica que esta concesión utiliza el semáforo de recursos pequeño. Cuando se establece en 0, indica que se utiliza un semáforo normal.|  
|**ideal_memory_kb**|**bigint**|Tamaño, en kilobytes (KB), de la concesión de memoria para ajustar todo en la memoria física. Está basado en la estimación de la cardinalidad.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
   
## <a name="remarks"></a>Notas  
 Un escenario de depuración típico para un tiempo de espera de consulta puede tener el siguiente aspecto:  
  
-   Comprobar estado memoria total sistema mediante [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md), [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)y varios contadores de rendimiento.  
  
-   Comprobar las reservas de memoria de ejecución de consultas en **sys.dm_os_memory_clerks** donde `type = 'MEMORYCLERK_SQLQERESERVATIONS'`.  
  
-   Comprobar consultas en espera<sup>1</sup> de concesiones con **sys.dm_exec_query_memory_grants**.  
  
    ```sql  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
    
    <sup>1</sup> En este caso, el tipo de espera normalmente es RESOURCE_SEMAPHORE. Para obtener más información, vea [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). 
  
-   Buscar la memoria caché para las consultas con concesiones de memoria mediante [sys.dm_exec_cached_plans &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) y [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```sql  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
    ```  
  
-   Examinar más detenidamente las consultas de gran cantidad de memoria mediante [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).  
  
    ```sql  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
      plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
    ```  
  
-   Si sospecha que una consulta descontrolada, examine el plan de presentación de [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) y texto del lote [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
 Las consultas que utilizan vistas de administración dinámica que incluyen `ORDER BY` o agregados pueden aumentar el consumo de memoria y, por tanto, contribuir al problema que están solucionando.  
  
 La característica del regulador de recursos permite que un administrador de bases de datos distribuya los recursos del servidor entre los grupos de recursos de servidor, hasta un máximo de 64 fondos. Empezando por [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], cada grupo se comporta como una instancia independiente del servidor pequeña y requiere 2 semáforos. El número de filas que se devuelven desde **sys.dm_exec_query_resource_semaphores** puede ser hasta 20 veces más que las filas que se devuelven en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_exec_query_resource_semaphores &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)     
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [Funciones y vistas de administración dinámica relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
