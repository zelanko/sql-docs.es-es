---
title: '* (Multiplicar) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
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
ms.openlocfilehash: 4182a358c422e3c9a11f76cb824f5386b88b350f
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725133"
---
# <a name="-multiply-ssis-expression"></a>* (Multiplicar) (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Multiplica dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expresión_numérica1, expresión_numérica2*  
 Expresión válida de un tipo de datos numérico. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Notas  
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
  
 Este ejemplo resta el resultado de una expresión de la columna **ListPrice** . La variable **Discount%** debe escribirse entre corchetes porque el nombre incluye el carácter %. Para más información, vea [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
