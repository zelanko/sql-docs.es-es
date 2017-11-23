---
title: Sys.dm_fts_index_keywords_by_property (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- dm_fts_index_keywords_by_property
- dm_fts_index_keywords_by_property_TSQL
- sys.dm_fts_index_keywords_by_property
- sys.dm_fts_index_keywords_by_property_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- search property lists [SQL Server], viewing keywords by property
- full-text search [SQL Server], viewing keywords
- sys.dm_fts_index_keywords_by_property dynamic management view
ms.assetid: fa41e052-a79a-4194-9b1a-2885f7828500
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a03bd54d417afae72ddc8d8f4221faf39472dfd2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmftsindexkeywordsbyproperty-transact-sql"></a>sys.dm_fts_index_keywords_by_property (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve todo el contenido relacionado con propiedades en el índice de texto completo de una tabla determinada. Esto incluye todos los datos que pertenecen a cualquier propiedad registrados por la lista de propiedades de búsqueda asociada a ese índice de texto completo.  
  
 Sys.dm_fts_index_keywords_by_property es una función de administración dinámica que le permite ver qué propiedades registradas han emitido IFilters en tiempo de índice, así como el contenido exacto de todas las propiedades de cada documento indizado.  
  
 **Para ver todo contenido de nivel de documento (incluido el contenido relacionado con la propiedad)**  
  
-   [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
 **Para ver la información de índice de texto completo de nivel superior**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
> [!NOTE]  
>  Para obtener información acerca de las listas de propiedades de búsqueda, vea [buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.dm_fts_index_keywords_by_property  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id ('*database_name*')  
 Una llamada a la [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) (función). Esta función acepta un nombre de base de datos y devuelve el identificador de base de datos, qué sys.dm_fts_index_keywords_by_property se usa para buscar la base de datos especificada. Si *database_name* es se omite, se devuelve el identificador de base de datos actual.  
  
 object_id ('*table_name*')  
 Una llamada a la [object_id ()](../../t-sql/functions/object-id-transact-sql.md) (función). Esta función acepta un nombre de tabla y devuelve el identificador de la tabla que contiene el índice de texto completo que se va a inspeccionar.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Columna|Data type|Description|  
|------------|---------------|-----------------|  
|palabra clave|**nvarchar(4000)**|Representación hexadecimal de la palabra clave que se almacena dentro del índice de texto completo.<br /><br /> Nota: OxFF representa el carácter especial que indica el final de un archivo o conjunto de datos.|  
|display_term|**nvarchar(4000)**|Formato legible de la palabra clave. Este formato se deriva del formato interno que se almacena en el índice de texto completo.<br /><br /> Nota: OxFF representa el carácter especial que indica el final de un archivo o conjunto de datos.|  
|column_id|**int**|Identificador de la columna en que la palabra clave actual forma parte del índice de texto completo.|  
|document_id|**int**|Identificador del documento o fila en que el término actual se indizó con texto completo. Este identificador corresponde al valor de clave de texto completo de ese documento o fila.|  
|property_id|**int**|Identificador de propiedad interno de la propiedad de búsqueda en el índice de texto completo de la tabla que especificó en el OBJECT_ID ('*table_name*') parámetro.<br /><br /> Cuando una propiedad determinada se agrega a una lista de propiedades de búsqueda, el servicio Motor de búsqueda de texto completo registra la propiedad y le asigna un identificador de propiedad interno que es específico de esa lista de propiedades. El identificador de propiedad interno, que es un entero, es único para una lista de propiedades de búsqueda determinada. Si una propiedad determinada se registra para varias listas de propiedades de búsqueda, se puede asignar un identificador de propiedad interno diferente para cada lista de propiedades de búsqueda.<br /><br /> Nota: El identificador de propiedad interno es distinto al identificador entero que se especifica al agregar la propiedad a la lista de propiedades de búsqueda. Para obtener más información, vea [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).<br /><br /> Para ver la asociación entre el identificador property_id y el nombre de propiedad:<br />                    [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista de administración dinámica puede responder preguntas como las siguientes:  
  
-   ¿Qué contenido se almacena en una determinada propiedad de un DocID específico?  
  
-   ¿Qué frecuencia tiene una determinada propiedad entre los documentos indizados?  
  
-   ¿Qué documentos contienen realmente una propiedad determinada? Todo esto resulta útil si al consultar una determinada propiedad de búsqueda, no se devuelve ninguno de los documentos que esperaba localizar.  
  
 Cuando la columna de clave de texto completo es un tipo de datos entero, como se recomienda, document_id se asigna directamente al valor de clave de texto completo de la tabla base.  
  
 Por el contrario, cuando la columna de clave de texto completo utiliza un tipo de datos que no es entero, document_id no representa la clave de texto completo en la tabla base. En este caso, para identificar la fila de la tabla base que se devuelve por dm_fts_index_keywords_by_property, necesita combinar esta vista con los resultados devueltos por [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md). Para poder combinarlos, debe almacenar la salida del procedimiento almacenado en una tabla temporal. A continuación, puede combinar la columna document_id de dm_fts_index_keywords_by_property con la columna DocId que es devuelto por este procedimiento almacenado. Tenga en cuenta que un **timestamp** columna no recibe valores durante la inserción, porque es generado automáticamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, la **timestamp** columna debe convertirse en **varbinary (8)** columnas. En el ejemplo siguiente se muestran estos pasos. En este ejemplo, *table_id* es el identificador de la tabla, *database_name* es el nombre de la base de datos y *table_name* es el nombre de la tabla.  
  
```  
USE database_name;  
GO  
CREATE TABLE #MyTempTable   
   (  
      docid INT PRIMARY KEY ,  
      [key] INT NOT NULL  
   );  
DECLARE @db_id int = db_id(N'database_name');  
DECLARE @table_id int = OBJECT_ID(N'table_name');  
INSERT INTO #MyTempTable EXEC sp_fulltext_keymappings @table_id;  
SELECT * FROM sys.dm_fts_index_keywords_by_property   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso SELECT en las columnas cubiertas por el índice de texto completo y permisos CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelven las palabras clave de la propiedad `Author` en el índice de texto completo de la tabla `Production.Document` de la base de datos de ejemplo `AdventureWorks`. En el ejemplo se utiliza el alias `KWBPOP` para la tabla devuelta por **sys.dm_fts_index_keywords_by_property**. El ejemplo utiliza las combinaciones internas para combinar columnas de [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) y [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
```  
-- Once the full-text index is configured to support property searching  
-- on the Author property, return any keywords indexed for this property.  
USE AdventureWorks2012;  
GO   
SELECT KWBPOP.* FROM   
   sys.dm_fts_index_keywords_by_property( DB_ID(),   
   object_id('Production.Document') ) AS KWBPOP  
   INNER JOIN  
      sys.registered_search_properties AS RSP ON(   
         (KWBPOP.property_id = RSP.property_id)   
         AND (RSP.property_name = 'Author') )  
   INNER JOIN  
      sys.fulltext_indexes AS FTI ON(   
         (FTI.[object_id] = object_id('Production.Document'))   
         AND (RSP.property_list_id = FTI.property_list_id) );  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)   
 [Mejorar el rendimiento de los índices de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [sp_fulltext_keymappings &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [Sys.dm_fts_index_keywords_by_document &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)   
 [Sys.dm_fts_index_keywords &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [Sys.registered_search_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [Sys.registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
