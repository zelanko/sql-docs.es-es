---
title: "&amp;(AND bit a bit) (Expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 06d2958e-66a5-44d8-8bc4-56209ebe1ff2
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6d5dad9457bbafe0218c1e71358d2c9c445f79a8
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="amp-bitwise-and-ssis-expression"></a>&amp;(AND bit a bit) (Expresión de SSIS)
  Lleva a cabo una operación AND bit a bit entre dos valores enteros. Compara cada bit del primer operando con el bit correspondiente del segundo operando. Si ambos bits son 1, el bit de resultado correspondiente se establece en 1. De lo contrario, se establece en 0.  
  
 Ambas condiciones deben ser de tipo entero con signo o de tipo entero sin signo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
integer_expression1 & integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression1, integer_expression2*  
 Cualquier expresión válida de tipo entero con o sin signo. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentarios  
 Si alguna de las condiciones es NULL, el resultado de la expresión será NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo realiza una operación AND bit a bit entre las columnas **NumberA** y **NumberB**. **NumberA** contiene 3 (0000011) y la columna **NumberB** contiene 7 (00000111).  
  
```  
NumberA & NumberB  
```  
  
 El resultado de evaluar la expresión es 3 (00000011).  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000011  
  
 Este ejemplo realiza una operación AND bit a bit entre las columnas **ReorderPoint** y **SafetyStockLevel** .  
  
```  
ReorderPoint & SafetyStockLevel  
```  
  
 Si el valor de **ReorderPoint** es 10 y el valor de **SafetyStockLevel** es 8, la expresión da como resultado 8 (00001000).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001000  
  
 Este ejemplo realiza una operación AND bit a bit entre dos enteros.  
  
```  
3 & 5   
```  
  
 El resultado de evaluar la expresión es 1 (00000001).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000001  
  
## <a name="see-also"></a>Vea también  
 [& & &#40; Operador lógico AND &#41; &#40; Expresión de SSIS &#41;](../../integration-services/expressions/logical-and-ssis-expression.md)   
 [Prioridad y asociatividad](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40; Expresión de SSIS &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

