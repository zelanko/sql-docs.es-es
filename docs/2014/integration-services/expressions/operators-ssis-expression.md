---
title: Operadores (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4908c50e3714229cae689adc3eee473e05dee184
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969155"
---
# <a name="operators-ssis-expression"></a>Operadores (expresión de SSIS)
  En esta sección se describen los operadores que proporciona el lenguaje de expresiones, así como la precedencia y la capacidad de asociación de los operadores que el evaluador de expresiones utiliza.  
  
 En la tabla siguiente se muestran temas relacionados con los operadores de esta sección.  
  
|Operator|Descripción|  
|--------------|-----------------|  
|[Conversión &#40;expresión de SSIS&#41;](cast-ssis-expression.md)|Convierte una expresión de un tipo de datos a otro.|  
|[&#40;&#41; &#40;Paréntesis&#41; &#40;expresión de SSIS&#41;](parentheses-ssis-expression.md)|Identifica el orden de evaluación de las expresiones.|  
|[+ &#40;Agregar&#41; &#40;SSIS&#41;](add-ssis.md)|Suma dos expresiones numéricas.|  
|[+ &#40;Concatenar&#41; &#40;expresión de SSIS&#41;](concatenate-ssis-expression.md)|Concatena dos expresiones.|  
|[- &#40;Restar&#41; &#40;expresión de SSIS&#41;](subtract-ssis-expression.md)|Resta la segunda expresión numérica de la primera.|  
|[- &#40;Negativo&#41; &#40;expresión de SSIS&#41;](negate-ssis-expression.md)|Niega una expresión numérica.|  
|[&#42; &#40;Multiplicar&#41; &#40;expresión de SSIS&#41;](multiply-ssis-expression.md)|Multiplica dos expresiones numéricas.|  
|[Dividir &#40;expresión de SSIS&#41;](divide-ssis-expression.md)|Divide la primera expresión numérica por la segunda.|  
|[&#40;Módulo&#41; &#40;expresión de SSIS&#41;](modulo-ssis-expression.md)|Proporciona el resto entero después de dividir la primera expresión numérica por la segunda.|  
|[&#124;&#124; &#40;OR lógico&#41; &#40;expresión de SSIS&#41;](logical-or-ssis-expression.md)|Realiza una operación lógica OR.|  
|[&& &#40;AND lógico&#41; &#40;expresión de SSIS&#41;](logical-and-ssis-expression.md)|Realiza una operación lógica AND.|  
|[\! &#40;NOT lógico&#41; &#40;expresión de SSIS&#41;](logical-not-ssis-expression.md)|Niega un operando booleano.|  
|[&#124; &#40;OR inclusivo bit a bit&#41; &#40;expresión de SSIS&#41;](bitwise-inclusive-or-ssis-expression.md)|Lleva a cabo una operación OR bit a bit entre dos valores enteros.|  
|[^ &#40;OR exclusivo bit a bit&#41; &#40;expresión de SSIS&#41;](bitwise-exclusive-or-ssis-expression.md)|Lleva a cabo una operación OR exclusiva bit a bit entre dos valores enteros.|  
|[& &#40;AND bit a bit&#41; &#40;expresión de SSIS&#41;](bitwise-and-ssis-expression.md)|Lleva a cabo una operación AND bit a bit entre dos valores enteros.|  
|[~ &#40;Not bit a bit&#41; &#40;expresión de SSIS&#41;](bitwise-not-ssis-expression.md)|Realiza una negación bit a bit de un entero.|  
|[== &#40;Igual&#41; &#40;expresión de SSIS&#41;](equal-ssis-expression.md)|Realiza una comparación para determinar si dos expresiones son iguales.|  
|[\!= &#40;Diferente&#41; &#40;expresión de SSIS&#41;](unequal-ssis-expression.md)|Realiza una comparación para determinar si dos expresiones no son iguales.|  
|[&#62; &#40;Mayor que&#41; &#40;expresión de SSIS&#41;](greater-than-ssis-expression.md)|Realiza una comparación para determinar si la primera expresión es mayor que la segunda.|  
|[&#60; &#40;Menor que&#41; &#40;expresión de SSIS&#41;](less-than-ssis-expression.md)|Realiza una comparación para determinar si la primera expresión es menor que la segunda.|  
|[&#62;= &#40;Mayor o igual que&#41; &#40;expresión de SSIS&#41;](greater-than-or-equal-to-ssis-expression.md)|Realiza una comparación para determinar si la primera expresión es mayor o igual que la segunda.|  
|[&#60;= &#40;Menor o igual que&#41; &#40;expresión de SSIS&#41;](less-than-or-equal-to-ssis-expression.md)|Realiza una comparación para determinar si la primera expresión es menor o igual que la segunda.|  
|[? : &#40;Condicional&#41; &#40;expresión de SSIS&#41;](conditional-ssis-expression.md)|Devuelve una de dos expresiones en función del resultado de la evaluación de una expresión booleana.|  
  
 Para obtener información sobre la posición de cada operador en la jerarquía de precedencia, vea [Operator Precedence and Associativity](operator-precedence-and-associativity.md).  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)   
 [Ejemplos de expresiones avanzadas de Integration Services](examples-of-advanced-integration-services-expressions.md)   
 [Expresiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md)  
  
  
