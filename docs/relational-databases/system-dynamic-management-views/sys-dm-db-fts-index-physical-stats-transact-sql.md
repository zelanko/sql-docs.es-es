---
title: Sys.dm_db_fts_index_physical_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_fts_index_physical_stats_TSQL
- dm_db_fts_index_physical_stats
- dm_db_fts_index_physical_stats_TSQL
- sys.dm_db_fts_index_physical_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_fts_index_physical_stats dynamic management view
ms.assetid: 997c3278-3630-47f6-ada3-190b6c16ce0e
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 87496b0041b356f76bca28cd30cefa459f2c4f98
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbftsindexphysicalstats-transact-sql"></a>sys.dm_db_fts_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada índice semántico o de texto completo de cada tabla que tenga un índice semántico o de texto completo asociado.  
  
||||  
|-|-|-|  
|**Nombre de columna**|**Tipo**|**Description**|  
|**object_id**|int|Identificador de objeto de la tabla que contiene el índice.|  
|**fulltext_index_page_count**|**bigint**|Tamaño lógico de la extracción en número de páginas de índice.|  
|**keyphrase_index_page_count**|**bigint**|Tamaño lógico de la extracción en número de páginas de índice.|  
|**similarity_index_page_count**|**bigint**|Tamaño lógico de la extracción en número de páginas de índice.|  
  
## <a name="general-remarks"></a>Notas generales  
 Para obtener más información, consulte [administrar y supervisar la búsqueda semántica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información sobre el estado de la indización semántica, consulte las siguientes vistas de administración dinámica:  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="permissions"></a>Permissions

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo consultar el tamaño lógico de cada índice semántico o de texto completo en todas las tablas que tienen un índice semántico o de texto completo asociado:  
  
```  
SELECT * FROM sys.dm_db_fts_index_physical_stats;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Administrar y supervisar la búsqueda semántica](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
