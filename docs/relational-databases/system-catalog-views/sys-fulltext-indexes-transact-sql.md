---
title: Sys.fulltext_indexes (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fulltext_indexes
- fulltext_indexes_TSQL
- sys.fulltext_indexes_TSQL
- sys.fulltext_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_indexes catalog view
- full-text indexes [SQL Server], properties
ms.assetid: 7fc10fdc-370f-4927-bba0-b76108a7508e
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 50f7333cd6bce024b4b85c9068c413c17719cd21
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysfulltextindexes-transact-sql"></a>sys.fulltext_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila por índice de texto completo de un objeto tabular.  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto al que pertenece este índice de texto completo.|  
|**unique_index_id**|**int**|Identificador del índice único que no es de texto completo correspondiente que se utiliza para relacionar el índice de texto completo con las filas.|  
|**fulltext_catalog_id**|**int**|Identificador del catálogo de texto completo en el que reside el índice de texto completo.|  
|**is_enabled**|**bit**|1 = El índice de texto completo está habilitado actualmente.|  
|**change_tracking_state**|**char(1)**|Estado del seguimiento de cambios.<br /><br /> M = Manual<br /><br /> A = Automático<br /><br /> O = Desactivado|  
|**change_tracking_state_desc**|**nvarchar(60)**|Descripción del estado del seguimiento de cambios.<br /><br /> MANUAL<br /><br /> AUTO<br /><br /> OFF|  
|**has_crawl_completed**|**bit**|Último rastreo (rellenado) completado por el índice de texto completo.|  
|**crawl_type**|**char(1)**|Tipo de rastreo último o actual.<br /><br /> F = Rastreo completo<br /><br /> I = Rastreo basado en la marca de tiempo incremental<br /><br /> U = Actualización de rastreo, basado en notificaciones<br /><br /> P = Rastreo completo detenido|  
|**crawl_type_desc**|**nvarchar(60)**|Descripción del tipo de rastreo último o actual.<br /><br /> FULL_CRAWL<br /><br /> INCREMENTAL_CRAWL<br /><br /> UPDATE_CRAWL<br /><br /> PAUSED_FULL_CRAWL|  
|**crawl_start_date**|**datetime**|Inicio del rastreo último o actual.<br /><br /> NULL = Ninguno|  
|**crawl_end_date**|**datetime**|Fin del rastreo último o actual.<br /><br /> NULL = Ninguno|  
|**incremental_timestamp**|**binary (8)**|Valor de marca de tiempo que deberá utilizarse para el siguiente rastreo incremental.<br /><br /> NULL = Ninguno|  
|**stoplist_id**|**int**|Id. de la [lista de palabras irrelevantes](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) que está asociado a este índice de texto completo.|  
|**data_space_id**|**int**|Grupo de archivos donde reside este índice de texto completo.|  
|**property_list_id**|**int**|Identificador de la lista de propiedades de búsqueda asociada a este índice de texto completo. NULL indica que no hay ninguna lista de propiedades de búsqueda asociada al índice de texto completo. Para obtener más información acerca de esta lista de propiedades de búsqueda, use la [sys.registered_search_property_lists &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) vista de catálogo.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente usa un índice de texto completo en la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks2012`. En el ejemplo se devuelve el identificador de objeto de la tabla, el identificador de la lista de propiedades de búsqueda y el identificador de la lista de palabras irrelevantes usada por el índice de texto completo.  
  
> [!NOTE]  
>  En el ejemplo de código que crea este índice de texto completo, consulte la sección "Ejemplos" de [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT object_id, property_list_id, stoplist_id FROM sys.fulltext_indexes  
    where object_id = object_id('HumanResources.JobCandidate');   
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)   
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [Sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)   
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
