---
title: EXP (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 366a938b2e90ce448cbcba2775f0eb7f327aab61
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393808"
---
# <a name="exp-ssis-expression"></a>EXP (expresión de SSIS)
  Devuelve el exponente de la base e de una expresión numérica. La función EXP complementa la acción de la función LN; también se suele llamar antilogaritmo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Comentarios  
 La expresión numérica se convierte al tipo de datos DT_R8 antes de que se calcule el exponente. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 El resultado devuelto es siempre un número positivo.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En estos ejemplos se aplica la función EXP a cero y a valores positivos y negativos.  
  
```  
EXP(74)  
```  
  
 Devuelve 1,373382979540176E+32.  
  
```  
EXP(-27)  
```  
  
 Devuelve 1,879528816539083E-12.  
  
```  
EXP(0)  
```  
  
 Devuelve 1.  
  
## <a name="see-also"></a>Vea también  
 [LOG &#40;expresión de SSIS&#41;](log-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
