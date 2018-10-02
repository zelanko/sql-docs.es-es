---
title: + (Signo unario más) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- + (positive)
- +
- positive
dev_langs:
- TSQL
helpviewer_keywords:
- + (positive operator)
- positive operator (+)
- positive values [SQL Server]
ms.assetid: 0f31c5cc-3078-4f6a-9870-7eb1a98053fb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8752e76af293b50ee6eb086d86e71d02f3260d6d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813663"
---
# <a name="unary-operators---positive"></a>Operadores unarios: positivo
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el valor de una expresión numérica (un operador unario). Los operadores unarios realizan una operación sobre una única expresión de cualquiera de los tipos de datos de la categoría del tipo de datos numérico.   
  
|Operador|Significado|  
|--------------|-------------|  
|[+ (Positivo)](../../t-sql/language-elements/unary-operators-positive.md)|El valor numérico es positivo.|  
|[- (Negativo)](../../t-sql/language-elements/unary-operators-negative.md)|El valor numérico es negativo.|  
|[~ (NOT bit a bit)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|Devuelve los bits complementarios del número.|  
  
 Los operadores + (Positivo) y - (Negativo) se pueden utilizar en cualquier expresión de cualquiera de los tipos de datos de la categoría del tipo de datos numérico. El operador ~ (NOT bit a bit) solo se puede utilizar en expresiones de cualquiera de los tipos de datos de la categoría del tipo de datos entero.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
+ numeric_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Es cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) válida de cualquiera de los tipos de datos de la categoría de tipos de datos numéricos, excepto los tipos de datos **datetime** y **smalldatetime**.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos de *numeric_expression*.  
  
## <a name="remarks"></a>Notas  
 Aunque una suma unaria puede aparecer antes de cualquier expresión numérica, no realiza ninguna operación en el valor devuelto de la expresión. En concreto, no devolvería el valor positivo de una expresión negativa. Para devolver el valor positivo de una expresión negativa, use la función [ABS](../../t-sql/functions/abs-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-setting-a-variable-to-a-positive-value"></a>A. Establecer una variable en un valor positivo  
 En el siguiente ejemplo se establece una variable en un valor positivo.  
  
```  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = +123.45;  
SELECT @MyNumber;  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
-----------   
123.45            
  
(1 row(s) affected)  
```  
  
### <a name="b-using-the-unary-plus-operator-with-a-negative-value"></a>B. Usar el operador de suma unaria con un valor negativo  
 En el siguiente ejemplo se muestra el uso de la suma unaria con una expresión negativa y la función ABS() en la misma expresión negativa. La suma unaria no afecta a la expresión, pero la función ABS devuelve el valor positivo de la expresión.  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = -5;  
SELECT +@Num1, ABS(@Num1);  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
----------- -----------  
-5          5  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Ver también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  (Operadores [Transact-SQL])  
 [ABS &#40;Transact-SQL&#41;](../../t-sql/functions/abs-transact-sql.md)  
  
  
