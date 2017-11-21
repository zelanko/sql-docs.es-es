---
title: "Crear lista de propiedades de búsqueda (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SEARCH_PROPERTY_LIST_TSQL
- CREATE SEARCH
- CREATE_SEARCH_TSQL
- CREATE_SEARCH_PROPERTY_TSQL
- CREATE SEARCH PROPERTY
- CREATE SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], creating
- CREATE SEARCH PROPERTY LIST statement
ms.assetid: 5440cbb8-3403-4d27-a2f9-8e1f5a1bc12b
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b055be4f948b62553ddbabb40613971a0e5619d8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-search-property-list-transact-sql"></a>CREATE SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Crea una nueva lista de propiedades de búsqueda. Una lista de propiedades de búsqueda se utiliza para especificar una o más propiedades de búsqueda que desea incluir en un índice de texto completo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE SEARCH PROPERTY LIST new_list_name  
   [ FROM [ database_name. ] source_list_name ]  
   [ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *new_list_name*  
 Es el nombre de la nueva lista de propiedades de búsqueda. *new_list_name* es un identificador con un máximo de 128 caracteres. *new_list_name* debe ser único entre todas las listas de propiedades de la base de datos actual y cumplir las reglas para identificadores. *new_list_name* se utilizará cuando se crea el índice de texto completo.  
  
 *database_name*  
 Es el nombre de la base de datos en la lista de propiedades especificada por *source_list_name* se encuentra. Si no se especifica, *database_name* el valor predeterminado es la base de datos actual.  
  
 *database_name* debe especificar el nombre de una base de datos existente. El inicio de sesión para la conexión actual debe estar asociado con un identificador de usuario existente en la base de datos especificada por *database_name*. También debe disponer de los necesarios [permisos](#Permissions) en la base de datos.  
  
 *source_list_name*  
 Especifica que la lista de propiedades de nueva se crea copiando una lista de propiedades existente desde *database_name*. Si *source_list_name* no existe, se produce un error de CREATE SEARCH PROPERTY LIST con un error. Las propiedades de búsqueda *source_list_name* son heredadas por *new_list_name*.  
  
 AUTORIZACIÓN *owner_name*  
 Especifica el nombre de un usuario o rol que posea la lista de propiedades. *owner_name* debe ser el nombre de un rol de los cuales el usuario actual es un miembro o el usuario actual debe tener el permiso IMPERSONATE *owner_name*. Si no se especifica, la propiedad se otorga al usuario actual.  
  
> [!NOTE]  
>  El propietario puede modificarse mediante el uso de la [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.  
  
## <a name="remarks"></a>Comentarios  
  
> [!NOTE]  
>  Para obtener información acerca de la propiedad listas en general, vea [buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 De forma predeterminada, una nueva lista de propiedades de búsqueda está vacía y debe modificarla para agregar manualmente una o más propiedades de búsqueda. Opcionalmente, puede copiar una lista de propiedades de búsqueda existente. En este caso, la nueva lista hereda las propiedades de búsqueda de su origen, pero se puede modificar para agregar o quitar propiedades. Cualquier propiedad de la lista de propiedades de búsqueda en el momento del siguiente rellenado completo se incluye en el índice de texto completo.  
  
 Una instrucción CREATE SEARCH PROPERTY LIST da error en cualquiera de las condiciones siguientes:  
  
-   Si la base de datos especificada por *database_name* no existe.  
  
-   Si la lista especificada por *source_list_name* no existe.  
  
-   Si no tiene los permisos correctos.  
  
 **Para agregar o quitar propiedades de una lista**  
  
-   [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)  
  
-   **Para quitar una lista de propiedades**  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
##  <a name="Permissions"></a> Permisos  
 Requiere los permisos CREATE FULLTEXT CATALOG en la base de datos actual y los permisos REERENCES en cualquier base de datos de la que copie una lista de propiedades de origen.  
  
> [!NOTE]  
>  El permiso REFERENCES se necesita para asociar la lista a un índice de texto completo. El permiso CONTROL se exige para agregar y quitar propiedades o quitar la lista. El propietario de la lista de propiedades puede conceder los permisos REFERENCE o CONTROL en la lista. Los usuarios con el permiso CONTROL también pueden conceder el permiso REFERENCES a otros usuarios.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-an-empty-property-list-and-associating-it-with-an-index"></a>A. Crear una lista de propiedades vacía y asociarla a un índice  
 El siguiente ejemplo crea una nueva lista de propiedades de búsqueda denominada `DocumentPropertyList`. El ejemplo se utiliza un [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) instrucción que se va a asociar la nueva lista de propiedades con el índice de texto completo de la `Production.Document` tabla el `AdventureWorks` base de datos, sin iniciar un rellenado.  
  
> [!NOTE]  
>  Para obtener un ejemplo que se agrega varias propiedades de búsqueda predefinidas conocidas a esta lista de propiedades de búsqueda, vea [ALTER SEARCH PROPERTY LIST &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-search-property-list-transact-sql.md). Después de agregar las propiedades de búsqueda a la lista, el administrador de bases de datos necesitaría utilizar otra instrucción ALTER FULLTEXT INDEX con la cláusula START FULL POPULATION.  
  
```  
CREATE SEARCH PROPERTY LIST DocumentPropertyList;  
GO  
USE AdventureWorks2012;  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList  
   WITH NO POPULATION;   
GO   
```  
  
### <a name="b-creating-a-property-list-from-an-existing-one"></a>B. Crear una lista de propiedades desde otra existente  
 El siguiente ejemplo crea una nueva lista de propiedades de búsqueda, `JobCandidateProperties`, a partir de la lista creada en el ejemplo A, `DocumentPropertyList`, que se asocia a un índice de texto completo en la base de datos `AdventureWorks2012`. A continuación, el ejemplo utiliza una instrucción ALTER FULLTEXT INDEX para asociar la nueva lista de propiedades al índice de texto completo de la tabla `HumanResources.JobCandidate` en la base de datos `AdventureWorks2012`. Esta instrucción ALTER FULLTEXT INDEX inicia un rellenado completo, que es el comportamiento predeterminado de la cláusula SET SEARCH PROPERTY LIST.  
  
```  
CREATE SEARCH PROPERTY LIST JobCandidateProperties 
FROM AdventureWorks2012.DocumentPropertyList;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   SET SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [Sys.registered_search_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [Sys.registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [Sys.dm_fts_index_keywords_by_property &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Buscar GUID del conjunto de propiedades e identificadores de enteros de propiedad para las propiedades de búsqueda](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  

