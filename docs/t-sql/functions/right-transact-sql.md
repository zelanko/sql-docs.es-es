---
title: DERECHA (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RIGHT_TSQL
- RIGHT
dev_langs:
- TSQL
helpviewer_keywords:
- rightmost character of expression
- RIGHT function
- character strings [SQL Server], RIGHT
ms.assetid: 43f1fe1f-aa18-47e3-ba20-e03e32254a6d
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 19dcdea078648b6ff41e08fcf82c9a4c705abe4c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="right-transact-sql"></a>RIGHT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la parte derecha de una cadena de caracteres con el número de caracteres especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
RIGHT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de caracteres o datos binarios. *character_expression* puede ser una constante, variable o columna. *character_expression* puede ser de cualquier tipo de datos, excepto **texto** o **ntext**, que se pueda convertir implícitamente a **varchar** o  **nvarchar**. De lo contrario, utilice la [conversión](../../t-sql/functions/cast-and-convert-transact-sql.md) función para convertir explícitamente *character_expression*.  
  
 *integer_expression*  
 Es un entero positivo que especifica cuántos caracteres de *character_expression* se devolverá. Si *integer_expression* es negativo, se devuelve un error. Si *integer_expression* es de tipo **bigint** y contiene un valor grande, *character_expression* debe ser de un tipo de datos de gran tamaño como **varchar (max)**.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve **varchar** cuando *character_expression* es un tipo de datos de caracteres no Unicode.  
  
 Devuelve **nvarchar** cuando *character_expression* es un tipo de datos de caracteres Unicode.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
 Al utilizar las intercalaciones de SC, la función RIGHT cuenta un par suplente UTF 16 como un carácter individual. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-right-with-a-column"></a>R: utilizar RIGHT con una columna  
 En el ejemplo siguiente se devuelven los cinco caracteres situados más a la derecha del nombre de cada persona de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT RIGHT(FirstName, 5) AS 'First Name'  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
First Name  
----------  
Ken  
Terri  
berto  
Rob  
  
(4 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>B. Utilizar RIGHT con una columna  
 El ejemplo siguiente devuelve los cinco caracteres situados más de cada apellido en el `DimEmployee` tabla.  
  
```  
-- Uses AdventureWorks  
  
SELECT RIGHT(LastName, 5) AS Name  
FROM dbo.DimEmployee  
ORDER BY EmployeeKey;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 ```
Name
-----
lbert
Brown
rello
lters
 ```  
  
### <a name="c-using-right-with-a-character-string"></a>C. Utilizar RIGHT con una cadena de caracteres  
 En el ejemplo siguiente se utiliza `RIGHT` para devolver los dos caracteres más a la derecha de la cadena de caracteres `abcdefg`.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) RIGHT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>Vea también  
 [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


