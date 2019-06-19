---
title: ~ (NOT bit a bit) (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4c07444ff1dd425671fbc17176fc3aa94e0705bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725598"
---
# <a name="-bitwise-not-ssis-expression"></a>~ (Not bit a bit) (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Realiza una negación bit a bit de un entero. Este operador puede aplicarse a tipos de datos enteros con o sin signo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression*  
 Expresión válida de cualquier tipo de datos entero. *integer*_*expression* es un entero que se transforma en un número binario para la operación bit a bit. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos de *integer_expression*.  
  
## <a name="remarks"></a>Notas  
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
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
