---
title: "- (Negativo) (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "- (negativo)"
  - "negativo (-), operador"
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# - (Negativo) (expresi&#243;n de SSIS)
  Niega una expresión numérica.  
  
## Sintaxis  
  
```  
  
-numeric_expression  
  
```  
  
## Argumentos  
 *numeric_expression*  
 Expresión válida de cualquier tipo de datos numérico. Solo se admiten tipos de datos numéricos con signo. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Tipos de resultado  
 Devuelve el tipo de datos de *numeric_expression*.  
  
## Ejemplos de expresiones  
 Este ejemplo niega el valor de la variable **Counter** y le suma el literal numérico 50.  
  
```  
-@Counter + 50  
```  
  
## Vea también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  