---
title: Sys.dm_column_store_object_pool (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
caps.latest.revision: "12"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d949467865b22b68188800a64d49ef7dc4a496c9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>Sys.dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Devuelve recuentos de diferentes tipos de uso de bloque de memoria de objeto para los objetos de índice de almacén de columnas.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|Identificador de la base de datos. Es único dentro de una instancia de una base de datos de SQL Server o un servidor de base de datos de SQL Azure. |  
|`object_id`|`int`|Id. del objeto. El objeto es uno de los tipos de objetos. | 
|`index_id`|`int`|Identificador del índice de almacén de columnas.|  
|`partition_number`|`bigint`|Número de partición en base 1 en el índice o montón. Cada tabla o vista tiene al menos una partición.| 
|`column_id`|`int`|Identificador de la columna de almacén de columnas. Esto es NULL para DELETE_BITMAP.| 
|`row_group_id`|`int`|Id. del grupo de filas.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT: un segmento de columna. `object_id`es el identificador de segmento. Un segmento almacena todos los valores de una columna dentro de un grupo de filas. Por ejemplo, si una tabla tiene 10 columnas, hay 10 segmentos de columna por grupo de filas. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY: un diccionario global que contiene información de búsqueda de todos los segmentos de columna en la tabla.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY - un diccionario local asociado a una columna.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY – otra representación del diccionario global. Esto proporciona un buscar inverso del valor a dictionary_id. Se usa para crear segmentos comprimidos como parte del motor de tupla o la carga masiva.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP: elimina de un mapa de bits que realiza el seguimiento de segmento. Hay un mapa de bits de eliminación por partición.|  
|`access_count`|`int`|Número de lectura o escritura accesos a este objeto.|  
|`memory_used_in_bytes`|`bigint`|Memoria utilizada por este objeto en el grupo de objetos.|  
|`object_load_time`|`datetime`|Tiempo de reloj para cuando object_id se puso en el grupo de objetos.|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.  

 
## <a name="see-also"></a>Vea también  
  
 [Índice relacionadas con funciones y vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [Sys.dm_db_index_operational_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
