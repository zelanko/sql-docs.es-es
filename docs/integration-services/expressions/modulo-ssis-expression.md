---
title: (Módulo) (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '% (modulo operator)'
- remainder of division operation
- modulo operator (%)
ms.assetid: e2920821-2f5b-4c76-8db8-8b9eddf4606f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 855e96dbc95b7b6b76fce213524705b289bce42b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277544"
---
# <a name="modulo-ssis-expression"></a>(Módulo) (expresión de SSIS)
  Proporciona el resto entero después de dividir la primera expresión numérica por la segunda.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dividend % divisor  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *dividend*  
 Es la expresión numérica que se va a dividir. *dividend* puede ser cualquier expresión numérica. Para más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *divisor*  
 Es la expresión numérica entre la que se va a dividir el dividendo. *divisor* puede ser cualquier expresión numérica excepto cero.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Notas  
 La evaluación de ambas expresiones debe devolver tipos de datos enteros, con o sin signo.  
  
 Si alguno de los operandos es NULL, el resultado será NULL.  
  
 No se puede usar 0 como divisor.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo calcula el módulo a partir de dos literales numéricos. El resultado es 3.  
  
```  
42 % 13  
```  
  
 Este ejemplo calcula el módulo de la columna **SalesQuota** y un literal numérico.  
  
```  
SalesQuota % 12  
```  
  
 Este ejemplo calcula el módulo de dos variables numéricas: **Sales$** y **Month**. La variable **Sales$** debe escribirse entre corchetes, ya que su nombre contiene el carácter $. Para más información, vea [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
@[Sales$] % @Month  
```  
  
 Este ejemplo usa el operador módulo para determinar si el valor de la variable **Value** es par o impar, y utiliza el operador condicional para devolver una cadena que describe el resultado. Para más información, vea [? : &#40;Condicional&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/conditional-ssis-expression.md).  
  
```  
@Value % 2 == 0? "even":"odd"  
```  
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
