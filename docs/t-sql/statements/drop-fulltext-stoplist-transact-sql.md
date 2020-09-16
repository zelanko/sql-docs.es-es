---
description: DROP FULLTEXT STOPLIST (Transact-SQL)
title: DROP FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_STOPLIST_TSQL
- DROP FULLTEXT STOPLIST
dev_langs:
- TSQL
helpviewer_keywords:
- DROP FULLTEXT STOPLIST statement
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 3ee2a2bb-1dfb-4e7c-90e9-9d917cd84a15
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dd3cc4e5679a5f766f02d7630b3b760290203d43
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549321"
---
# <a name="drop-fulltext-stoplist-transact-sql"></a>DROP FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Quita una lista de palabras irrelevantes de texto completo de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST solo se admite para el nivel de compatibilidad 100 y posterior. Para los niveles de compatibilidad 80 y 90, la lista de palabras irrelevantes del sistema siempre se asigna a la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP FULLTEXT STOPLIST stoplist_name  
;  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *stoplist_name*  
 Es el nombre de la lista de palabras irrelevantes de texto completo que se va a quitar de la base de datos.  
  
## <a name="remarks"></a>Observaciones  
 DROP FULLTEXT STOPLIST produce un error si algún índice de texto completo hace referencia a la lista de palabras irrelevantes de texto completo que se va a quitar.  
  
## <a name="permissions"></a>Permisos  
 Para quitar una lista de palabras irrelevantes es necesario tener el permiso DROP en la lista de palabras irrelevantes o ser miembro de los roles fijos de base de datos **db_owner** o **db_ddladmin**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita una lista de palabras irrelevantes de texto completo denominada `myStoplist`.  
  
```  
DROP FULLTEXT STOPLIST myStoplist;  
```  
  
## <a name="see-also"></a>Consulte también  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
  
