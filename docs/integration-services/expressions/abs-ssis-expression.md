---
title: "ABS (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "ABS, función"
  - "valor positivo absoluto"
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# ABS (expresi&#243;n de SSIS)
  Devuelve el valor absoluto (positivo) de una expresión numérica.  
  
## Sintaxis  
  
```  
  
ABS(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 Expresión numérica con o sin signo.  
  
## Tipos de resultado  
 El tipo de datos de la expresión numérica pasada a la función.  
  
## Comentarios  
 ABS devuelve un resultado NULL si el valor del argumento es NULL.  
  
## Ejemplos de expresiones  
 Estos ejemplos aplican la función ABS a un número positivo y a un número negativo. Ambos devuelven 1,23.  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 Este ejemplo aplica la función ABS a una expresión que resta valores de las variables **HighTemperature** y **LowTempature**.  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## Vea también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  