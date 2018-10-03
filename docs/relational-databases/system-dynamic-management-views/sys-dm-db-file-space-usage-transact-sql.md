---
title: Sys.dm_db_file_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_file_space_usage
- sys.dm_db_file_space_usage_TSQL
- sys.dm_db_file_space_usage
- dm_db_file_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_file_space_usage dynamic management view
ms.assetid: 148a5276-a8d5-49d2-8146-3c63d24c2144
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b803b86c216d877c0e056dd4892931575ca91010
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838003"
---
# <a name="sysdmdbfilespaceusage-transact-sql"></a>sys.dm_db_file_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información de uso del espacio para cada fila de la base de datos.  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_db_file_space_usage**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|Id. de la base de datos.|  
|file_id|**smallint**|Identificador de archivo.<br /><br /> file_ID se asigna a file_id en [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) y a fileid en [sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md).|  
|filegroup_id|**smallint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Identificador de grupo de archivos|  
|total_page_count|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número total de páginas del archivo.|  
|allocated_extent_page_count|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número total de páginas de las extensiones asignadas en el archivo.|  
|unallocated_extent_page_count|**bigint**|Número total de páginas en las extensiones no asignadas en el archivo.<br /><br /> No se incluyen las páginas no utilizadas en extensiones asignadas.|  
|version_store_reserved_page_count|**bigint**|Número total de páginas en las extensiones uniformes asignadas para el almacén de versiones. Las páginas de almacén de la versión nunca se asignan desde extensiones mixtas.<br /><br /> No se incluyen las páginas IAM porque siempre se asignan desde extensiones mixtas. Se incluyen las páginas PFS si están asignadas desde una extensión uniforme.<br /><br /> Para obtener más información, consulte [sys.dm_tran_version_store &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md).|  
|user_object_reserved_page_count|**bigint**|Número total de páginas asignadas desde extensiones uniformes para objetos de usuario en la base de datos. En el recuento se incluyen las páginas no utilizadas de una extensión asignada.<br /><br /> No se incluyen las páginas IAM porque siempre se asignan desde extensiones mixtas. Se incluyen las páginas PFS si están asignadas desde una extensión uniforme.<br /><br /> Puede usar la columna total_pages de la [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) para devolver el recuento de páginas reservadas de cada unidad de asignación en el objeto de usuario de la vista de catálogo. No obstante, tenga en cuenta que la columna total_pages incluye las páginas IAM.|  
|internal_object_reserved_page_count|**bigint**|Número total de páginas en extensiones uniformes asignadas para objetos internos en el archivo. En el recuento se incluyen las páginas no utilizadas de una extensión asignada.<br /><br /> No se incluyen las páginas IAM porque siempre se asignan desde extensiones mixtas. Se incluyen las páginas PFS si están asignadas desde una extensión uniforme.<br /><br /> No existe ninguna vista de catálogo ni objeto de administración dinámica que devuelva el recuento de páginas de cada objeto interno.|  
|mixed_extent_page_count|**bigint**|Número total de páginas asignadas y no asignadas en extensiones mixtas asignadas en el archivo. Las extensiones mixtas contienen páginas asignadas a diferentes objetos. Este recuento no incluye todas las páginas IAM del archivo.|
|modified_extent_page_count|**bigint**|**Se aplica a**: de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br />Número total de páginas modificadas en asigna las extensiones del archivo desde la última copia de seguridad de base de datos completa. El número de páginas modificadas puede utilizarse para realizar un seguimiento de la cantidad de los cambios diferenciales en la base de datos desde la última copia de seguridad completa, para decidir si es necesaria la copia de seguridad diferencial.|
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
|distribution_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador numérico único asociado con la distribución.|  
  
## <a name="remarks"></a>Comentarios  
 Los recuentos de páginas siempre son en el nivel de extensión. Por tanto, los valores de recuento de páginas siempre serán un múltiplo de ocho. Las extensiones que contienen páginas de asignación del Mapa de asignación global (GAM) y del Mapa de asignación global compartido (SGAM) se asignan a extensiones uniformes. No se incluyen en los recuentos de páginas descritos anteriormente. Para obtener más información sobre las páginas y extensiones, consulte [páginas y extensiones Architecture Guide](../../relational-databases/pages-and-extents-architecture-guide.md). 
  
 El contenido del almacén de versión actual está en [sys.dm_tran_version_store](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md). El seguimiento de las páginas del almacén de la versión se realiza en el nivel de archivo en vez de en el nivel de sesión y tarea porque son recursos globales. Una sesión puede generar versiones, pero las versiones no pueden quitarse cuando finaliza la sesión. Debe tenerse en cuenta una limpieza del almacén de versiones cuando se tengan que ejecutar transacciones prolongadas que necesiten acceso a la versión determinada. Las transacciones de ejecución prolongada relacionadas con la versión limpieza del almacén se pueden detectar mediante la visualización de la columna elapsed_time_seconds en [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md).  
  
 Los cambios frecuentes en la columna mixed_extent_page_count pueden indicar un uso exhaustivo de páginas SGAM. Cuando ocurre esto, puede ver muchas esperas de PAGELATCH_UP en las que el recurso esperado es una página SGAM. Para obtener más información, consulte [sys.dm_os_waiting_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md), [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md), y [sys.dm_os_latch_ estadísticas &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md).  
  
## <a name="user-objects"></a>Objetos de usuario  
 Los objetos siguientes se incluyen en los contadores de páginas de objetos de usuario:  
  
-   Índices y tablas definidos por el usuario  
  
-   Índices y tablas del sistema  
  
-   Índices y tablas temporales globales  
  
-   Índices y tablas temporales locales  
  
-   Variables de tabla  
  
-   Tablas devueltas en las funciones con valores de tabla.  
  
## <a name="internal-objects"></a>Objetos internos  
 Los objetos internos están solo en tempdb. Los objetos siguientes se incluyen en los contadores de páginas de objetos internos:  
  
-   Tablas de trabajo para operaciones de cola o cursor y almacenamiento de objetos grandes (LOB) temporales  
  
-   Archivos de trabajo para operaciones como la combinación hash  
  
-   Ordenaciones  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|sys.dm_db_file_space_usage.database_id, file_id|sys.dm_io_virtual_file_stats.database_id, file_id|Uno a uno|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="examples"></a>Ejemplos  
  
### <a name="determing-the-amount-of-free-space-in-tempdb"></a>Determinar la cantidad de espacio disponible en tempdb  
 La consulta siguiente devuelve el número total de páginas libres y el espacio libre total en megabytes (MB) están disponibles en todos los archivos de **tempdb**.  
  
```sql
USE tempdb;  
GO  
SELECT SUM(unallocated_extent_page_count) AS [free pages],   
(SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]  
FROM sys.dm_db_file_space_usage;  
```  

### <a name="determining-the-amount-of-space-used-by-user-objects"></a>Determinar la cantidad de espacio utilizado por objetos de usuario  
 La consulta siguiente devuelve el número total de páginas utilizadas por los objetos de usuario y el espacio total utilizado por los objetos de usuario en tempdb.  
  
```sql  
USE tempdb;  
GO  
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],  
(SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]  
FROM sys.dm_db_file_space_usage;
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
