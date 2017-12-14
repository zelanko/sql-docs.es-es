---
title: "Dividir (expresión de SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 5bde9223-872d-443e-8a27-57735e1d8f3d
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ae36c790ba78fbf0d64991bb69429d39636b560
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="divide-ssis-expression"></a>Dividir (expresión de SSIS)
  Divide la primera expresión numérica por la segunda.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dividend / divisor  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *dividend*  
 Es la expresión numérica que se va a dividir. *dividend* puede ser cualquier expresión numérica. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *divisor*  
 Es la expresión numérica entre la que se va a dividir el dividendo. *divisor* puede ser cualquier expresión numérica excepto cero.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentarios  
 Si alguno de los operandos es NULL, el resultado será NULL.  
  
 No se permite dividir por cero. En función de cómo se evalúe la subexpresión *divisor* , se producirá uno de los siguientes errores:  
  
-   Si la subexpresión *divisor* que devuelve cero es una constante, el error aparecerá en tiempo de diseño y hará que no se valide la expresión.  
  
-   Si la subexpresión *divisor* que devuelve cero contiene variables pero no contiene columnas de entrada, el componente al que la expresión pertenece no superará la validación previa a la ejecución del paquete.  
  
-   Si la subexpresión *divisor* que se evalúa como cero contiene columnas de entrada, el error aparecerá en tiempo de ejecución y se controlará en función de las reglas de flujo de errores del componente de flujo de datos.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo divide dos literales numéricos.  
  
```  
25 / 5  
```  
  
 Este ejemplo divide los valores de la columna **ListPrice** por los valores de la columna **StandardCost** .  
  
```  
ListPrice / StandardCost  
```  
  
## <a name="see-also"></a>Vea también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
