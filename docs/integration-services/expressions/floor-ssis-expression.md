---
title: FLOOR (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f0161fe842ad8271d04a69b9cb2726db3403314
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917019"
---
# <a name="floor-ssis-expression"></a>FLOOR (expresión de SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Devuelve el mayor entero que es menor o igual que una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 El tipo de datos numérico de la expresión del argumento. El resultado es la parte entera del valor calculado en el mismo tipo de datos que *numeric_expression*.  
  
## <a name="remarks"></a>Observaciones  
 FLOOR devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Estos ejemplos aplican la función FLOOR a valores positivos, negativos y cero.  
  
```  
FLOOR(123.45)  
```  
  
 Devuelve 123,00  
  
```  
FLOOR(-123.45)  
```  
  
 Devuelve -124,00  
  
```  
FLOOR(0.00)  
```  
  
 Devuelve 0,00.  
  
## <a name="see-also"></a>Consulte también  
 [CEILING &#40;expresión de SSIS&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
