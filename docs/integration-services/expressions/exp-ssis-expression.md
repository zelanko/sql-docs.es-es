---
title: "EXP (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "funciones exponenciales"
  - "EXP, función"
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# EXP (expresi&#243;n de SSIS)
  Devuelve el exponente de la base e de una expresión numérica. La función EXP complementa la acción de la función LN; también se suele llamar antilogaritmo.  
  
## Sintaxis  
  
```  
  
EXP(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 Expresión numérica válida.  
  
## Tipos de resultado  
 DT_R8  
  
## Comentarios  
 La expresión numérica se convierte al tipo de datos DT_R8 antes de que se calcule el exponente. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 El resultado devuelto es siempre un número positivo.  
  
## Ejemplos de expresiones  
 En estos ejemplos se aplica la función EXP a cero y a valores positivos y negativos.  
  
```  
EXP(74)  
```  
  
 Devuelve 1,373382979540176E+32.  
  
```  
EXP(-27)  
```  
  
 Devuelve 1,879528816539083E-12.  
  
```  
EXP(0)  
```  
  
 Devuelve 1.  
  
## Vea también  
 [LOG &#40;expresión de SSIS&#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  