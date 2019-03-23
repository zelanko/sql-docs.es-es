---
title: LOG (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- base-10 logarithms
- LOG function
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fde9e5cdaea245fd0b99820a89a4466e2d669fdf
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386423"
---
# <a name="log-ssis-expression"></a>LOG (expresión de SSIS)
  Devuelve el logaritmo en base 10 de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LOG(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica válida, distinta de cero y no negativa.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Comentarios  
 La *expresión numérica* se convierte al tipo de datos DT_R8 antes de que se calcule el logaritmo. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 Si la evaluación de *numeric_expression* devuelve cero o un valor negativo, el resultado devuelto será NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal numérico. La función devuelve el valor 1,988291341907488.  
  
```  
LOG(97.34)  
```  
  
 En este ejemplo se utiliza la columna **Length**. Si el valor de la columna es 101,24, la función devuelve 2,005352136486217.  
  
```  
LOG(Length)   
```  
  
 En este ejemplo se utiliza la variable **Length**. La variable debe tener un tipo de datos numérico o la expresión debe incluir una conversión explícita a un tipo de datos numérico [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Si el valor de **Length** es 234,567, la función devuelve 2.370266913465859.  
  
```  
LOG(@Length)   
```  
  
## <a name="see-also"></a>Vea también  
 [EXP &#40;expresión de SSIS&#41;](exp-ssis-expression.md)   
 [LN &#40;expresión de SSIS&#41;](ln-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
