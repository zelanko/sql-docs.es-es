---
description: Precedencia y capacidad de asociación de operadores
title: Precedencia y capacidad de asociación de operadores | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- associativity [Integration Services]
- precedence [Integration Services]
ms.assetid: 5094164f-dabc-45b5-b611-384feb2b3fe3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cda01c12856bff3e28b06c9cfddccb368e6a3e6b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477514"
---
# <a name="operator-precedence-and-associativity"></a>Precedencia y capacidad de asociación de operadores

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Cada operador del conjunto de operadores admitidos por el evaluador de expresiones tiene una precedencia designada en la jerarquía de precedencia e incluye el sentido de evaluación. El sentido de evaluación para un operador es la capacidad de asociación del operador. Los operadores con mayor precedencia se evalúan antes que los operadores con menor precedencia. Si una expresión compleja tiene múltiples operadores, la precedencia del operador determina el orden en que se realizan las operaciones. El orden de ejecución puede afectar de manera significativa al valor resultante. Algunos operadores tienen igual precedencia. Si una expresión contiene varios operadores con la misma precedencia, dichos operadores se evalúan de izquierda a derecha o de derecha a izquierda.  
  
 En la tabla siguiente se muestra la precedencia de operadores de mayor a menor. Los operadores del mismo nivel tienen la misma precedencia.  
  
|Símbolo del operador|Tipo de operación|asociatividad|  
|---------------------|-----------------------|-------------------|  
|( )|Expresión|De izquierda a derecha|  
|-, !, ~|Unario|De derecha a izquierda|  
|conversiones de tipos|Unario|De derecha a izquierda|  
|*, / ,%|Multiplicativo|De izquierda a derecha|  
|+, -|Aditivo|De izquierda a derecha|  
|\<, >, \<=, >=|Relacional|De izquierda a derecha|  
|==, !=|Igualdad|De izquierda a derecha|  
|&|AND bit a bit|De izquierda a derecha|  
|^|OR exclusivo bit a bit|De izquierda a derecha|  
|&#124;|OR inclusivo bit a bit|De izquierda a derecha|  
|&&|Y lógico|De izquierda a derecha|  
|&#124;&#124;|O lógico|De izquierda a derecha|  
|? :|Expresión condicional|De derecha a izquierda|  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
