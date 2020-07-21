---
title: FLOOR (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8624354ff5b29430a58f0393047c9a875cf984c2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428683"
---
# <a name="floor-ssis-expression"></a>FLOOR (expresión de SSIS)
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
 [CEILING &#40;expresión de SSIS&#41;](ceiling-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
