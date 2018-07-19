---
title: Sys.dm_column_store_object_pool (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 18faadc4dbcd4b2966c8e922aed01127b13c8baa
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061413"
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>sys.dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Devuelve los recuentos de diferentes tipos de uso del grupo de memoria de objeto para objetos de índice de almacén de columnas.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|Identificador de la base de datos. Esto es único dentro de una instancia de una base de datos de SQL Server o un servidor de base de datos SQL de Azure. |  
|`object_id`|`int`|Id. del objeto. El objeto es uno de los tipos de objetos. | 
|`index_id`|`int`|Identificador del índice de almacén de columnas.|  
|`partition_number`|`bigint`|Número de partición en base 1 en el índice o montón. Cada tabla o vista tiene al menos una partición.| 
|`column_id`|`int`|Identificador de la columna de almacén de columnas. Esto es nulo para DELETE_BITMAP.| 
|`row_group_id`|`int`|Id. del grupo de filas.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT – un segmento de columna. `object_id` es el identificador de segmento. Un segmento almacena todos los valores de una columna dentro de un grupo de filas. Por ejemplo, si una tabla tiene 10 columnas, hay 10 segmentos de columna por grupo de filas. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY: un diccionario global que contiene información de búsqueda de todos los segmentos de columna en la tabla.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY - un diccionario local asociado a una columna.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY: otra representación del diccionario global. Esto proporciona una búsqueda inversa de valor a dictionary_id. Se usa para crear segmentos comprimidos como parte del motor de tupla o la carga masiva.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP: elimina de un mapa de bits que realiza el seguimiento de segmento. Hay un mapa de bits de eliminación por partición.|  
|`access_count`|`int`|Número de lee o escribe los accesos a este objeto.|  
|`memory_used_in_bytes`|`bigint`|Memoria usada por este objeto en el grupo de objetos.|  
|`object_load_time`|`datetime`|Tiempo de reloj para cuando object_id se puso en el grupo de objetos.|  
  
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
  
  
