---
title: sys.dm_db_fts_index_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2e80aef6d8a0ee33aa7a9a0d9bb71abc3ddf1e15
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742031"
---
# <a name="sysdmdbftsindexphysicalstats-transact-sql"></a>sys.dm_db_fts_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada índice semántico o de texto completo de cada tabla que tenga un índice semántico o de texto completo asociado.  
  
||||  
|-|-|-|  
|**Nombre de columna**|**Tipo**|**Descripción**|  
|**object_id**|INT|Identificador de objeto de la tabla que contiene el índice.|  
|**fulltext_index_page_count**|**bigint**|Tamaño lógico de la extracción en número de páginas de índice.|  
|**keyphrase_index_page_count**|**bigint**|Tamaño lógico de la extracción en número de páginas de índice.|  
|**similarity_index_page_count**|**bigint**|Tamaño lógico de la extracción en número de páginas de índice.|  
  
## <a name="general-remarks"></a>Notas generales  
 Para obtener más información, consulte [administrar y supervisar la búsqueda semántica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información sobre el estado de la indización semántica, consulte las siguientes vistas de administración dinámica:  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="permissions"></a>Permisos

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
  
  
