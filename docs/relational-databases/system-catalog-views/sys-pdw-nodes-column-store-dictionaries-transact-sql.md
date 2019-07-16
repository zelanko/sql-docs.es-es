---
title: sys.pdw_nodes_column_store_dictionaries (Transact-SQL) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.custom: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 7ae1c2e4-45c0-4880-a692-1f299fbcfd19
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7a588d23d5e3e7f9cb314342a739ceb8e051ca2c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059379"
---
# <a name="syspdwnodescolumnstoredictionaries-transact-sql"></a>sys.pdw_nodes_column_store_dictionaries (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada diccionario que se usa en los índices de almacén de columnas. Los diccionarios se usan para codificar algunos tipos de datos (no todos), por tanto no todas las columnas en un índice de almacén de columnas tienen diccionarios. Un diccionario puede ser un diccionario primario, para todos los segmentos, y posiblemente para otros diccionarios que se usan para un subconjunto de los segmentos de la columna.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Indica el identificador de partición. Es único en una base de datos.|  
|**hobt_id**|**bigint**|Identificador del montón o el índice de árbol b (hobt) para la tabla que contiene este índice de almacén de columnas.|  
|**column_id**|**int**|Identificador de la columna de almacén de columnas.|  
|**dictionary_id**|**int**|Identificador del diccionario.|  
|**version**|**int**|Versión del formato de diccionario.|  
|**type**|**int**|Tipo de diccionario:<br /><br /> 1 - diccionario que contiene de hash **int** valores<br /><br /> 2 - no utilizado<br /><br /> 3 - diccionario de hash que contiene los valores de cadena<br /><br /> 4 - diccionario que contiene de hash de **float** valores|  
|**last_id**|**int**|El último identificador de datos del diccionario.|  
|**entry_count**|**bigint**|Número de entradas en el diccionario.|  
|**on_disc_size**|**bigint**|Tamaño del diccionario en bytes.|  
|**pdw_node_id**|**int**|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
  
