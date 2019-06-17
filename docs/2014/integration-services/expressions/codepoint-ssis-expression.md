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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
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
  
## <a name="remarks"></a>Comentarios  
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
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
