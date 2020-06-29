---
title: Precedencia y capacidad de asociación de operadores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- associativity [Integration Services]
- precedence [Integration Services]
ms.assetid: 5094164f-dabc-45b5-b611-384feb2b3fe3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 47033560e074169524c20d0c6f697de51652c6ce
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437172"
---
# <a name="operator-precedence-and-associativity"></a>Precedencia y capacidad de asociación de operadores
  Cada operador del conjunto de operadores admitidos por el evaluador de expresiones tiene una precedencia designada en la jerarquía de precedencia e incluye el sentido de evaluación. El sentido de evaluación para un operador es la capacidad de asociación del operador. Los operadores con mayor precedencia se evalúan antes que los operadores con menor precedencia. Si una expresión compleja tiene múltiples operadores, la precedencia del operador determina el orden en que se realizan las operaciones. El orden de ejecución puede afectar de manera significativa al valor resultante. Algunos operadores tienen igual precedencia. Si una expresión contiene varios operadores con la misma precedencia, dichos operadores se evalúan de izquierda a derecha o de derecha a izquierda.  
  
 En la tabla siguiente se muestra la precedencia de operadores de mayor a menor. Los operadores del mismo nivel tienen la misma precedencia.  
  
|Símbolo del operador|Tipo de operación|Capacidad de asociación|  
|---------------------|-----------------------|-------------------|  
|( )|Expression|De izquierda a derecha|  
|-, !, ~|Unario|De derecha a izquierda|  
|conversiones de tipos|Unario|De derecha a izquierda|  
|*, / ,%|Multiplicativa|De izquierda a derecha|  
|+, -|Aditiva|De izquierda a derecha|  
|\<, >, \<=, >=|Relacional|De izquierda a derecha|  
|==, !=|Igualdad|De izquierda a derecha|  
|&|AND bit a bit|De izquierda a derecha|  
|^|OR exclusivo bit a bit|De izquierda a derecha|  
|&#124;|OR inclusivo bit a bit|De izquierda a derecha|  
|&&|Y lógico|De izquierda a derecha|  
|&#124;&#124;|O lógico|De izquierda a derecha|  
|? :|Expresión condicional|De derecha a izquierda|  
  
## <a name="see-also"></a>Consulte también  
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
