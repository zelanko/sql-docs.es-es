---
title: ^ (OR exclusivo bit a bit) (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- bitwise exclusive OR (^)
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b5153a210c1d276b481cea240e1f28b77751ad4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769511"
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
 Cualquier expresión válida de tipo entero con o sin signo. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
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
 [&#124;&#124; &#40;Operador OR lógico&#41; &#40;expresión de SSIS&#41;](logical-or-ssis-expression.md)   
 [&#124; &#40;OR inclusivo bit a bit&#41; &#40;expresión de SSIS&#41;](bitwise-inclusive-or-ssis-expression.md)   
 [Precedencia y capacidad de asociación de operadores](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
