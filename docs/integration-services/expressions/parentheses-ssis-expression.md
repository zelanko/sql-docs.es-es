---
title: () (Paréntesis) (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 705dbabc07308d4e6112489d3d22a0354075fcad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47595443"
---
# <a name="-parentheses-ssis-expression"></a>() (Paréntesis) (expresión de SSIS)
  Identifica el orden de evaluación de las expresiones. Las expresiones escritas entre paréntesis tienen la prioridad de evaluación más alta. Las expresiones anidadas escritas entre paréntesis se evalúan desde dentro hacia fuera.  
  
 Los paréntesis también se usan para hacer que resulte más fácil comprender las expresiones complejas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es cualquier expresión válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 El tipo de datos de *expression*. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo muestra cómo el uso de paréntesis modifica la prioridad de los operadores. La primera expresión se evalúa como 100, mientras que la segunda se evalúa como 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Ver también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
