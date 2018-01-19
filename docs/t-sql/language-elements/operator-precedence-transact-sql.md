---
title: Precedencia de operadores (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- operators [Transact-SQL], precedence
- operator precedence [Transact-SQL]
- order of operator execution [Transact-SQL]
- precedence [SQL Server], operators
ms.assetid: f04d2439-6fff-4e4c-801f-cc62faef510a
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b1208137b82bf64a6b48a7d6f2db2bc681a7d7f6
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="operator-precedence-transact-sql"></a>Prioridad de operador (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cuando una expresión compleja tiene múltiples operadores, la prioridad de operador determina la secuencia en que se realiza la operación. El orden de ejecución puede afectar de manera significativa al valor resultante.  
  
 Los operadores tienen los niveles de prioridad que se muestran en la siguiente tabla. Un operador de los niveles más altos se evalúa antes que un operador de un nivel más bajo.  
  
|Nivel|Operadores|  
|-----------|---------------|  
|1|~ (operador bit a bit NOT)|  
|2|* (Multiplicar), / (dividir), % (módulo)|  
|3|+ (Positivo), - (negativo), + (suma), (+ concatenación),-(resta), & (AND bit a bit), ^ (bit a bit OR exclusivo), &#124; (OR bit a bit)|  
|4|=, >, \<, > =, < =, <>,! =,! >,! < (operadores de comparación)|  
|5|NOT|  
|6|y|  
|7|ALL, ANY, BETWEEN, IN, LIKE, OR, SOME|  
|8|= (asignación)|  
  
 Cuando en una expresión dos operadores tengan el mismo nivel de prioridad de operador, se evalúan de izquierda a derecha en función de su posición dentro de la expresión. Por ejemplo, en la expresión utilizada en la siguiente instrucción `SET`, el operador de resta se evalúa antes que el operador de suma.  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 4 - 2 + 27;  
-- Evaluates to 2 + 27 which yields an expression result of 29.  
SELECT @MyNumber;  
```  
  
 Utilice paréntesis para suplantar la prioridad definida de los operadores en una expresión. Todo lo que está dentro del paréntesis se evalúa en primer lugar para producir un valor antes de que dicho valor lo pueda utilizar cualquier otro operador que se encuentre fuera del paréntesis.  
  
 Por ejemplo, en la expresión utilizada en la siguiente instrucción `SET`, el operador de multiplicación tiene una prioridad mayor que el operador de suma. Por lo tanto, se evalúa antes; el resultado de la expresión es `13`.  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * 4 + 5;  
-- Evaluates to 8 + 5 which yields an expression result of 13.  
SELECT @MyNumber;  
```  
  
 En la expresión utilizada en la siguiente instrucción `SET`, el paréntesis hace que primero se lleve a cabo la suma. El resultado de la expresión es `18`.  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + 5);  
-- Evaluates to 2 * 9 which yields an expression result of 18.  
SELECT @MyNumber;  
```  
  
 Si una expresión tiene paréntesis anidados, se evalúa primero la expresión más anidada. El siguiente ejemplo contiene paréntesis anidados, con la expresión `5 - 3` en el conjunto de paréntesis más anidado. Esta expresión produce un valor de `2`. Entonces, el operador de suma (`+`) suma este resultado a `4`. Esto produce un valor de `6`. Finalmente, `6` se multiplica por `2` para producir un resultado de expresión de `12`.  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + (5 - 3) );  
-- Evaluates to 2 * (4 + 2) which then evaluates to 2 * 6, and   
-- yields an expression result of 12.  
SELECT @MyNumber;  
```  
  
## <a name="see-also"></a>Vea también  
 [Operadores lógicos &#40; Transact-SQL &#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
