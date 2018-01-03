---
title: Sys.stats_columns (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- stats_columns_TSQL
- stats_columns
- sys.stats_columns
- sys.stats_columns_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.stats_columns catalog view
ms.assetid: 93414d07-97e9-4501-8577-f35b8d68fbe9
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13114155ad4820ee293acdd11b7833083dafd9fc
ms.sourcegitcommit: c4633058216bcf6748db0eaa0e815761dc98c24d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2017
---
# <a name="sysstatscolumns-transact-sql"></a>sys.stats_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada columna que forma parte de **sys.stats** estadísticas.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. del objeto del que forma parte esta columna.|  
|**stats_id**|**int**|Id. de las estadísticas de las que forma parte esta columna.<br /><br />Si las estadísticas corresponden a un índice, el *stats_id* valor es el mismo que el *index_id* valor en el [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo.|  
|**stats_column_id**|**int**|Ordinal de base 1 del conjunto de columnas de estadísticas.|  
|**column_id**|**int**|Identificador de la columna de **sys.columns**.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
 [Estadísticas](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [Sys.dm_db_stats_histogram &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [Sys.Stats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)  
  
  
