---
title: () (Paréntesis) (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3fc1a9beb0468f50291854d8eb5cd0e3bf9ba8d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768811"
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
 El tipo de datos de *expression*. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo muestra cómo el uso de paréntesis modifica la prioridad de los operadores. La primera expresión se evalúa como 100, mientras que la segunda se evalúa como 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
