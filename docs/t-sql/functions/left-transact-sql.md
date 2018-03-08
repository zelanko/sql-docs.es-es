---
title: LEFT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
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
- LEFT
- LEFT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- character strings [SQL Server], LEFT
- characters [SQL Server], leftmost
- LEFT function
- leftmost character of expression
ms.assetid: 44a8c71b-63d8-458b-8b5d-99d570067c3c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 822680e5939e628b17c15d08c3cb513ad9b348ed
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="left-transact-sql"></a>LEFT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la parte izquierda de una cadena de caracteres con el número de caracteres especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
LEFT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de caracteres o datos binarios. *character_expression* puede ser una constante, variable o columna. *character_expression* puede ser de cualquier tipo de datos, excepto **texto** o **ntext**, que se pueda convertir implícitamente a **varchar** o  **nvarchar**. De lo contrario, utilice la [conversión](../../t-sql/functions/cast-and-convert-transact-sql.md) función para convertir explícitamente *character_expression*.  
  
 *integer_expression*  
 Es un entero positivo que especifica cuántos caracteres de la *character_expression* se devolverá. Si *integer_expression* es negativo, se devuelve un error. Si *integer_expression* es de tipo **bigint** y contiene un valor grande, *character_expression* debe ser de un tipo de datos de gran tamaño como **varchar (max)**.  
  
 El *integer_expression* parámetro cuenta un carácter de suplente de UTF-16 como un solo carácter.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve **varchar** cuando *character_expression* es un tipo de datos de caracteres no Unicode.  
  
 Devuelve **nvarchar** cuando *character_expression* es un tipo de datos de caracteres Unicode.  
  
## <a name="remarks"></a>Comentarios  
 Al utilizar intercalaciones de SC, el *integer_expression* parámetro cuenta un par suplente de UTF-16 como un solo carácter. Para más información, consulte [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-left-with-a-column"></a>A. Utilizar LEFT con una columna  
 En el ejemplo siguiente se devuelven los cinco caracteres situados más a la izquierda de cada nombre de producto de la tabla `Product` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT LEFT(Name, 5)   
FROM Production.Product  
ORDER BY ProductID;  
GO  
```  
  
### <a name="b-using-left-with-a-character-string"></a>B. Utilizar LEFT con una cadena de caracteres  
 En el ejemplo siguiente se utiliza `LEFT` para devolver los dos caracteres situados más a la izquierda de la cadena de caracteres `abcdefg`.  
  
```  
SELECT LEFT('abcdefg',2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab   
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-left-with-a-column"></a>C. Utilizar LEFT con una columna  
 En el ejemplo siguiente se devuelven los cinco caracteres situados más a la izquierda de cada nombre de producto.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT(EnglishProductName, 5)   
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="d-using-left-with-a-character-string"></a>D. Utilizar LEFT con una cadena de caracteres  
 En el ejemplo siguiente se utiliza `LEFT` para devolver los dos caracteres situados más a la izquierda de la cadena de caracteres `abcdefg`.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab  
```  
  
## <a name="see-also"></a>Vea también  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

