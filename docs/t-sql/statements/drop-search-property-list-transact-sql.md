---
title: "QUITAR lista de propiedades de búsqueda (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SEARCH_PROPERTY_LIST_TSQL
- DROP SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- DROP SEARCH PROPERTY LIST statement
- search property lists [SQL Server], dropping
- search property lists [SQL Server], deleting
ms.assetid: 7c7ce52a-6b77-4a1c-9abf-d5feb664bea8
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 970fd636239f6de212d667ef6ec22edfa182859c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-search-property-list-transact-sql"></a>DROP SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Quita una lista de propiedades de la base de datos actual si la lista de propiedades de búsqueda no está asociada actualmente a ningún índice de texto completo de la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP SEARCH PROPERTY LIST property_list_name  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *property_list_name*  
 Es el nombre de la lista de propiedades de búsqueda que se va a quitar. *property_list_name* es un identificador.  
  
 Para ver los nombres de las listas de propiedades existente, use la [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) vista de catálogo como sigue:  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
## <a name="remarks"></a>Comentarios  
 No puede quitar una lista de propiedades de búsqueda de una base de datos mientras la lista está asociada a algún índice de texto completo y los intentos de hacerlo producirán un error. Para quitar una lista de propiedades de búsqueda de un índice de texto completo determinado, utilice la [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) (instrucción) y especifique la cláusula SET SEARCH PROPERTY LIST con OFF o el nombre de otra lista de propiedades de búsqueda.  
  
 **Para ver la propiedad listas en una instancia de servidor**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 **Para ver la propiedad listas asociados a los índices de texto completo**  
  
-   [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
 **Para quitar una lista de propiedades de un índice de texto completo**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Permisos  
 Se necesita el permiso CONTROL en la lista de propiedades de búsqueda.  
  
> [!NOTE]  
>  El propietario de la lista de propiedades puede conceder permisos CONTROL para la lista. De manera predeterminada, el usuario que crea una lista de propiedades de búsqueda es su propietario. El propietario puede modificarse mediante el uso de la [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita la lista de propiedades `JobCandidateProperties` de la base de datos `AdventureWorks2012`.  
  
```  
DROP SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [Crear lista de propiedades de búsqueda &#40; Transact-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Sys.registered_search_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [Sys.registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
  

