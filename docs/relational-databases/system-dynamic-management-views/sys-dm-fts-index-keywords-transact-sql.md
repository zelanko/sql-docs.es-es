---
title: Sys. dm_fts_index_keywords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_index_keywords
- sys.dm_fts_index_keywords
- sys.dm_fts_index_keywords_TSQL
- dm_fts_index_keywords_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords dynamic management function
- full-text search [SQL Server], viewing keywords
- troubleshooting [SQL Server], full-text search
ms.assetid: fce7b2a1-7e74-4769-86a8-c77c7628decd
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 3b95ce96f126249da124ea5830e7cc898fa9f8b6
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898857"
---
# <a name="sysdm_fts_index_keywords-transact-sql"></a>sys.dm_fts_index_keywords (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve información sobre el contenido de un índice de texto completo para la tabla especificada.  
  
 **Sys. dm_fts_index_keywords** es una función de administración dinámica.  
  
> [!NOTE]  
>  Para ver la información del índice de texto completo de nivel inferior, use la función de administración dinámica [Sys. dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md) en el nivel de documento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.dm_fts_index_keywords( DB_ID('database_name'), OBJECT_ID('table_name') )  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id ('*database_name*')  
 Una llamada a la función [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) . Esta función acepta un nombre de base de datos y devuelve el identificador de base de datos, que **Sys. dm_fts_index_keywords** usa para encontrar la base de datos especificada. Si el parámetro *database_name* se omite, se devuelve el identificador de base de datos actual.  
  
 object_id ('*TABLE_NAME*')  
 Una llamada a la función [OBJECT_ID ()](../../t-sql/functions/object-id-transact-sql.md) . Esta función acepta un nombre de tabla y devuelve el identificador de la tabla que contiene el índice de texto completo que se va a inspeccionar.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**keyword**|**nvarchar(4000)**|Representación hexadecimal de la palabra clave almacenada en el índice de texto completo.<br /><br /> Nota: OxFF representa el carácter especial que indica el final de un archivo o conjunto de archivos.|  
|**display_term**|**nvarchar(4000)**|Formato legible de la palabra clave. Este formato se deriva del formato hexadecimal.<br /><br /> Nota: el valor de **display_term** para OxFF es "final de archivo".|  
|**column_id**|**int**|Identificador de la columna en que la palabra clave actual forma parte del índice de texto completo.|  
|**document_count**|**int**|Número de documentos o filas que contienen el término actual.|  
  
## <a name="remarks"></a>Comentarios  
 La información devuelta por **Sys. dm_fts_index_keywords** es útil para averiguar lo siguiente, entre otras cosas:  
  
-   Si una palabra clave forma parte del índice de texto completo.  
  
-   Cuántos documentos o filas contienen una palabra clave determinada.  
  
-   La palabra clave más común en el índice de texto completo:  
  
    -   **document_count** de cada *keyword_value* en comparación con el total **document_count**, el recuento de documentos de 0xFF.  
  
    -   Normalmente, es probable que sea adecuado declarar las palabras clave comunes como palabras irrelevantes.  
  
> [!NOTE]  
>  El **document_count** devuelto por **Sys. dm_fts_index_keywords** puede ser menos preciso para un documento específico que el número devuelto por **Sys. Dm_fts_index_keywords_by_document** o una consulta **Contains** . Se calcula que esta posible imprecisión es inferior a un uno por ciento. Esta inexactitud puede producirse porque un **document_id** se puede contar dos veces cuando continúa en varias filas del fragmento de índice o cuando aparece más de una vez en la misma fila. Para obtener un recuento más preciso para un documento específico, use **Sys. dm_fts_index_keywords_by_document** o una consulta **Contains** .  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-high-level-full-text-index-content"></a>A. Mostrar el contenido del índice de texto completo de alto nivel  
 En el ejemplo siguiente se muestra información sobre el contenido de alto nivel del índice de texto completo en la tabla `HumanResources.JobCandidate`.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords(db_id('AdventureWorks2012'), object_id('HumanResources.JobCandidate'))  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones y vistas de administración dinámica de la búsqueda de texto completo y la búsqueda semántica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
