---
title: "CEILING (expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce44f2297c19b62687ca097343dc970397ca28d6
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

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
  
## <a name="remarks"></a>Comentarios  
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
  
## <a name="see-also"></a>Vea también  
 [FLOOR &#40; Expresión de SSIS &#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
