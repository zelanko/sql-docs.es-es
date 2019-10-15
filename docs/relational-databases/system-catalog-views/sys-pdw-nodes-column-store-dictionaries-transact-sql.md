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
ms.openlocfilehash: 618a92cfd0f1602753b9fcfd61ac232eff5cecd4
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305186"
---
# <a name="syspdw_nodes_column_store_dictionaries-transact-sql"></a>sys.pdw_nodes_column_store_dictionaries (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada diccionario utilizado en los índices de almacén de columnas. Los diccionarios se usan para codificar algunos tipos de datos (no todos), por tanto no todas las columnas en un índice de almacén de columnas tienen diccionarios. Un diccionario puede ser un diccionario primario, para todos los segmentos, y posiblemente para otros diccionarios que se usan para un subconjunto de los segmentos de la columna.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Indica el identificador de partición. Es único en una base de datos.|  
|**hobt_id**|**bigint**|IDENTIFICADOR del índice de montículo o árbol B (HoBT) de la tabla que tiene este índice de almacén de columnas.|  
|**column_id**|**int**|Identificador de la columna de almacén de columnas.|  
|**dictionary_id**|**int**|Identificador del diccionario.|  
|**version**|**int**|Versión del formato de diccionario.|  
|**Tipo**|**int**|Tipo de diccionario:<br /><br /> 1: Diccionario hash que contiene valores **int**<br /><br /> 2: no se usa<br /><br /> 3: Diccionario hash que contiene valores de cadena<br /><br /> 4: Diccionario hash que contiene valores **float**|  
|**last_id**|**int**|El último identificador de datos del diccionario.|  
|**entry_count**|**bigint**|Número de entradas en el diccionario.|  
|**on_disc_size**|**bigint**|Tamaño del diccionario en bytes.|  
|**pdw_node_id**|**int**|Identificador único de un nodo [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW SERVER STATE`.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
  
