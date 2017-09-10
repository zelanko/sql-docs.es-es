---
title: --(Comentario) (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a03aff79db25c07fc828145177e29196405a9264
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="---comment-transact-sql"></a>-- (Comentarios) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Indica texto proporcionado por el usuario. Los comentarios se pueden insertar en una línea independiente, anidada al final de una línea de comandos de [!INCLUDE[tsql](../../includes/tsql-md.md)] o dentro de una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] El servidor no evalúa el comentario.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>Argumentos  
 *text_of_comment*  
 Cadena de caracteres que contiene el texto del comentario.  
  
## <a name="remarks"></a>Comentarios  
 Use los dos guiones (--) para comentarios de una línea o anidados. Los comentarios que se insertan con dos guiones (--) se terminan con un carácter de nueva línea. No hay límite de longitud para los comentarios. En la tabla siguiente se enumeran los métodos abreviados de teclado que puede utilizar para acotar un texto como comentario o quitar los comentarios.  
  
|Acción|Standard|  
|------------|--------------|  
|Hacer un comentario al texto seleccionado|CTRL+K, CTRL+C|  
|Quitar un comentario del texto seleccionado|CTRL+K, CTRL+U|  
  
 Para obtener más información acerca de métodos abreviados de teclado, consulte [SQL Server Management Studio Keyboard Shortcuts](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
 Para comentarios de varias líneas, vea [barra diagonal estrella comentario &#40; Transact-SQL &#41; ](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se utilizan los caracteres -- de comentario.  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Lenguaje de control de flujo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

