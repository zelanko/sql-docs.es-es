---
title: "~ (NOT bit a bit) (expresión de SSIS) | Microsoft Docs"
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
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
caps.latest.revision: "31"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 57e1a67408db2b1ed6412e269559be3faa9c9d1a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="-bitwise-not-ssis-expression"></a>~ (Not bit a bit) (expresión de SSIS)
  Realiza una negación bit a bit de un entero. Este operador puede aplicarse a tipos de datos enteros con o sin signo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression*  
 Expresión válida de cualquier tipo de datos entero. *integer*_*expression* es un entero que se transforma en un número binario para la operación bit a bit. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos de *integer_expression*.  
  
## <a name="remarks"></a>Comentarios  
 None  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo realiza una operación ~ (NOT) bit a bit en el número 170, cuya representación binaria es 0000 0000 1010 1010. Se trata de un entero con signo.  
  
```  
  
~ 170  
```  
  
 El resultado de la operación es -170 (con representación binaria 1111111101010101).  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## <a name="see-also"></a>Vea también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
