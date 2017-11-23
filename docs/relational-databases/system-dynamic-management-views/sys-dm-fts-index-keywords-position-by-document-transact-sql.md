---
title: Sys.dm_fts_index_keywords_position_by_document (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document
- sys.dm_fts_index_keywords_position_by_document
dev_langs: TSQL
helpviewer_keywords: sys.dm_fts_index_keywords_position_by_document dynamic management view
ms.assetid: 0d70184f-baa2-411b-a32d-a4c5af890edd
caps.latest.revision: "5"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c9fc96c8db1521ac99601312869146290a622147
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmftsindexkeywordspositionbydocument-transact-sql"></a>Sys.dm_fts_index_keywords_position_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve información de posición de la palabra clave en los documentos indizados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id ('*database_name*')  
 Una llamada a la [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) (función). Esta función acepta un nombre de base de datos y devuelve el identificador de base de datos, qué sys.dm_fts_index_keywords_position_by_document se usa para buscar la base de datos especificada.  
  
 object_id ('*table_name*')  
 Una llamada a la [object_id ()](../../t-sql/functions/object-id-transact-sql.md) (función). Esta función acepta un nombre de tabla y devuelve el identificador de la tabla que contiene el índice de texto completo que se va a inspeccionar.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Columna|Data type|Description|  
|------------|---------------|-----------------|  
|palabra clave|**varbinary(128)**|Que representa la palabra clave de cadena binaria.|  
|display_term|**nvarchar(4000)**|Formato legible de la palabra clave. Este formato se deriva del formato interno que se almacena en el índice de texto completo.|  
|column_id|**int**|Identificador de la columna en que la palabra clave actual forma parte del índice de texto completo.|  
|document_id|**bigint**|Identificador del documento o fila en que el término actual se indizó con texto completo. Este identificador corresponde al valor de clave de texto completo de ese documento o fila.|  
|position|**int**|La posición de la palabra clave en el documento.|  
  
## <a name="remarks"></a>Comentarios  
 Use la DMV para identificar la ubicación de las palabras indizadas en los documentos indizados. Esta DMV puede utilizarse para solucionar problemas cuando **sys.dm_fts_index_keywords_by_document** indica las palabras están en el índice de texto completo, pero al ejecutar una consulta con esas palabras, no se devuelve el documento.  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso SELECT en las columnas cubiertas por el índice de texto completo y permisos CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve las palabras clave del índice de texto completo de la `Production.Document` tabla de la `AdventureWorks` base de datos de ejemplo.  
  
```  
USE AdventureWorks2012;  
GO   
  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
);   
GO  
```  
  
 Puede agregar un predicado en el otro columns_id como se muestra en la siguiente consulta de ejemplo, para aislar aún más las ubicaciones.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>Vea también  
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)   
 [Mejorar el rendimiento de los índices de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [Búsqueda de texto completo y funciones de búsqueda semántica &#40; Transact-SQL &#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [Funciones y vistas de administración dinámica de la búsqueda semántica y búsqueda de texto completo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Búsquedas de texto completo y semántica almacenan procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
