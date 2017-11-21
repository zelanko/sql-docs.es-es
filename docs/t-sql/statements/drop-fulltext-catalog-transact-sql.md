---
title: "QUITAR el catálogo de texto completo (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- DROP_FULLTEXT_CATALOG_TSQL
- DROP FULLTEXT CATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- dropping full-text catalogs
- removing full-text catalogs
- full-text catalogs [SQL Server], removing
- deleting full-text catalogs
- DROP FULLTEXT CATALOG statement
ms.assetid: b54efb0b-400b-49ce-923b-ce20a2a12255
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32445ba8410673168ffe8e7da61cdd1b37d71afe
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-fulltext-catalog-transact-sql"></a>DROP FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quita un catálogo de texto completo de una base de datos Debe quitar todos los índices de texto completo asociados con el catálogo antes de quitar el catálogo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP FULLTEXT CATALOG catalog_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *Catalog_Name*  
 Es el nombre del catálogo que se va a quitar. Si *catalog_name* no existe, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error y no lleva a cabo la operación de colocar. El grupo de archivos del catálogo de texto completo no debe estar marcado como OFFLINE ni READONLY para que el comando se ejecute correctamente.  
  
## <a name="permissions"></a>Permissions  
 Usuario debe tener el permiso DROP en el catálogo de texto completo o ser miembro de la **db_owner**, o **db_ddladmin** funciones fijas de base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Sys.fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [Crear catálogo de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)  
  
  

