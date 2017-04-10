---
title: "SQRT (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "SQRT, función"
  - "raíz cuadrada de la expresión dada"
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# SQRT (expresi&#243;n de SSIS)
  Devuelve la raíz cuadrada de una expresión numérica.  
  
## Sintaxis  
  
```  
  
SQRT(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 Expresión numérica de cualquier tipo de datos numérico. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Tipos de resultado  
 DT_R8  
  
## Comentarios  
 SQRT devuelve un resultado NULL si el valor del argumento es NULL.  
  
 SQRT produce un error si el argumento es un valor negativo.  
  
 Antes de realizar la operación de raíz cuadrada, se convierte el argumento al tipo de datos DT_R8.  
  
## Ejemplos de expresiones  
 Este ejemplo devuelve la raíz cuadrada de un literal numérico. El resultado devuelto es 12.  
  
```  
SQRT(144)  
```  
  
 Este ejemplo devuelve la raíz cuadrada de una expresión, el resultado de restar valores de las columnas **Value1** y **Value2** .  
  
```  
SQRT(Value1 - Value2)  
```  
  
 Este ejemplo devuelve la longitud del tercer lado de un triángulo rectángulo aplicando la función SQUARE a dos variables y calculando a continuación la raíz cuadrada de la suma. Si **Side1** contiene 3 y **Side2** contiene 4, la función SQRT devuelve 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  En las expresiones, los nombres de variables siempre incluyen el prefijo @.  
  
## Vea también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  