---
title: EXP (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- EXP_TSQL
- EXP
dev_langs:
- TSQL
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 5a9b8c52-6fb6-4e33-8b02-a878785b2f51
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 401560f260064a7d09ab2e34dde01a21aa655d9c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="exp-transact-sql"></a>EXP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el valor exponencial del elemento especificado **float** expresión.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
EXP ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de tipo **float** o de un tipo que pueda convertirse implícitamente a **float**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **float**  
  
## <a name="remarks"></a>Comentarios  
 La constante **e** (2,718281 …) es la base de los logaritmos naturales.  
  
 El exponente de un número es la constante **e** elevado a la potencia del número. Por ejemplo, EXP(1,0) = e^1,0 = 2,71828182845905 y EXP(10) = e^10 = 22026,4657948067.  
  
 El valor exponencial del logaritmo natural de un número es el número propio: EXP (registro (*n*)) =  *n* . Y el logaritmo natural del valor exponencial de un número es el número de sí misma: registro (EXP (*n*)) =  *n* .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-finding-the-exponent-of-a-number"></a>A. Obtener el exponente de un número  
 En el ejemplo siguiente se declara una variable y se devuelve el valor exponencial de la variable especificada (`10`) con una descripción de texto.  
  
```  
DECLARE @var float  
SET @var = 10  
SELECT 'The EXP of the variable is: ' + CONVERT(varchar,EXP(@var))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------------------------------  
The EXP of the variable is: 22026.5  
(1 row(s) affected)  
```  
  
### <a name="b-finding-exponentials-and-natural-logarithms"></a>B. Obtener valores exponenciales y logaritmos naturales  
 En el ejemplo siguiente se devuelve el valor exponencial del logaritmo natural de `20` y el logaritmo natural del valor exponencial de `20`. Dado que estas funciones son funciones inversas entre sí, el valor devuelto en ambos casos es `20`.  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------- ----------------------  
20                     20  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-finding-the-exponent-of-a-number"></a>C. Obtener el exponente de un número  
 En el ejemplo siguiente se devuelve el valor exponencial del valor especificado (`10`).  
  
```  
SELECT EXP(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------  
22026.4657948067  
```  
  
### <a name="d-finding-exponential-values-and-natural-logarithms"></a>D. Obtener valores exponenciales y logaritmos naturales  
 En el ejemplo siguiente se devuelve el valor exponencial del logaritmo natural de `20` y el logaritmo natural del valor exponencial de `20`. Dado que estas funciones son funciones inversas entre sí, el valor devuelto en ambos casos es `20`.  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------- -----------------  
20                  20  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [Registro &#40; Transact-SQL &#41;](../../t-sql/functions/log-transact-sql.md)   
 [LOG10 &#40; Transact-SQL &#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  

