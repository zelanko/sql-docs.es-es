---
title: "POWER (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "POWER, función"
ms.assetid: db48ae65-bfa6-4db1-8d3c-d0d4f8a399bc
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# POWER (expresi&#243;n de SSIS)
  Devuelve el resultado de elevar una expresión numérica a una determinada potencia. La evaluación del parámetro de potencia debe devolver un entero.  
  
## Sintaxis  
  
```  
  
POWER(numeric_expression,power)  
```  
  
## Argumentos  
 *numeric_expression*  
 Expresión numérica válida.  
  
 *power*  
 Expresión numérica válida.  
  
## Tipos de resultado  
 DT_R8  
  
## Comentarios  
 Los argumentos *numeric_expression* y *power* se convierten al tipo de datos DT_R8 antes de que se calcule la potencia. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Si el valor de *numeric_expression* da como resultado cero y el valor de *power* es negativo, el evaluador de expresiones devolverá un error y establecerá el resultado devuelto en NULL.  
  
 Si *numeric_expression* o *power* producen resultados indeterminados, el resultado devuelto será NULL.  
  
 El argumento *power* puede ser una fracción. Por ejemplo, puede utilizar el valor 0,5 como potencia.  
  
## Ejemplos de expresiones  
 Este ejemplo usa un literal numérico. La función eleva 4 a la potencia 3 y devuelve 64.  
  
```  
POWER(4,3)  
```  
  
 Este ejemplo utiliza la columna **Length** y la variable **DimensionCount** . Si el valor de **Length** es 8 y el de **DimensionCount** es 2, el resultado devuelto es 64.  
  
```  
POWER(Length, @DimensionCount)   
```  
  
## Vea también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  