---
title: "+= (Concatenación de cadenas) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 12/07/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c557bcc1d3c2f314ce57e93701b11833f5a6fc6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="string-concatenation---equal-transact-sql"></a>Concatenación de cadenas: igual (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concatena dos cadenas y establece como valor de la cadena el resultado de la operación. Por ejemplo, si una variable @x es igual a 'Adventure', a continuación, @x += '´Works' toma el valor original de @x, agrega 'Works' a la cadena y establece @x en el nuevo valor 'AdventureWorks'.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquiera de los tipos de datos de caracteres.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos que se define para la variable.  
  
## <a name="remarks"></a>Comentarios  
 ESTABLECER @v1 += 'expression' es equivalente a conjunto @v1 = @v1 + ('expression'). Además, establece @v1 = @v2 + @v3 + @v4 es equivalente a conjunto @v1 = (@v2 + @v3) + @v4.  
  
 El operador += no se puede utilizar sin una variable. Por ejemplo, el código siguiente provocará un error:  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>Ejemplos  
### <a name="a-concatenation-using--operator"></a>A. Concatenación con += (operador)
 En el siguiente ejemplo se concatena con el operador `+=`.  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>B. Orden de evaluación al concatenar utilizando += (operador)
En el ejemplo siguiente se concatena varias cadenas para formar una cadena larga y, a continuación, intenta calcular la longitud de la cadena final. Este ejemplo muestra las reglas de truncamiento y orden de evaluación, al usar el operador de concatenación. 

```
DECLARE @x varchar(4000) = replicate('x', 4000)
DECLARE @z varchar(8000) = replicate('z',8000)
DECLARE @y varchar(max);
 
SET @y = '';
SET @y += @x + @z;
SELECT LEN(@y) AS Y; -- 8000
 
SET @y = '';
SET @y = @y + @x + @z;
SELECT LEN(@y) AS Y; -- 12000
 
SET @y = '';
SET @y = @y +(@x + @z);
SELECT LEN(@y) AS Y; -- 8000
-- or
SET @y = '';
SET @y = @x + @z + @y;
SELECT LEN(@y) AS Y; -- 8000
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Y      `  
  
 `-------`  
  
 `8000`  
  
  `(1 row(s) affected)` 
  
    
  `Y      `  
  
 `-------`  
  
 `12000`  
  
  `(1 row(s) affected)` 

`Y      `  
  
 `-------`  
  
 `8000`  
  
  `(1 row(s) affected)` 
  
    
  `Y      `  
  
 `-------`  
  
 `8000`  
  
  `(1 row(s) affected)`   
   
## <a name="see-also"></a>Vea también  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+= &#40; Agregar es igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40; Concatenación de cadenas &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  

