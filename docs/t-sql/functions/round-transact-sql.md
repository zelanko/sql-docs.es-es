---
title: ROUND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6c1f1fe588447ba4fdbac3cdc66fcc17ea5a6508
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041229"
---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve un valor numérico, redondeado a la longitud o precisión especificadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de la categoría de tipos de datos numérico exacto o numérico aproximado, excepto para el tipo de datos **bit**.  
  
 *length*  
 Es la precisión con la que *numeric_expression* se va a redondear. *length* debe ser una expresión de tipo **tinyint**, **smallint** o **int**. Si *length* es un número positivo, *numeric_expression* se redondea al número de posiciones decimales especificado por *length*. Si *length* es un número negativo, *numeric_expression* se redondea al número de posiciones decimales especificado por *length*.  
  
 *function*  
 Es el tipo de operación que se va a realizar. *function* debe ser **tinyint**, **smallint** o **int**. Si *function* se omite o tiene el valor 0 (predeterminado), *numeric_expression* se redondea. Si se especifica un valor distinto de 0, *numeric_expression* se trunca.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve los tipos de datos siguientes.  
  
|Resultado de la expresión|Tipo de valor devuelto|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|Categorías **decimal** y **numeric** (p, s)|**decimal(p, s)**|  
|Categorías **money** y **smallmoney**|**money**|  
|Categorías **float** y **real**|**float**|  
  
## <a name="remarks"></a>Notas  
 ROUND siempre devuelve un valor. Si *length* es un valor negativo y mayor que el número de dígitos anteriores al separador decimal, ROUND devuelve 0.  
  
|Ejemplo|Resultado|  
|-------------|------------|  
|ROUND(748.58, -4)|0|  
  
 ROUND devuelve un valor de *numeric_expression* redondeado, independientemente del tipo de datos, cuando *length* es un número negativo.  
  
|Ejemplos|Resultado|  
|--------------|------------|  
|ROUND(748.58, -1)|750,00|  
|ROUND(748.58, -2)|700,00|  
|ROUND(748.58, -3)|Da como resultado un desbordamiento aritmético, porque 748.58 es de forma predeterminada decimal(5,2), que no puede devolver 1000.00.|  
|Para redondear a cuatro dígitos, cambie el tipo de datos de la entrada. Por ejemplo:<br /><br /> `SELECT ROUND(CAST (748.58 AS decimal (6,2)),-3);`|1000,00|  
  
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
----------  ----------
123.4500    100.00
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
  
## <a name="see-also"></a>Consulte también  
 [CEILING &#40;Transact-SQL&#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40;Transact-SQL&#41;](../../t-sql/functions/floor-transact-sql.md)   
 [Funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
