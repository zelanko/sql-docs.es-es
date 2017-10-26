---
title: "() (Paréntesis) (expresión de SSIS) | Documentos de Microsoft"
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
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e1bcdc618477d4b4c3cee1dc07b01053335f745
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

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
  
## <a name="see-also"></a>Vea también  
 [Prioridad y asociatividad](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40; Expresión de SSIS &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

