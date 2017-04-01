---
title: "CEILING (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "entero más pequeño mayor o igual que la expresión"
  - "Función CEILING [SSIS]"
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# CEILING (expresi&#243;n de SSIS)
  Devuelve el menor entero mayor o igual que una expresión numérica.  
  
## Sintaxis  
  
```  
  
CEILING(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 Expresión numérica válida.  
  
## Tipos de resultado  
 El tipo de datos de la expresión numérica pasada a la función.  
  
## Comentarios  
 CEILING devuelve un resultado NULL si el valor del argumento es NULL.  
  
## Ejemplos de expresiones  
 Estos ejemplos aplican la función CEILING a valores positivos, negativos y cero.  
  
```  
CEILING(123.74)  
```  
  
 Devuelve 124.00.  
  
```  
CEILING(-124.27)  
```  
  
 Devuelve -124.00.  
  
```  
CEILING(0.00)  
```  
  
 Devuelve 0,00.  
  
## Vea también  
 [FLOOR &#40;expresión de SSIS&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  