---
title: "+ (Sumar) (SSIS) | Microsoft Docs"
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
  - "+ (sumar)"
  - "sumar (+), operador"
  - "agregar expresiones"
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# + (Sumar) (SSIS)
  Suma dos expresiones numéricas.  
  
## Sintaxis  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## Argumentos  
 *numeric_expression1, numeric_ expression2*  
 Expresión válida de un tipo de datos numérico.  
  
## Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Comentarios  
 Si alguno de los operandos es NULL, el resultado será NULL.  
  
## Ejemplos de expresiones  
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
  
## Vea también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  