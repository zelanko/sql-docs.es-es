---
title: SIGN (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8ab30748b50df8cbb176c5fa1bdb6c11f0b2b132
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sign-ssis-expression"></a>SIGN (expresión de SSIS)
  Devuelve el signo positivo (+1), negativo (-1) o cero (0) de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica con signo válida. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Notas  
 SIGN devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve el signo de un literal numérico. El resultado devuelto es -1.  
  
```  
SIGN(-123.45)  
```  
  
 Este ejemplo devuelve el signo del resultado de restar la columna **StandardCost** de la columna **DealerPrice** .  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## <a name="see-also"></a>Ver también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
