---
title: "&amp;&amp; (AND l&#243;gico) (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "&& (AND lógico)"
  - "AND, AND lógico"
  - "AND lógico (&&)"
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# &amp;&amp; (AND l&#243;gico) (expresi&#243;n de SSIS)
  Realiza una operación lógica AND. La expresión devuelve TRUE si todas las condiciones son TRUE.  
  
## Sintaxis  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## Argumentos  
 *boolean_expression1, boolean_expression2*  
 Cualquier expresión válida cuya evaluación devuelva TRUE, FALSE o NULL.  
  
## Tipos de resultado  
 DT_BOOL  
  
## Comentarios  
 En la siguiente tabla se muestra el resultado del operador &&.  
  
|Resultado|Expresión|Expresión|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## Ejemplos de expresiones  
 En este ejemplo se usan las columnas **StandardCost** y **ListPrice** . Este ejemplo devuelve TRUE si el valor de la columna **StandardCost** es menor que 300 y el valor de la columna **ListPrice** es mayor que 500.  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 En este ejemplo se utilizan las variables **SPrice** y **LPrice** en lugar de literales.  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## Vea también  
 [& &#40;AND bit a bit&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)   
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  