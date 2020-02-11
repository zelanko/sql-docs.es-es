---
title: Sys. dm_column_store_object_pool (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83369736ee18c36b3967bbbd129e0fd64574a2ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68265987"
---
# <a name="sysdm_column_store_object_pool-transact-sql"></a>Sys. dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Devuelve recuentos de diferentes tipos de uso del bloque de memoria de objetos para los objetos de índice de almacén de columnas.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|Identificador de la base de datos. Esto es único dentro de una instancia de SQL Server base de datos o un servidor de Azure SQL Database. |  
|`object_id`|`int`|Id. del objeto. El objeto es uno de los object_types. | 
|`index_id`|`int`|Identificador del índice de almacén de columnas.|  
|`partition_number`|`bigint`|Número de partición en base 1 en el índice o montón. Cada tabla o vista tiene al menos una partición.| 
|`column_id`|`int`|Identificador de la columna de almacén de columnas. Es NULL para DELETE_BITMAP.| 
|`row_group_id`|`int`|IDENTIFICADOR de filas.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT: segmento de columna. `object_id`es el identificador del segmento. Un segmento almacena todos los valores de una columna dentro de un filas. Por ejemplo, si una tabla tiene 10 columnas, hay 10 segmentos de columna por filas. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY: un diccionario global que contiene información de búsqueda para todos los segmentos de columna de la tabla.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY: Diccionario local asociado a una columna.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY: otra representación del diccionario global. Esto proporciona una búsqueda inversa del valor que se va a dictionary_id. Se usa para crear segmentos comprimidos como parte de la carga masiva o de la tupla.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP: un mapa de bits que realiza un seguimiento de las eliminaciones de segmentos. Hay un mapa de bits de eliminación por partición.|  
|`access_count`|`int`|Número de accesos de lectura o escritura a este objeto.|  
|`memory_used_in_bytes`|`bigint`|Memoria usada por este objeto en el grupo de objetos.|  
|`object_load_time`|`datetime`|Hora del reloj en el que se ha introducido object_id en el grupo de objetos.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   
 
## <a name="see-also"></a>Consulte también  
  
 [Funciones y vistas de administración dinámica relacionadas con índices &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [Sys. dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
