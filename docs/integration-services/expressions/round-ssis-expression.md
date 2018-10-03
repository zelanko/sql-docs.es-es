---
title: ROUND (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 01814908d83b302f5f79ae9ac2be713f022fdb43
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622353"
---
# <a name="round-ssis-expression"></a>ROUND (expresión de SSIS)
  Devuelve una expresión numérica, redondeada a la longitud o precisión especificada. La evaluación del parámetro de longitud debe devolver un entero.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión con un tipo numérico válido. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *length*  
 Expresión entera. Es la precisión con la que *numeric_expression* se redondea.  
  
## <a name="result-types"></a>Tipos de resultado  
 El mismo tipo que *numeric*_*expression*.  
  
## <a name="remarks"></a>Notas  
 La evaluación del argumento *length* debe devolver cero o un entero positivo.  
  
 ROUND devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Estos ejemplos redondean los literales numéricos a una longitud de tres. El primer resultado devuelto es 137,1570, el segundo 137,1580.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>Ver también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
