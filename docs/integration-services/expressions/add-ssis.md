---
title: + (Agregar) (SSIS) | Documentos de Microsoft
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
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 04596cf4762f2473da1555f4ce5f9cd210678986
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="-add-ssis"></a>+ (Sumar) (SSIS)
  Suma dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression1, numeric_ expression2*  
 Expresión válida de un tipo de datos numérico.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="remarks"></a>Comentarios  
 Si alguno de los operandos es NULL, el resultado será NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo suma literales numéricos.  
  
```  
5 + 6.09 + 7.0  
```  
  
 Este ejemplo suma los valores de las columnas **VacationHours** y **SickLeaveHours** .  
  
```  
VacationHours + SickLeaveHours  
```  
  
 Este ejemplo suma un valor calculado a la columna **StandardCost** . La variable **Profit%** debe escribirse entre corchetes porque el nombre incluye el carácter %. Para obtener más información, vea [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>Vea también  
 [Prioridad y asociatividad](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40; Expresión de SSIS &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
