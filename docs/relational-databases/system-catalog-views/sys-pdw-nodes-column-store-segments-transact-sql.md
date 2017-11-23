---
title: Sys.pdw_nodes_column_store_segments (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79944f54d12681ab7a430362ec0204a8d54bf477
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>Sys.pdw_nodes_column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada columna de un índice de almacén de columnas.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Indica el identificador de partición. Es único en una base de datos.|  
|**hobt_id**|**bigint**|Identificador del montón o el índice de árbol b (hobt) para la tabla que contiene este índice de almacén de columnas.|  
|**column_id**|**int**|Identificador de la columna de almacén de columnas.|  
|**segment_id**|**int**|Identificador del segmento de columna.|  
|**version**|**int**|Versión del formato de segmento de columna.|  
|**encoding_type**|**int**|Tipo de codificación empleado para dicho segmento.|  
|**row_count**|**int**|Número de filas del grupo de filas.|  
|**has_nulls**|**int**|1 si el segmento de la columna tiene valores NULL.|  
|**base_id**|**bigint**|Identificador del valor base si se utiliza la codificación de tipo 1.  Si el tipo de codificación 1 no se está usando, base_id se establece en 1.|  
|**magnitud**|**float**|Magnitud si se utiliza el tipo de codificación 1.  Si el tipo de codificación 1 no se está usando, magnitud se establece en 1.|  
|**primary__dictionary_id**|**int**|Identificador del diccionario principal.|  
|**secondary_dictionary_id**|**int**|Identificador del diccionario secundario. Devuelve -1 si no hay ningún diccionario secundario.|  
|**min_data_id**|**bigint**|Identificador de datos mínimo en el segmento de columna.|  
|**max_data_id**|**bigint**|Identificador de datos máximo en el segmento de columna.|  
|**null_value**|**bigint**|Valor usado para representar valores NULL.|  
|**on_disk_size**|**bigint**|Tamaño del segmento en bytes.|  
|**pdw_node_id**|**int**|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nota.|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 La consulta siguiente devuelve información acerca de los segmentos de un índice de almacén de columnas.  
  
```tsql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
```  
  
 Unir sys.pdw_nodes_column_store_segments con otras tablas del sistema para determinar el recuento de filas y el tamaño de los segmentos en el disco.  
  
```  
SELECT o.name, css.hobt_id, css. column_id, css.pdw_node_id, css.row_count, css.on_disk_size  
FROM sys.pdw_nodes_column_store_segments AS css  
JOIN sys.pdw_nodes_partitions AS pnp  
    ON css.partition_id = pnp.partition_id  
JOIN sys.pdw_nodes_tables AS part  
    ON pnp.object_id = part.object_id   
    AND pnp.pdw_node_id = part.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON part.name = TMap.physical_name  
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
ORDER BY css.hobt_id, css.column_id;  
```  
  
## <a name="permissions"></a>Permissions  
 Requiere **VIEW SERVER STATE** permiso.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Crear índice de almacén de columnas &#40; Transact-SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [Sys.pdw_nodes_column_store_row_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [Sys.pdw_nodes_column_store_dictionaries &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  

