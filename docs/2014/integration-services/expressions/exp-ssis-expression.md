---
title: EXP (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6c8327f2f39e5c90d6bbf4d990430ccecfc50273
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077125"
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
 La expresión numérica se convierte al tipo de datos DT_R8 antes de que se calcule el exponente. Para más información, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
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
 [Registro &#40;expresión de SSIS&#41;](log-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
