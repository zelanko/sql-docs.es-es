---
title: "CEILING (expresión de SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 971c7038c0b144ac4073162e0d14b519e263328f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
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
 [FLOOR &#40;expresión de SSIS&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
