---
title: CREAR FULLTEXT STOPLIST (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STOPLIST_TSQL
- FULLTEXT STOPLIST
- STOPLIST
- FULLTEXT_STOPLIST_TSQL
- CREATE FULLTEXT STOPLIST
- CREATE_FULLTEXT_STOPLIST_TSQL
dev_langs: TSQL
helpviewer_keywords:
- stoplists [full-text search]
- CREATE FULLTEXT STOPLIST statement
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 0669b1d0-46cc-4fac-8df7-5f7fa7af5db4
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1836d3f750b8c1ac75fd7ed6b9626e159d16eae3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="create-fulltext-stoplist-transact-sql"></a>CREATE FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea una nueva lista de palabras irrelevantes de texto completo en la base de datos actual.  
  
 Las palabras irrelevantes se administran en bases de datos mediante objetos denominados *listas de palabras irrelevantes*. Una lista de palabras irrelevantes es una lista de palabras que, cuando se asocia a un índice de texto completo, se aplica a las consultas de texto completo en ese índice. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST y DROP FULLTEXT STOPLIST solo se admiten para un nivel de compatibilidad de 100. En niveles de compatibilidad de 80 y 90, estas instrucciones no se admiten. Sin embargo, en todos los niveles de compatibilidad la lista de palabras irrelevantes del sistema se asocia automáticamente a los nuevos índices de texto completo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE FULLTEXT STOPLIST stoplist_name  
[ FROM { [ database_name.]source_stoplist_name } | SYSTEM STOPLIST ]  
[ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *stoplist_name*  
 Es el nombre de la lista de palabras irrelevantes. *stoplist_name* puede tener un máximo de 128 caracteres. *stoplist_name* debe ser único entre todas las listas de palabras irrelevantes en la base de datos actual y cumplir las reglas para identificadores.  
  
 *stoplist_name* se utilizará cuando se crea el índice de texto completo.  
  
 *database_name*  
 Es el nombre de la base de datos donde la lista de palabras irrelevantes especificada por *source_stoplist_name* se encuentra. Si no se especifica, *database_name* el valor predeterminado es la base de datos actual.  
  
 *source_stoplist_name*  
 Especifica que la nueva lista de palabras irrelevantes se crea copiando otra lista existente. Si *source_stoplist_name* no existe, o el usuario de base de datos no tiene los permisos correctos, CREATE FULLTEXT STOPLIST produce un error. Si alguno de los idiomas especificados en las palabras irrelevantes de la lista de palabras irrelevantes de origen no está registrado en la base de datos actual, CREATE FULLTEXT STOPLIST crea correctamente la lista, pero se devuelven advertencias y no se agregan las palabras irrelevantes correspondientes.  
  
 SYSTEM STOPLIST  
 Especifica que se crea la nueva lista de palabras irrelevantes de la lista de palabras irrelevantes que existe de forma predeterminada en el [base de datos Resource](../../relational-databases/databases/resource-database.md).  
  
 AUTORIZACIÓN *owner_name*  
 Especifica el nombre de una entidad de seguridad de base de datos como propietaria de la lista de palabras irrelevantes. *owner_name* debe ser el nombre de una entidad de seguridad de los cuales el usuario actual es un miembro o el usuario actual debe tener el permiso IMPERSONATE *owner_name*. Si no se especifica, la propiedad se otorga al usuario actual.  
  
## <a name="remarks"></a>Comentarios  
 El creador de la lista de palabras irrelevantes es su propietario.  
  
## <a name="permissions"></a>Permissions  
 Para crear una lista STOPLIST se requieren permisos CREATE FULLTEXT CATALOG. El propietario de la lista de palabras irrelevantes puede conceder explícitamente el permiso CONTROL para una lista de palabras irrelevantes para permitir a los usuarios agregar y quitar palabras, y quitar la lista de palabras irrelevantes.  
  
> [!NOTE]  
>  El uso de una lista de palabras irrelevantes con un índice de texto completo requiere el permiso REFERENCE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-new-full-text-stoplist"></a>A. Crear una lista de palabras irrelevantes de texto completo  
 En el ejemplo siguiente se crea una nueva lista de palabras irrelevantes de texto completo denominada `myStoplist`.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist;  
GO  
```  
  
### <a name="b-copying-a-full-text-stoplist-from-an-existing-full-text-stoplist"></a>B. Copiar una lista de palabras irrelevantes de texto completo a partir de una lista de palabras irrelevantes de texto completo existente  
 En el ejemplo siguiente se crea una lista de palabras irrelevantes de texto completo denominada `myStoplist2` copiando la lista de palabras irrelevantes de AdventureWorks denominada `Customers.otherStoplist`.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist2 FROM AdventureWorks.otherStoplist;  
GO  
```  
  
### <a name="c-copying-a-full-text-stoplist-from-the-system-full-text-stoplist"></a>C. Copiar una lista de palabras irrelevantes de texto completo a partir de la lista de palabras irrelevantes de texto completo del sistema  
 En el ejemplo siguiente se crea una lista de palabras irrelevantes de texto completo denominada `myStoplist3` copiando la lista de palabras irrelevantes del sistema.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist3 FROM SYSTEM STOPLIST;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Sys.fulltext_stoplists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [Sys.fulltext_stopwords &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
