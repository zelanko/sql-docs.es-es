---
title: + (Sumar) (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9341cb3647db9e8e7061b1418b169c4ac4d158d5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378553"
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
 Determinados por los tipos de datos de los dos argumentos. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
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
  
 Este ejemplo suma un valor calculado a la columna **StandardCost** . La variable **Profit%** debe escribirse entre corchetes porque el nombre incluye el carácter %. Para obtener más información, vea [Identificadores &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>Vea también  
 [Precedencia y capacidad de asociación de operadores](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
