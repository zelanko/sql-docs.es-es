---
description: '- (Restar) (expresión de SSIS)'
title: '- (Restar) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6d4235e64f59814075a5d0d57e24d5345b9876a0
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243695"
---
# <a name="--subtract-ssis-expression"></a>- (Restar) (expresión de SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Resta la segunda expresión numérica de la primera.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
numeric_expression1 - numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expresión_numérica1, expresión_numérica2*  
 Expresión válida de un tipo de datos numérico. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Dependen de los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Observaciones  
 - Incluya la expresión unaria menos entre paréntesis para asegurarse de que se evalúa en el orden correcto.  

 - Si alguno de los operandos es NULL, el resultado será NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo resta literales numéricos.  
  
```  
5 - 6.09  
```  
  
 Este ejemplo resta el valor de la columna **StandardCost** del valor de la columna **ListPrice** .  
  
```  
ListPrice - StandardCost  
```  
  
 Este ejemplo resta un valor calculado de la columna **ListPrice** . La variable **Discount%** debe escribirse entre corchetes porque el nombre incluye el carácter %. Para más información, vea [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
