---
title: '| (OR inclusivo bit a bit) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 47a5ad352069006a43a3c2f24c89dae9caf09bc8
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923497"
---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>| (OR inclusivo bit a bit) (expresión de SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Lleva a cabo una operación OR bit a bit entre dos valores enteros. Compara cada bit del primer operando con el bit correspondiente del segundo operando. Si cualquiera de los bits es 1, el bit de resultado correspondiente se establece en 1. De lo contrario, se establece en cero (0).  
  
 Ambas condiciones deben ser de tipo entero con signo o de tipo entero sin signo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression1 ,integer_ expression2*  
 Cualquier expresión válida de tipo entero con o sin signo. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Observaciones  
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
  
## <a name="see-also"></a>Consulte también  
 [&#124;&#124; &#40;Operador OR lógico&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [^ &#40;OR exclusivo bit a bit&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
