---
title: SIGN (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b77aaffe4e6f0f0163978ba346abdd31cdc61ce8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62897311"
---
# <a name="sign-ssis-expression"></a>SIGN (expresión de SSIS)
  Devuelve el signo positivo (+1), negativo (-1) o cero (0) de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica con signo válida. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Observaciones  
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
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
