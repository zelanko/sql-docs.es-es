---
title: "LOG (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "logaritmos de base 10"
  - "LOG, función"
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# LOG (expresi&#243;n de SSIS)
  Devuelve el logaritmo en base 10 de una expresión numérica.  
  
## Sintaxis  
  
```  
  
LOG(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 Expresión numérica válida, distinta de cero y no negativa.  
  
## Tipos de resultado  
 DT_R8  
  
## Comentarios  
 La *expresión numérica* se convierte al tipo de datos DT_R8 antes de que se calcule el logaritmo. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Si la evaluación de *numeric_expression* devuelve cero o un valor negativo, el resultado devuelto será NULL.  
  
## Ejemplos de expresiones  
 Este ejemplo usa un literal numérico. La función devuelve el valor 1,988291341907488.  
  
```  
LOG(97.34)  
```  
  
 En este ejemplo se utiliza la columna **Length**. Si el valor de la columna es 101,24, la función devuelve 2,005352136486217.  
  
```  
LOG(Length)   
```  
  
 En este ejemplo se utiliza la variable **Length**. La variable debe tener un tipo de datos numérico o la expresión debe incluir una conversión explícita a un tipo de datos numérico [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Si el valor de **Length** es 234,567, la función devuelve 2.370266913465859.  
  
```  
LOG(@Length)   
```  
  
## Vea también  
 [EXP &#40;expresión de SSIS&#41;](../../integration-services/expressions/exp-ssis-expression.md)   
 [LN &#40;expresión de SSIS&#41;](../../integration-services/expressions/ln-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  