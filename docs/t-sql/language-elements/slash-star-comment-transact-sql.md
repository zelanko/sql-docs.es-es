---
title: Barra diagonal y asterisco (comentario de bloque) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- /*...*/_TSQL
- Comment
- /*...*/
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- /*...*/ (comment)
- remarks [SQL Server]
- comments [SQL Server]
ms.assetid: 4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 662aaa76f7af8a45513219af63c66fe3a65bede6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65981651"
---
# <a name="slash-star-block-comment-transact-sql"></a>Barra diagonal y asterisco (comentario de bloque) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


  Indica texto proporcionado por el usuario. El servidor no evalúa el texto situado entre /* y \*/.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
/*  
text_of_comment  
*/  
```  
  
## <a name="arguments"></a>Argumentos  
 *text_of_comment*  
 Es el texto del comentario. Es una o más cadenas de caracteres.  
  
## <a name="remarks"></a>Notas  
 Los comentarios se pueden insertar en una línea aparte o dentro de una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]. Los comentarios con varias líneas deben indicarse con /* y \*/. Una regla de estilo que se usa a menudo para los comentarios de varias líneas es comenzar la primera línea con /\*, las siguientes con \*\* y finalizar con \*/.  
  
 No hay límite de longitud para los comentarios.  
  
 Se admiten comentarios anidados. Si el patrón de carácter /* aparece en algún lugar de un comentario existente, se trata como el comienzo de un comentario anidado y, por tanto, requiere una marca de comentario de cierre \*/. Si no existe esta marca de comentario de cierre, se genera un error.  
  
 Por ejemplo, el código siguiente genera un error.  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/   
SELECT @@VERSION;  
GO   
```  
  
 Para solucionar este error, realice el cambio siguiente.  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/ */  
SELECT @@VERSION;  
GO  
  
```  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utilizan comentarios para explicar la finalidad de la sección del código.  
  
```  
USE AdventureWorks2012;  
GO  
/*  
This section of the code joins the Person table with the Address table,   
by using the Employee and BusinessEntityAddress tables in the middle to   
get a list of all the employees in the AdventureWorks2012 database   
and their contact information.  
*/  
SELECT p.FirstName, p.LastName, a.AddressLine1, a.AddressLine2, a.City, a.PostalCode  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e ON p.BusinessEntityID = e.BusinessEntityID   
JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
JOIN Person.Address AS a ON ea.AddressID = a.AddressID;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [-- &#40;Comment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [Lenguaje de control de flujo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

