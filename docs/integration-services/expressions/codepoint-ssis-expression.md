---
title: "CODEPOINT (expresión de SSIS) | Microsoft Docs"
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
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43a96940ba28fc76ae271ff0f10b2b3177635346
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
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
  
## <a name="remarks"></a>Notas  
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
  
## <a name="see-also"></a>Ver también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
