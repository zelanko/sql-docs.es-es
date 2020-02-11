---
title: Sys. column_store_segments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_store_segments
- sys.column_store_segments_TSQL
- sys.column_store_segments
- column_store_segments_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_segments catalog view
ms.assetid: 1253448c-2ec9-4900-ae9f-461d6b51b2ea
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8d476e2f21693254eac5fc4712d53ac854e74ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68140000"
---
# <a name="syscolumn_store_segments-transact-sql"></a>sys.column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

Devuelve una fila por cada segmento de columna de un índice de almacén de columnas. Hay un segmento de columna por columna por cada filas. Por ejemplo, una tabla con 10 filas y 34 columnas devuelve 340 filas. 
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**partition_id**|**BIGINT**|Indica el identificador de partición. Es único en una base de datos.|  
|**hobt_id**|**BIGINT**|Identificador del montón o el índice de árbol b (hobt) para la tabla que contiene este índice de almacén de columnas.|  
|**column_id**|**int**|Identificador de la columna de almacén de columnas.|  
|**segment_id**|**int**|IDENTIFICADOR de filas. Por compatibilidad con versiones anteriores, el nombre de columna sigue siendo llamado segment_id aunque se trata del identificador de filas. Puede identificar de forma única un segmento mediante \<hobt_id, partition_id, column_id> <segment_id>.|  
|**Versión**|**int**|Versión del formato de segmento de columna.|  
|**encoding_type**|**int**|Tipo de codificación que se usa para ese segmento:<br /><br /> 1 = VALUE_BASED-no cadena/binaria sin diccionario (muy similar a 4 con algunas variaciones internas)<br /><br /> 2 = VALUE_HASH_BASED una columna no cadena/binaria con valores comunes en el Diccionario<br /><br /> 3 = STRING_HASH_BASED-cadena/columna binaria con valores comunes en el Diccionario<br /><br /> 4 = STORE_BY_VALUE_BASED-no cadena/binaria sin Diccionario<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-cadena/binario sin Diccionario<br /><br /> Todas las codificaciones aprovechan el empaquetado de bits y la codificación de longitud de ejecución cuando sea posible.|  
|**row_count**|**int**|Número de filas del grupo de filas.|  
|**has_nulls**|**int**|1 si el segmento de la columna tiene valores NULL.|  
|**base_id**|**BIGINT**|Identificador del valor base si se está utilizando el tipo de codificación 1.  Si no se usa el tipo de codificación 1, base_id se establece en-1.|  
|**magnitude**|**float**|Magnitud si se usa el tipo de codificación 1.  Si no se usa el tipo de codificación 1, Magnitude se establece en-1.|  
|**primary_dictionary_id**|**int**|Un valor de 0 representa el Diccionario global. Un valor de-1 indica que no hay ningún diccionario global creado para esta columna.|  
|**secondary_dictionary_id**|**int**|Un valor distinto de cero apunta al diccionario local para esta columna en el segmento actual (es decir, filas). Un valor de-1 indica que no hay ningún diccionario local para este segmento.|  
|**min_data_id**|**BIGINT**|Identificador de datos mínimo en el segmento de columna.|  
|**max_data_id**|**BIGINT**|Identificador de datos máximo en el segmento de columna.|  
|**null_value**|**BIGINT**|Valor usado para representar valores NULL.|  
|**on_disk_size**|**BIGINT**|Tamaño del segmento en bytes.|  
  
## <a name="remarks"></a>Observaciones  
 La consulta siguiente devuelve información acerca de los segmentos de un índice de almacén de columnas.  
  
```sql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 5 OR i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
GO  
```  
  
## <a name="permissions"></a>Permisos  
 Todas las columnas necesitan al menos el permiso **View definition** en la tabla. Las columnas siguientes devuelven null a menos que el usuario también tenga el permiso **Select** : has_nulls, base_id, Magnitude, min_data_id, max_data_id y null_value.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Preguntas más frecuentes sobre el catálogo del sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Sys. Columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [Sys. computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guía de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-overview.md)    
 [Sys. column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
  

