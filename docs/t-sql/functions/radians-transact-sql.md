---
title: RADIANS (Transact-SQL) | Documentos de Microsoft
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
- RADIANS
- RADIANS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RADIANS function
ms.assetid: e9f69951-ecda-45d9-8909-dcb716b1b1c0
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 64c662ed806f5173c506756433318d589a42d4ea
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="radians-transact-sql"></a>RADIANS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve los radianes de una expresión numérica en grados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
RADIANS ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de exactos categoría de tipos de datos numéricos o numéricos aproximados excepto para la **bits** tipo de datos.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve el mismo tipo que *numeric_expression*.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-radians-to-show-00"></a>A. Utilizar RADIANS para mostrar 0.0  
 En este ejemplo se devuelve el resultado `0.0` debido a que la expresión numérica que se va a convertir en radianes es demasiado pequeña para la función `RADIANS`.  
  
```  
SELECT RADIANS(1e-307)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------   
0.0                        
(1 row(s) affected)  
```  
  
### <a name="b-using-radians-to-return-the-equivalent-angle-of-a-float-expression"></a>B. Utilizar RADIANS para devolver el ángulo equivalente de una expresión float  
 En este ejemplo se toma una expresión `float` y se devuelve el valor `RADIANS` del ángulo especificado.  
  
```  
-- First value is -45.01.  
DECLARE @angle float  
SET @angle = -45.01  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is -181.01.  
DECLARE @angle float  
SET @angle = -181.01  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is 0.00.  
DECLARE @angle float  
SET @angle = 0.00  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is 0.1472738.  
DECLARE @angle float  
SET @angle = 0.1472738  
SELECT 'The RADIANS of the angle is: ' +  
    CONVERT(varchar, RADIANS(@angle))  
GO  
-- Last value is 197.1099392.  
DECLARE @angle float  
SET @angle = 197.1099392  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------------------------   
The RADIANS of the angle is: -0.785573                        
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: -3.15922                         
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 0                                
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 0.00257041                       
 (1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 3.44022                          
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [decimal y numeric &#40; Transact-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [float y real &#40; Transact-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)   
 [int, bigint, smallint y tinyint &#40; Transact-SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)   
 [Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [Money y smallmoney &#40; Transact-SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
  
  


