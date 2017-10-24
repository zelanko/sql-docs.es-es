---
title: ROUND (Transact-SQL) | Documentos de Microsoft
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
- ROUND_TSQL
- ROUND
dev_langs:
- TSQL
helpviewer_keywords:
- rounding expressions
- ROUND function [Transact-SQL]
ms.assetid: 23921ed6-dd6a-4c9e-8c32-91c0d44fe4b7
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: cba8b5a9b62a21fc810ff9bb5fcd3d0c6429f9f5
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un valor numérico, redondeado a la longitud o precisión especificadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ROUND (numeric_expression , length )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de exactos categoría de tipos de datos numéricos o numéricos aproximados excepto para la **bits** tipo de datos.  
  
 *length*  
 Es la precisión con que *numeric_expression* se redondea. *longitud* debe ser una expresión de tipo **tinyint**, **smallint**, o **int**. Cuando *longitud* es un número positivo, *numeric_expression* se redondea al número de posiciones decimales que especifica *longitud*. Cuando *longitud* es un número negativo, *numeric_expression* se redondea a la izquierda del separador decimal, según lo especificado por *longitud*.  
  
 *function*  
 Es el tipo de operación que se va a realizar. *función* debe ser **tinyint**, **smallint**, o **int**. Cuando *función* se omite o tiene un valor de 0 (valor predeterminado), *numeric_expression* se redondea. Si especifica un valor distinto de 0 es, *numeric_expression* se trunca.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve los tipos de datos siguientes.  
  
|Resultado de la expresión|Tipo de valor devuelto|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|**decimal** y **numérico** categoría (p, s)|**decimal (p, s)**|  
|**Money** y **smallmoney** categoría|**money**|  
|**float** y **real** categoría|**float**|  
  
## <a name="remarks"></a>Comentarios  
 ROUND siempre devuelve un valor. Si *longitud* es negativo y mayor que el número de dígitos que hay delante del separador decimal, ROUND devuelve 0.  
  
|Ejemplo|Resultado|  
|-------------|------------|  
|ROUND (748.58, -4)|0|  
  
 ROUND devuelve un redondeado *numeric_expression*, independientemente del tipo de datos, cuando *longitud* es un número negativo.  
  
|Ejemplos|Resultado|  
|--------------|------------|  
|ROUND (748.58, -1)|750.00|  
|ROUND (748.58, -2)|700.00|  
|ROUND(748.58, -3)|Da como resultado un desbordamiento aritmético, porque 748.58 es de forma predeterminada decimal(5,2), que no puede devolver 1000.00.|  
|Para redondear a cuatro dígitos, cambie el tipo de datos de la entrada. Por ejemplo:<br /><br /> `SELECT ROUND(CAST (748.58 AS decimal (6,2)),-3);`|1000.00|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-round-and-estimates"></a>A. Usar ROUND y valores estimados  
 En el ejemplo siguiente se muestran dos expresiones que demuestran que cuando se usa la función `ROUND`, el último dígito siempre es un valor estimado.  
  
```  
SELECT ROUND(123.9994, 3), ROUND(123.9995, 3);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -----------  
123.9990    124.0000      
```  
  
### <a name="b-using-round-and-rounding-approximations"></a>B. Usar ROUND y aproximaciones de redondeo  
 En el ejemplo siguiente se muestran redondeos y aproximaciones.  
  
```  
SELECT ROUND(123.4545, 2), ROUND(123.45, -2);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ----------
123.45    100.00
```
  
### <a name="c-using-round-to-truncate"></a>C. Usar ROUND para truncar  
 En el ejemplo siguiente se utilizan dos instrucciones `SELECT` para demostrar la diferencia entre redondear y truncar. La primera instrucción redondea el resultado. La segunda instrucción lo trunca.  
  
```  
SELECT ROUND(150.75, 0);  
GO  
SELECT ROUND(150.75, 0, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
151.00  
  
(1 row(s) affected)  
  
--------  
150.00  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-round-and-estimates"></a>D. Usar ROUND y valores estimados  
 En el ejemplo siguiente se muestran dos expresiones que demuestran que cuando se usa la función `ROUND`, el último dígito siempre es un valor estimado.  
  
```  
SELECT ROUND(123.994999, 3), ROUND(123.995444, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ---------
123.995000    123.995444
```
  
## <a name="see-also"></a>Vea también  
 [CEILING &#40; Transact-SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40; Transact-SQL &#41;](../../t-sql/functions/floor-transact-sql.md)   
 [Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


