---
title: Sys.dm_db_index_usage_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_usage_stats_TSQL
- sys.dm_db_index_usage_stats
- sys.dm_db_index_usage_stats_TSQL
- dm_db_index_usage_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_usage_stats dynamic management view
ms.assetid: d06a001f-0f72-4679-bc2f-66fff7958b86
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d2096243b65573d7d54a372252794976c93d527
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52415340"
---
# <a name="sysdmdbindexusagestats-transact-sql"></a>sys.dm_db_index_usage_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve recuentos de diferentes tipos de operaciones de índice y la hora en que se realizó por última vez cada uno de los tipos de operación.  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, cada fila que contiene datos que no pertenecen al inquilino conectado se filtra.  
  
> [!NOTE]  
>  **Sys.dm_db_index_usage_stats** no devuelve información acerca de los índices optimizados para memoria. Para obtener información sobre el uso de índices optimizados para memoria, vea [sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md).  
  
> [!NOTE]  
>  Para llamar a esta vista desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilice **sys.dm_pdw_nodes_db_index_usage_stats**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**smallint**|Id. de la base de datos en la que se define la tabla o vista.|  
|**object_id**|**int**|Id. de la tabla o vista en la que se define el índice.|  
|**index_id**|**int**|Id. del índice.|  
|**user_seeks**|**bigint**|Número de consultas de búsqueda realizadas por el usuario.|  
|**user_scans**|**bigint**|Número de recorridos por consultas de usuario que no utilizan 'Buscar' predicado.|  
|**user_lookups**|**bigint**|Número de búsquedas de marcadores realizadas por consultas de usuario.|  
|**user_updates**|**bigint**|Número de consultas de actualización realizadas por el usuario. Esto incluye Insert, Delete y que representa el número de operaciones realizadas no las filas reales afectadas actualiza. Por ejemplo, si elimina 1000 filas en una sola instrucción, este recuento se incrementa en 1|  
|**last_user_seek**|**datetime**|Hora en que el usuario realizó la última búsqueda.|  
|**last_user_scan**|**datetime**|Hora en que el usuario realizó el último recorrido.|  
|**last_user_lookup**|**datetime**|Hora de la última búsqueda del usuario.|  
|**last_user_update**|**datetime**|Hora en que el usuario realizó la última actualización.|  
|**system_seeks**|**bigint**|Número de consultas de búsqueda realizadas por el sistema.|  
|**system_scans**|**bigint**|Número de consultas de recorrido realizadas por el sistema.|  
|**system_lookups**|**bigint**|Número de búsquedas realizadas por consultas del sistema.|  
|**system_updates**|**bigint**|Número de consultas de actualización realizadas por el sistema.|  
|**last_system_seek**|**datetime**|Hora de última búsqueda del sistema.|  
|**last_system_scan**|**datetime**|Hora en que el sistema realizó el último recorrido.|  
|**last_system_lookup**|**datetime**|Hora en que el sistema realizó la última búsqueda.|  
|**last_system_update**|**datetime**|Hora en que el sistema realizó la última actualización.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="remarks"></a>Comentarios  
 Cada búsqueda, recorrido o actualización en el índice especificado realizado por una ejecución de la consulta se cuenta como un uso de ese índice e incrementa el contador correspondiente en esa vista. Se ofrece información tanto de las operaciones causadas por las consultas emitidas por el usuario, como de las consultas generadas internamente, tales como los recorridos realizados para recopilar estadísticas.  
  
 El **user_updates** contador indica el nivel de mantenimiento en el índice causado por insertar, actualizar o eliminar operaciones en la tabla o vista subyacente. Puede utilizar esta vista para determinar los índices que las aplicaciones apenas utilizan. También puede utilizar esta vista para determinar los índices que producen una sobrecarga de mantenimiento. Puede considerar la opción de quitar los índices que produzcan esta sobrecarga, pero que no se utilicen para consultas o se usen con poca frecuencia.  
  
 Los contadores se inicializan en un valor vacío cada vez que se inicia el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER). Además, cada vez que una base de datos se separa o se apaga (por ejemplo, porque se establece AUTO_CLOSE en ON), se quitan todas las filas asociadas con la base de datos.  
  
 Cuando se utiliza un índice, se agrega una fila a **sys.dm_db_index_usage_stats** si ya no existe una fila para el índice. Cuando se agrega la fila, sus contadores se establecen inicialmente en cero.  
  
 Durante la actualización a [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], se quitan las entradas de sys.dm_db_index_usage_stats. A partir [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], se conservan las entradas tal como estaban antes de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].  
  
## <a name="permissions"></a>Permisos  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.  
  
## <a name="see-also"></a>Vea también  

 [Funciones y vistas de administración dinámica relacionadas con índices &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  


