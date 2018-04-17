---
title: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
caps.latest.revision: 6
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ba6a0f40c709667195c1507b9a36b79c99f1f18e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve actual i/OS, bloqueo, de nivel de fila y obtener acceso a la actividad de método de grupos de filas comprimidos en un índice de almacén de columnas. Use **sys.dm_db_column_store_row_group_operational_stats** para realizar el seguimiento de la cantidad de tiempo una consulta de usuario debe esperar para leer o escribir en un grupo de filas comprimido o una partición de un índice de almacén de columnas e identifique los grupos de filas que tienen actividades de E/S importantes o las zonas activas.  
  
 Índices columnstore en memoria no aparecen en esta DMV.  
 
 
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador de la tabla con el índice de almacén de columnas.|  
|**index_id**|**int**|Identificador del índice de almacén de columnas.|  
|**partition_number**|**int**|Número de partición en base 1 en el índice o montón.|  
|**Row_group_id**|**int**|Id. del grupo de filas en el índice de almacén de columnas. Es único dentro de una partición.|  
|**scan_count**|**int**|Número de exámenes mediante el grupo de filas desde el último reinicio SQL.|  
|**delete_buffer_scan_count**|**int**|Número de veces que el búfer de eliminación se utiliza para determinar las filas eliminadas de este grupo de filas. Esto incluye el acceso a la tabla hash en memoria y el árbol b subyacente.|  
|**index_scan_count**|**int**|Número de veces que se ha analizado la partición de índice de almacén de columnas. Este es el mismo para todos los grupos de filas en la partición.|  
|**rowgroup_lock_count**|**bigint**|Recuento acumulado de solicitudes de bloqueo para este grupo de filas desde el último reinicio SQL.|  
|**rowgroup_lock_wait_count**|**bigint**|Número acumulado de veces que el motor de base de datos ha esperado en este bloqueo de grupo de filas desde el último reinicio SQL.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|Número acumulado de milisegundos que el motor de base de datos ha esperado en este bloqueo de grupo de filas desde el último reinicio SQL.|  
  
## <a name="permissions"></a>Permissions  
 Necesita los siguientes permisos:  
  
-   Permiso CONTROL en la tabla especificada por object_id.  
  
-   Permiso VIEW DATABASE STATE para devolver información acerca de todos los objetos de la base de datos, utilizando el carácter comodín de objeto @*object_id* = NULL  
  
 El permiso VIEW DATABASE STATE permite devolver todos los objetos de la base de datos, independientemente de los permisos CONTROL denegados en objetos específicos.  
  
 Si se deniega el permiso VIEW DATABASE STATE, no se puede devolver ningún objeto de la base de datos, independientemente de que se hayan concedido permisos CONTROL a objetos específicos. Además, cuando el carácter comodín de base de datos @*database_id*= se especifica NULL, se omite la base de datos.  
  
 Para obtener más información, consulte [funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con índices &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Supervisar y optimizar el rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [Sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

