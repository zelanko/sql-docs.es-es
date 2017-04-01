---
title: "FLOOR (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "entero más grande menor o igual que la expresión"
  - "Función FLOOR [SSIS]"
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# FLOOR (expresi&#243;n de SSIS)
  Devuelve el mayor entero que es menor o igual que una expresión numérica.  
  
## Sintaxis  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 Expresión numérica válida.  
  
## Tipos de resultado  
 El tipo de datos numérico de la expresión del argumento. El resultado es la parte entera del valor calculado en el mismo tipo de datos que *numeric_expression*.  
  
## Comentarios  
 FLOOR devuelve un resultado NULL si el valor del argumento es NULL.  
  
## Ejemplos de expresiones  
 Estos ejemplos aplican la función FLOOR a valores positivos, negativos y cero.  
  
```  
FLOOR(123.45)  
```  
  
 Devuelve 123,00  
  
```  
FLOOR(-123.45)  
```  
  
 Devuelve -124,00  
  
```  
FLOOR(0.00)  
```  
  
 Devuelve 0,00.  
  
## Vea también  
 [CEILING &#40;expresión de SSIS&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  