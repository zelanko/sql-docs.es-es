---
title: CODEPOINT (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 10d2eeb6991c0c75e8dbe8102f94148f60f0a361
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62769382"
---
# <a name="codepoint-ssis-expression"></a>CODEPOINT (expresión de SSIS)
  Devuelve el punto de código Unicode del primer carácter de la izquierda de una expresión de caracteres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres de la que se va a evaluar el primer carácter de la izquierda.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_UI2  
  
## <a name="remarks"></a>Observaciones  
 *character_expression* necesita tener el tipo de datos DT_WSTR.  
  
 CODEPOINT devuelve un resultado NULL si *character_expression* es NULL o una cadena vacía.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal de cadena. El resultado devuelto es 77, el punto de código Unicode correspondiente a la M.  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 En este ejemplo se utiliza una variable. Si el valor de **Name** es Touring Front Wheel, el resultado devuelto es 84, el punto de código Unicode correspondiente a la T.  
  
```  
CODEPOINT(@Name)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
