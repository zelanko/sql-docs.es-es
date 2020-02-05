---
title: ABS (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2d332c8cdffae320d602f0581c7641d69c31c4fa
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297701"
---
# <a name="abs-ssis-expression"></a>ABS (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
