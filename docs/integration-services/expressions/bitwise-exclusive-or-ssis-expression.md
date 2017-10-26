---
title: "^ (Bit a bit OR exclusivo) (expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- bitwise exclusive OR (^)
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4c0a93affde5af98cdeb24fd04bb00d9ac72af7
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="-bitwise-exclusive-or-ssis-expression"></a>^ (OR exclusivo bit a bit) (expresión de SSIS)
  Lleva a cabo una operación OR exclusiva bit a bit entre dos valores enteros. Compara cada bit del primer operando con el bit correspondiente del segundo operando. Si un bit es 0 y el otro bit es 1, el bit de resultado correspondiente se establece en 1. Si ambos bits son 0, o bien si ambos bits son 1, el bit de resultado correspondiente se establece en 0.  
  
 Ambas condiciones deben ser de tipo entero con signo o de tipo entero sin signo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression1, integer_expression2*  
 Cualquier expresión válida de tipo entero con o sin signo. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentarios  
 Si alguna de las condiciones es NULL, el resultado de la expresión será NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo realiza una operación OR exclusiva bit a bit entre las variables **NumberA** y **NumberB**. **NumberA** contiene 3 (00000011) y **NumberB** contiene 7 (00000111).  
  
```  
@NumberA ^ @NumberB  
```  
  
 El resultado de evaluar la expresión es 4 (00000100).  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000100  
  
 Este ejemplo realiza una operación OR exclusiva bit a bit entre las columnas **ReorderPoint** y **SafetyStockLevel** .  
  
```  
ReorderPoint ^ SafetyStockLevel  
```  
  
 Si el valor de **ReorderPoint** es 10 y el de **SafetyStockLevel** es 8, la expresión da como resultado 2 (00000010).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00000010  
  
 Este ejemplo realiza una operación OR exclusiva bit a bit entre dos enteros.  
  
```  
3 ^ 5   
```  
  
 El resultado de evaluar la expresión es 6 (00000110).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000110  
  
## <a name="see-also"></a>Vea también  
 [&#124; &#124; &#40; Operador lógico OR &#41; &#40; Expresión de SSIS &#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [&#124; &#40; Bit a bit OR inclusivo &#41; &#40; Expresión de SSIS &#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [Prioridad y asociatividad](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40; Expresión de SSIS &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

