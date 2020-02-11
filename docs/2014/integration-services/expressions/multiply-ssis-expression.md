---
title: '* (Multiplicar) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6ec24cd980cbfc71c5b9ba834f01bd17eb422400
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768872"
---
# <a name="-multiply-ssis-expression"></a>* (Multiplicar) (expresión de SSIS)
  Multiplica dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expresión_numérica1, expresión_numérica2*  
 Expresión válida de un tipo de datos numérico. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Observaciones  
 Si alguno de los operandos es NULL, el resultado será NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo multiplica literales numéricos.  
  
```  
5 * 6.09  
```  
  
 Este ejemplo multiplica los valores de la columna **ListPrice** por 10 %.  
  
```  
ListPrice * .10  
```  
  
 Este ejemplo resta el resultado de una expresión de la columna **ListPrice** . La variable **Discount%** debe escribirse entre corchetes porque el nombre incluye el carácter %. Para más información, vea [Identificadores &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
