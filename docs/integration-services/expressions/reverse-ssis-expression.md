---
title: "REVERSE (expresión de SSIS) | Microsoft Docs"
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
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2a20cd5329e2d94cb4da44208e6811fd076d6cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="reverse-ssis-expression"></a>REVERSE (expresión de SSIS)
  Devuelve una expresión de caracteres en orden inverso.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres que se va a invertir.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentarios  
 El argumento *character_expression* ha de tener el tipo de datos DT_WSTR.  
  
 REVERSE devuelve un resultado NULL si el valor de *character_expression* es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal de cadena. El resultado devuelto es "ekiB niatnuoM".  
  
```  
REVERSE("Mountain Bike")  
```  
  
 En este ejemplo se utiliza una variable. Si **Name** contiene Touring Bike, el resultado devuelto es "ekiB gniruoT".  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
