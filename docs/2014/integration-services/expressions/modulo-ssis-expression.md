---
title: (Módulo) (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 163dbfecd4605c6c9624d94c047b1c7e893d8fcd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768881"
---
# <a name="modulo-ssis-expression"></a>(Módulo) (expresión de SSIS)
  Proporciona el resto entero después de dividir la primera expresión numérica por la segunda.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dividend % divisor  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *dividend*  
 Es la expresión numérica que se va a dividir. *dividend* puede ser cualquier expresión numérica. Para más información, vea [Tipos de datos de Integration Services](../data-flow/integration-services-data-types.md).  
  
 *divisor*  
 Es la expresión numérica entre la que se va a dividir el dividendo. *divisor* puede ser cualquier expresión numérica excepto cero.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentarios  
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
  
 Este ejemplo calcula el módulo de dos variables numéricas: **Sales$** y **Month**. La variable **Sales$** debe escribirse entre corchetes, ya que su nombre contiene el carácter $. Para más información, vea [Identificadores &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
@[Sales$] % @Month  
```  
  
 Este ejemplo usa el operador módulo para determinar si el valor de la variable **Value** es par o impar, y utiliza el operador condicional para devolver una cadena que describe el resultado. Para más información, vea [? : &#40;Condicional&#41; &#40;expresión de SSIS&#41;](conditional-ssis-expression.md).  
  
```  
@Value % 2 == 0? "even":"odd"  
```  
  
## <a name="see-also"></a>Vea también  
 [Precedencia y capacidad de asociación de operadores](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
