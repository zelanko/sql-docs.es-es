---
title: "+ (Concatenar) (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "concatenación [Integration Services]"
  - "+ (operador de concatenación)"
  - "concatenación, operador (+)"
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# + (Concatenar) (expresi&#243;n de SSIS)
  Concatena dos expresiones en una expresión.  
  
## Sintaxis  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## Argumentos  
 *expression1, expression2*  
 Cualquier expresión válida con tipo de datos DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
## Tipos de resultado  
 DT_WSTR  
  
## Comentarios  
 La expresión puede usar los tipos de datos DT_STR y DT_WSTR, o uno de los dos.  
  
 La concatenación de los tipos de datos DT_STR y DT_WSTR devuelve un resultado de tipo DT_WSTR. La longitud de la cadena es la suma de las longitudes de las cadenas originales expresadas en caracteres.  
  
 Solo se pueden concatenar datos con los tipos de datos de cadena DT_STR y DT_WSTR o con los tipos de datos de bloque de objetos binarios grandes (BLOB) DT_TEXT, DT_NTEXT y DT_IMAGE. Los otros tipos de datos deben convertirse explícitamente en uno de estos tipos de datos antes de que se produzca la concatenación. Para obtener más información sobre conversiones válidas entre tipos de datos, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Ambas expresiones deben tener el mismo tipo de datos o una expresión debe poder convertirse implícitamente al tipo de datos de la otra expresión. Por ejemplo, si se concatena la cadena "Order date is " y la columna **OrderDate** , los valores de **OrderDate** se convierten implícitamente a un tipo de datos de cadena. Para concatenar dos valores numéricos, ambos valores deben convertirse explícitamente a un tipo de datos de cadena.  
  
 En una concatenación solo se puede usar un tipo de datos BLOB: DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
 Si alguno de los elementos es NULL, el resultado será NULL.  
  
 Los literales de cadena deben escribirse entre comillas.  
  
## Ejemplos de expresiones  
 Este ejemplo concatena los valores de las columnas **FirstName** y **LastName** e inserta un espacio entre ellos.  
  
```  
FirstName + ' ' + LastName  
```  
  
 En este ejemplo se concatenan las variables **ZIPCode** y **ZIPCode+4**. Ambas variables tienen un tipo de datos de cadena. **ZIPCode+4** debe escribirse entre corchetes porque el nombre de la variable incluye el carácter +.  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## Vea también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  