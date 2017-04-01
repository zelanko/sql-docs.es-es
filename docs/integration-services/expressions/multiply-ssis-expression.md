---
title: "* (Multiplicar) (expresi&#243;n de SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "* (operador multiplicar)"
  - "multiplicar, operador (*)"
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# * (Multiplicar) (expresi&#243;n de SSIS)
  Multiplica dos expresiones numéricas.  
  
## Sintaxis  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## Argumentos  
 *expresión_numérica1, expresión_numérica2*  
 Expresión válida de un tipo de datos numérico. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Comentarios  
 Si alguno de los operandos es NULL, el resultado será NULL.  
  
## Ejemplos de expresiones  
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
  
## Vea también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  