---
title: ABS (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7fafc0ba09a8345e0639016aadfdef185900589d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62769621"
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
  
## <a name="remarks"></a>Observaciones  
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
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
