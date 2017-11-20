---
title: "ABS (expresión de SSIS) | Documentos de Microsoft"
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
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cf829866d0e55798b612af57a8d8c6cef6d3fcd4
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="abs-ssis-expression"></a>ABS (expresión de SSIS)
  Devuelve el valor absoluto (positivo) de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ABS(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica con o sin signo.  
  
## <a name="result-types"></a>Tipos de resultado  
 El tipo de datos de la expresión numérica pasada a la función.  
  
## <a name="remarks"></a>Comentarios  
 ABS devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Estos ejemplos aplican la función ABS a un número positivo y a un número negativo. Ambos devuelven 1,23.  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 Este ejemplo aplica la función ABS a una expresión que resta valores de las variables **HighTemperature** y **LowTempature**.  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

