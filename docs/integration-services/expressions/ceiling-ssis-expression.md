---
title: CEILING (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b3de7c4bd0d60c17feeb596859a34b877f9cfc3f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759123"
---
# <a name="ceiling-ssis-expression"></a>CEILING (expresión de SSIS)
  Devuelve el menor entero mayor o igual que una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CEILING(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 El tipo de datos de la expresión numérica pasada a la función.  
  
## <a name="remarks"></a>Notas  
 CEILING devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Estos ejemplos aplican la función CEILING a valores positivos, negativos y cero.  
  
```  
CEILING(123.74)  
```  
  
 Devuelve 124.00.  
  
```  
CEILING(-124.27)  
```  
  
 Devuelve -124.00.  
  
```  
CEILING(0.00)  
```  
  
 Devuelve 0,00.  
  
## <a name="see-also"></a>Ver también  
 [FLOOR &#40;expresión de SSIS&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
