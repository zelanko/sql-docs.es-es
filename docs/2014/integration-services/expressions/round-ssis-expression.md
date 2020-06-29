---
title: ROUND (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5edad70330a5745f9d150cf8a0ad0d540132c029
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437112"
---
# <a name="round-ssis-expression"></a>ROUND (expresión de SSIS)
  Devuelve una expresión numérica, redondeada a la longitud o precisión especificada. La evaluación del parámetro de longitud debe devolver un entero.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión con un tipo numérico válido. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 *length*  
 Expresión entera. Es la precisión con la que *numeric_expression* se redondea.  
  
## <a name="result-types"></a>Tipos de resultado  
 El mismo tipo que *numeric*_*expression*.  
  
## <a name="remarks"></a>Observaciones  
 La evaluación del argumento *length* debe devolver cero o un entero positivo.  
  
 ROUND devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Estos ejemplos redondean los literales numéricos a una longitud de tres. El primer resultado devuelto es 137,1570, el segundo 137,1580.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
