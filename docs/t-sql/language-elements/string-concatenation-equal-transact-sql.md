---
title: "+= (Concatenación de cadenas y asignación) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 12/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 70f37ef6816f5288c1d50240bf813a20ff33fae7
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="-string-concatenation-assignment-transact-sql"></a>+= (Asignación de concatenación de cadenas) (Transact-SQL)
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
  
 ```
 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
    
 Y       
 ------- 
 12000 
  
 (1 row(s) affected) 

 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
 Y       
 ------- 
 8000 
  
 (1 row(s) affected)
  ```   
   
## <a name="see-also"></a>Vea también  
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+= &#40;Add Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40;String Concatenation&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  
