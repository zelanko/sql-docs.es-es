---
title: '| (OR inclusivo bit a bit) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3f7a092b8ad649285417ee7961ac891b90b87674
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381533"
---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>| (OR inclusivo bit a bit) (expresión de SSIS)
  Lleva a cabo una operación OR bit a bit entre dos valores enteros. Compara cada bit del primer operando con el bit correspondiente del segundo operando. Si cualquiera de los bits es 1, el bit de resultado correspondiente se establece en 1. De lo contrario, se establece en cero (0).  
  
 Ambas condiciones deben ser de tipo entero con signo o de tipo entero sin signo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression1 ,integer_ expression2*  
 Cualquier expresión válida de tipo entero con o sin signo. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentarios  
 Si alguna de las condiciones es NULL, el resultado de la expresión será NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo realiza una operación OR inclusiva bit a bit entre las variables **NumberA** y **NumberB**. **NumberA** contiene 3 (00000011) y **NumberB** contiene 9 (00001001).  
  
```  
@NumberA | @NumberB  
```  
  
 El resultado de evaluar la expresión es 11 (00001011).  
  
 00000011  
  
 00001001  
  
 ----------\-  
  
 00001011  
  
 Este ejemplo realiza una operación OR inclusiva bit a bit entre las columnas **ReorderPoint** y **SafetyStockLevel** .  
  
```  
ReorderPoint | SafetyStockLevel  
```  
  
 Si el valor de **ReorderPoint** es 10 y el de **SafetyStockLevel** es 8, el resultado de evaluar la expresión es 10 (00001010).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001010  
  
 Este ejemplo realiza una operación OR inclusiva bit a bit entre dos enteros.  
  
```  
3 | 5   
```  
  
 El resultado de evaluar la expresión es 7 (00000111).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000111  
  
## <a name="see-also"></a>Vea también  
 [&#124;&#124; &#40;OR lógico&#41; &#40;expresión de SSIS&#41;](logical-or-ssis-expression.md)   
 [^ &#40;OR exclusivo bit a bit&#41; &#40;expresión de SSIS&#41;](bitwise-exclusive-or-ssis-expression.md)   
 [Precedencia y capacidad de asociación de operadores](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
