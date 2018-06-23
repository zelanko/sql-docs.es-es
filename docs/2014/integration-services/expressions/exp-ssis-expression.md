---
title: EXP (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 24fde8e1d3401a3c1d8af837f84f34850c81f5e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203669"
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
  
## <a name="remarks"></a>Notas  
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
  
  