---
title: sys.dm_fts_index_keywords_by_document (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_by_document_TSQL
- dm_fts_index_keywords_by_document_TSQL
- sys.dm_fts_index_keywords_by_document
- dm_fts_index_keywords_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- sys.dm_fts_index_keywords_by_document dynamic management function
- full-text search [SQL Server], viewing keywords
ms.assetid: 793b978b-c8a1-428c-90c2-a3e49d81b5c9
author: pmasl
ms.author: pelopes
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed1ebf610eafe5c882b2e19ed70129e0cac432fb
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944368"
---
# <a name="sysdmftsindexkeywordsbydocument-transact-sql"></a>sys.dm_fts_index_keywords_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Devuelve información sobre el contenido de nivel de documento de un índice de texto completo asociado a la tabla especificada.  
  
 sys.dm_fts_index_keywords_by_document es una función de administración dinámica.  
  
 **Para ver la información de índice de texto completo de nivel superior**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
 **Para ver información sobre el contenido de nivel de propiedad relacionados con una propiedad de documento**  
  
-   [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.dm_fts_index_keywords_by_document  
(   
    DB_ID('database_name'),     OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id('*database_name*')  
 Una llamada a la [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) función. Esta función acepta un nombre de base de datos y devuelve el identificador de base de datos, que sys.dm_fts_index_keywords_by_document utiliza para buscar la base de datos especificada. Si el parámetro *database_name* se omite, se devuelve el identificador de base de datos actual.  
  
 object_id('*table_name*')  
 Una llamada a la [object_id ()](../../t-sql/functions/object-id-transact-sql.md) función. Esta función acepta un nombre de tabla y devuelve el identificador de la tabla que contiene el índice de texto completo que se va a inspeccionar.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|columna|Data type|Descripción|  
|------------|---------------|-----------------|  
|palabra clave|**nvarchar(4000)**|Representación hexadecimal de la palabra clave que se almacena dentro del índice de texto completo.<br /><br /> Nota: OxFF representa el carácter especial que indica el final de un archivo o un conjunto de datos.|  
|display_term|**nvarchar(4000)**|Formato legible de la palabra clave. Este formato se deriva del formato interno que se almacena en el índice de texto completo.<br /><br /> Nota: OxFF representa el carácter especial que indica el final de un archivo o un conjunto de datos.|  
|column_id|**int**|Identificador de la columna en que la palabra clave actual forma parte del índice de texto completo.|  
|document_id|**int**|Identificador del documento o fila en que el término actual se indizó con texto completo. Este identificador corresponde al valor de clave de texto completo de ese documento o fila.|  
|occurrence_count|**int**|Número de repeticiones de la palabra clave actual en el documento o fila que se indica mediante **document_id**. Cuando '*search_property_name*' se especifica, occurrence_count sólo muestra el número de repeticiones de la palabra clave actual en la propiedad de búsqueda especificado en el documento o fila.|  
  
## <a name="remarks"></a>Comentarios  
 La información devuelta por sys.dm_fts_index_keywords_by_document es útil para averiguar lo siguiente, entre otras cosas:  
  
-   El número total de palabras clave que contiene un índice de texto completo.  
  
-   Si una palabra clave forma parte de un documento o fila determinados.  
  
-   Cuántas veces aparece una palabra clave en el índice de texto completo; es decir:  
  
     ([SUM](../../t-sql/functions/sum-transact-sql.md)(**occurrence_count**) WHERE **keyword**=*keyword_value* )  
  
-   Número de veces que una palabra clave aparece en un documento o fila determinados.  
  
-   Número de palabras clave contenidas en un documento o fila determinados.  
  
 Además, también puede utilizar la información proporcionada por sys.dm_fts_index_keywords_by_document para recuperar todas las palabras clave que pertenecen a un documento o fila determinados.  
  
 Cuando la columna de clave de texto completo es un tipo de datos entero, como se recomienda, document_id se asigna directamente al valor de clave de texto completo de la tabla base.  
  
 Por el contrario, cuando la columna de clave de texto completo utiliza un tipo de datos que no es entero, document_id no representa la clave de texto completo en la tabla base. En este caso, para identificar la fila en la tabla base que devuelve dm_fts_index_keywords_by_document, necesita combinar esta vista con los resultados devueltos por [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md). Para poder combinarlos, debe almacenar la salida del procedimiento almacenado en una tabla temporal. A continuación, puede combinar la columna document_id de dm_fts_index_keywords_by_document con la columna DocId que este procedimiento almacenado devuelve. Tenga en cuenta que un **timestamp** columna no recibe valores durante la inserción, porque es generado automáticamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, el **timestamp** columna debe convertirse a **varbinary (8)** columnas. En el ejemplo siguiente se muestran estos pasos. En este ejemplo, *table_id* es el identificador de la tabla, *database_name* es el nombre de la base de datos y *table_name* es el nombre de la tabla.  
  
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
SELECT * FROM sys.dm_fts_index_keywords_by_document   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso SELECT en las columnas cubiertas por el índice de texto completo y permisos CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-full-text-index-content-at-the-document-level"></a>A. Mostrar el contenido del índice de texto completo en el nivel de documento  
 En el ejemplo siguiente se muestra el contenido del índice de texto completo en el nivel de documento en la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks2012`.  
  
> [!NOTE]  
>  Puede crear este índice ejecutando el ejemplo proporcionado para el `HumanResources.JobCandidate` tabla [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_by_document(db_id('AdventureWorks'),   
object_id('HumanResources.JobCandidate'));  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de la búsqueda semántica y búsqueda de texto completo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [sp_fulltext_keymappings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [Mejorar el rendimiento de los índices de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
  
