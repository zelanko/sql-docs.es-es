---
title: Broker (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.internal_tables
- internal_tables
- sys.internal_tables_TSQL
- internal_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- internal tables
- sys.internal_tables catalog view
ms.assetid: a5821c70-f150-4676-8476-3a31f7403dca
caps.latest.revision: 52
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 023f2b4a26a816ed31013aa20355593d0eda0faa
ms.sourcegitcommit: 84cc5ed00833279da3adbde9cb6133a4e788ed3f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2018
ms.locfileid: "39216896"
---
# <a name="sysinternaltables-transact-sql"></a>sys.internal_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada objeto que es una tabla interna. Las tablas internas son generadas de forma automática por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fin de permitir varias características. Por ejemplo, cuando se crea un índice XML principal, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea automáticamente una tabla interna para hacer que persistan los datos del documento XML dividido. Las tablas internas aparecen en la **sys** esquema de cada base de datos y tienen nombres únicos y generados por el sistema que indican su función, por ejemplo, **xml_index_nodes_2021582240_32001** o  **queue_messages_1977058079**  
  
 Las tablas internas no contienen datos accesibles para el usuario y su esquema es fijo e inalterable. No se puede hacer referencia a los nombres de las tablas internas en las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por ejemplo, no se puede ejecutar una instrucción como SELECT \* FROM  *\<sys.internal_table_name >*. Sin embargo, se pueden consultar vistas de catálogo para ver los metadatos de las tablas internas.  
  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**\<Las columnas que se heredan de sys.objects >**||Para obtener una lista de columnas que hereda esta vista, consulte [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**internal_type**|**tinyint**|Tipo de la tabla interna:<br /><br /> 201 = **queue_messages**<br /><br /> 202 = **xml_index_nodes**<br /><br /> 203 = **fulltext_catalog_freelist**<br /><br /> 205 = **query_notification**<br /><br /> 206 = **service_broker_map**<br /><br /> 207 = **extended_indexes** (por ejemplo, un índice espacial)<br /><br /> 208 = **filestream_tombstone**<br /><br /> 209 = **change_tracking**<br /><br /> 210 = **tracked_committed_transactions**<br /><br /> 236 = **selective_xml_index_node_table**|  
|**internal_type_desc**|**nvarchar(60)**|Descripción del tipo de tabla interna:<br /><br /> QUEUE_MESSAGES<br /><br /> XML_INDEX_NODES<br /><br /> FULLTEXT_CATALOG_FREELIST<br /><br /> FULLTEXT_CATALOG_MAP<br /><br /> QUERY_NOTIFICATION<br /><br /> SERVICE_BROKER_MAP<br /><br /> EXTENDED_INDEXES<br /><br /> FILESTREAM_TOMBSTONE<br /><br /> CHANGE_TRACKING<br /><br /> TRACKED_COMMITTED_TRANSACTIONS<br /><br /> SELECTIVE_XML_INDEX_NODE_TABLE|  
|**parent_id**|**int**|Id. del primario, independientemente de si es de ámbito de esquema o no. Es 0 si no hay primario.<br /><br /> **queue_messages** = **object_id** de cola<br /><br /> **xml_index_nodes** = **object_id** del índice xml<br /><br /> **fulltext_catalog_freelist** = **fulltext_catalog_id** del catálogo de texto completo<br /><br /> **fulltext_index_map** = **object_id** del índice de texto completo<br /><br /> **query_notification**, o **service_broker_map** = 0<br /><br /> **extended_indexes** = **object_id** de un índice extendido, como un índice espacial<br /><br /> **object_id** de la tabla para la tabla que está habilitado el seguimiento = **change_tracking**|  
|**parent_minor_id**|**int**|Id. secundario del primario.<br /><br /> **xml_index_nodes** = **index_id** del índice XML<br /><br /> **extended_indexes** = **index_id** de un índice extendido, como un índice espacial<br /><br /> 0 = **queue_messages**, **fulltext_catalog_freelist**, **fulltext_index_map**, **query_notification**,  **service_broker_map**, o **change_tracking**|  
|**lob_data_space_id**|**int**|Un valor distinto de cero es el Id. del espacio de datos (grupo de archivos o esquema de partición) que almacena los datos de objetos grandes (LOB) para esta tabla.|  
|**filestream_data_space_id**|**int**|Reservado para uso futuro.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Notas  
 Las tablas internas se colocan en el mismo grupo de archivos que la entidad primaria. Puede usar la consulta del catálogo que se muestra en el ejemplo F a continuación para devolver el número de páginas que usan las tablas internas para los datos almacenados consecutivamente, no consecutivamente y de objetos grandes (LOB).  
  
 Puede usar el [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) procedimiento del sistema para devolver datos de uso de espacio para las tablas internas. **sp_spaceused** informa del espacio de tabla interna de las maneras siguientes:  
  
-   Cuando se especifica un nombre de cola, se hace referencia a la tabla interna subyacente asociada a la cola y se informa del consumo del almacenamiento.  
  
-   Las páginas que se usan en las tablas internas de índices XML, índices espaciales y los índices de texto completo se incluyen en el **index_size** columna. Cuando se especifica una tabla o nombre de la vista indizada, las páginas de los índices XML, índices espaciales y los índices de texto completo para ese objeto se incluyen en las columnas **reservada** y **index_size**.  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se demuestra cómo consultar los metadatos de las tablas internas de consulta mediante vistas de catálogo.  
  
### <a name="a-show-internal-tables-that-inherit-columns-from-the-sysobjects-catalog-view"></a>A. Mostrar las tablas internas que heredan las columnas de la vista de catálogo sys.objects  
  
```  
SELECT * FROM sys.objects WHERE type = 'IT';  
```  
  
### <a name="b-return-all-internal-table-metadata-including-that-which-is-inherited-from-sysobjects"></a>B. Devolver todos los metadatos de las tablas internas (incluido los que se heredan de sys.objects)  
  
```  
SELECT * FROM sys.internal_tables;  
```  
  
### <a name="c-return-internal-table-columns-and-column-data-types"></a>C. Devolver las columnas de las tablas internas y los tipos de datos de las columnas  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,typ.name AS column_data_type   
    ,col.*  
FROM sys.internal_tables AS itab  
JOIN sys.columns AS col ON itab.object_id = col.object_id  
JOIN sys.types AS typ ON typ.user_type_id = col.user_type_id  
ORDER BY itab.name, col.column_id;  
```  
  
### <a name="d-return-internal-table-indexes"></a>D. Devolver los índices de las tablas internas  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    , itab.name AS internal_table_name  
    , idx.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx ON itab.object_id = idx.object_id  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="e-return-internal-table-statistics"></a>E. Devolver estadísticas de las tablas internas  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    , s.*  
FROM sys.internal_tables AS itab  
JOIN sys.stats AS s ON itab.object_id = s.object_id  
ORDER BY itab.name, s.stats_id;  
```  
  
### <a name="f-return-internal-table-partition-and-allocation-unit-information"></a>F. Devolver información de la unidad de asignación y de la partición de las tablas internas  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,idx.name AS heap_or_index_name  
    ,p.*  
    ,au.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx  
--     JOIN to the heap or the clustered index  
    ON itab.object_id = idx.object_id AND idx.index_id IN (0,1)  
JOIN   sys.partitions AS p   
    ON p.object_id = idx.object_id AND p.index_id = idx.index_id  
JOIN   sys.allocation_units AS au  
--     IN_ROW_DATA (type 1) and ROW_OVERFLOW_DATA (type 3) => JOIN to partition's Hobt  
--     else LOB_DATA (type 2) => JOIN to the partition ID itself.  
ON au.container_id =    
    CASE au.type   
        WHEN 2 THEN p.partition_id   
        ELSE p.hobt_id   
    END  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="g-return-internal-table-metadata-for-xml-indexes"></a>G. Devolver los metadatos de las tablas internas para los índices XML  
  
```  
SELECT t.name AS parent_table  
    ,t.object_id AS parent_table_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
    ,xi.name AS primary_XML_index_name  
    ,xi.index_id as primary_XML_index_id  
FROM sys.internal_tables AS it  
JOIN sys.tables AS t   
    ON it.parent_id = t.object_id  
JOIN sys.xml_indexes AS xi   
    ON it.parent_id = xi.object_id  
    AND it.parent_minor_id  = xi.index_id  
WHERE it.internal_type_desc = 'XML_INDEX_NODES';  
GO  
```  
  
### <a name="h-return-internal-table-metadata-for-service-broker-queues"></a>H. Devolver los metadatos de las tablas internas para las colas de Service Broker  
  
```  
SELECT q.name AS queue_name  
    ,q.object_id AS queue_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.service_queues  AS  q ON it.parent_id = q.object_id  
WHERE it.internal_type_desc = 'QUEUE_MESSAGES';  
GO  
```  
  
## <a name="i-return-internal-table-metadata-for-all-service-broker-services"></a>I. Devolver los metadatos de las tablas internas para todos los servicios de Service Broker  
  
```  
SELECT *   
FROM tempdb.sys.internal_tables   
WHERE internal_type_desc = 'SERVICE_BROKER_MAP';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
