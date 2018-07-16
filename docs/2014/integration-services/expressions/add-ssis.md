---
title: + (Sumar) (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2b7b971521991be68d69efd2519b423958ef4fbf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248865"
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
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="remarks"></a>Notas  
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
  
 Este ejemplo suma un valor calculado a la columna **StandardCost** . La variable **Profit%** debe escribirse entre corchetes porque el nombre incluye el carácter %. Para obtener más información, vea [Identificadores &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>Vea también  
 [Precedencia y asociatividad](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
