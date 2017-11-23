---
title: Barra diagonal estrella (bloque de comentario) (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /*...*/_TSQL
- Comment
- /*...*/
dev_langs: TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- /*...*/ (comment)
- remarks [SQL Server]
- comments [SQL Server]
ms.assetid: 4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 60ae52af725a065a8319a2fde1e87e1b8bb52e02
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="slash-star-block-comment-transact-sql"></a>Barra diagonal estrella (bloque de comentario) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


  Indica texto proporcionado por el usuario. El texto situado entre el / * y \*/ no se evalúa por el servidor.  
  
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
  
## <a name="remarks"></a>Comentarios  
 Los comentarios se pueden insertar en una línea aparte o dentro de una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]. Comentarios de varias líneas deben indicarse con / * y \*/. Una regla de estilo que se utiliza a menudo para comentarios de varias líneas es comenzar la primera línea con /\*, las siguientes líneas con \* \*, una letra y terminar con \*/.  
  
 No hay límite de longitud para los comentarios.  
  
 Se admiten comentarios anidados. Si el / * patrón de carácter aparece en algún lugar dentro de un comentario existente, se trata como el inicio de un comentario anidado y, por lo tanto, requiere un cierre \*/ marca de comentario. Si no existe esta marca de comentario de cierre, se genera un error.  
  
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
  
## <a name="see-also"></a>Vea también  
 [--&#40; Comentario &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [Lenguaje de control de flujo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

