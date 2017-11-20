---
title: Precedencia y asociatividad | Documentos de Microsoft
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
- associativity [Integration Services]
- precedence [Integration Services]
ms.assetid: 5094164f-dabc-45b5-b611-384feb2b3fe3
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1b6f1c3252fb8a2f68fae20a67cc6174ea41924a
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="operator-precedence-and-associativity"></a>Precedencia y capacidad de asociación de operadores
  Cada operador del conjunto de operadores admitidos por el evaluador de expresiones tiene una precedencia designada en la jerarquía de precedencia e incluye el sentido de evaluación. El sentido de evaluación para un operador es la capacidad de asociación del operador. Los operadores con mayor precedencia se evalúan antes que los operadores con menor precedencia. Si una expresión compleja tiene múltiples operadores, la precedencia del operador determina el orden en que se realizan las operaciones. El orden de ejecución puede afectar de manera significativa al valor resultante. Algunos operadores tienen igual precedencia. Si una expresión contiene varios operadores con la misma precedencia, dichos operadores se evalúan de izquierda a derecha o de derecha a izquierda.  
  
 En la tabla siguiente se muestra la precedencia de operadores de mayor a menor. Los operadores del mismo nivel tienen la misma precedencia.  
  
|Símbolo del operador|Tipo de operación|Capacidad de asociación|  
|---------------------|-----------------------|-------------------|  
|( )|Expresión|De izquierda a derecha|  
|–, !, ~|Unario|De derecha a izquierda|  
|conversiones de tipos|Unario|De derecha a izquierda|  
|*, / ,%|Multiplicativa|De izquierda a derecha|  
|+, –|Aditiva|De izquierda a derecha|  
|\<, >, \<=, >=|Relacionales|De izquierda a derecha|  
|==, !=|Igualdad|De izquierda a derecha|  
|&|AND bit a bit|De izquierda a derecha|  
|^|OR exclusivo bit a bit|De izquierda a derecha|  
|&#124;|OR inclusivo bit a bit|De izquierda a derecha|  
|&&|Y lógico|De izquierda a derecha|  
|&#124;&#124;|O lógico|De izquierda a derecha|  
|? :|Expresión condicional|De derecha a izquierda|  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

