---
title: STUFF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STUFF
- STUFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 10edb8b1b1e3008321bc03e2e65419dca8956f86
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  La función STUFF inserta una cadena en otra. Elimina una longitud determinada de caracteres de la primera cadena a partir de la posición de inicio y, a continuación, inserta la segunda cadena en la primera, en la posición de inicio.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de datos de caracteres. *character_expression* puede ser una constante, variable o columna de caracteres o datos binarios.  
  
 *start*  
 Es un valor entero que especifica la ubicación donde comienzan la eliminación y la inserción. Si *iniciar* es negativo o cero, se devuelve una cadena nula. Si *iniciar* es mayor que el primer *character_expression*, se devuelve una cadena nula. *iniciar* puede ser de tipo **bigint**.  
  
 *length*  
 Es un entero que especifica el número de caracteres que se elimina. Si *longitud* es negativo, se devuelve una cadena nula. Si *longitud* es mayor que el primer *character_expression*, elimina todo hasta el último carácter del último *character_expression*.  Si *longitud* es cero, se produce de inserción delante del primer carácter en la cadena. *longitud* puede ser de tipo **bigint**.

 *replaceWith_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de datos de caracteres. *character_expression* puede ser una constante, variable o columna de caracteres o datos binarios. Esta expresión reemplaza *longitud* caracteres de *character_expression* empezando por *iniciar*. Proporcionar `NULL` como el *replaceWith_expression*, quita los caracteres sin insertar nada.   
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve datos de caracteres si *character_expression* es uno de los tipos de datos de caracteres admitidos. Devuelve datos binarios si *character_expression* es uno de los tipos de datos binarios admitidos.  
  
## <a name="remarks"></a>Comentarios  
 Si la posición de inicio o la longitud es negativa, o si la posición de inicio es mayor que la longitud de la primera cadena, se devuelve una cadena NULL. Si la posición inicial es 0, se devuelve un valor NULL. Si la longitud que se va a eliminar es mayor que la primera cadena, se elimina hasta el primer carácter de la primera cadena.  

Si el valor resultante es mayor que el máximo admitido por el tipo devuelto, se genera un error.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
 Al utilizar intercalaciones de SC, ambos *character_expression* y *replaceWith_expression* pueden incluir pares suplentes. El parámetro de longitud contará cada suplente en *character_expression* como un único carácter.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve una cadena de caracteres creada eliminando tres caracteres de la primera cadena, `abcdef`, a partir de la posición `2` de `b`, e insertando la segunda cadena en el punto de eliminación.  
  
```  
SELECT STUFF('abcdef', 2, 3, 'ijklmn');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
aijklmnef   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
