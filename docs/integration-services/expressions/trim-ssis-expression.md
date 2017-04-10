---
title: "TRIM (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "espacio en blanco iniciales"
  - "TRIM, función"
  - "espacios en blanco finales"
ms.assetid: 7dd9081d-a3d4-483a-bf7e-bf2bd7692d39
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# TRIM (expresi&#243;n de SSIS)
  Devuelve una expresión de caracteres después de quitar los espacios iniciales y finales.  
  
> [!NOTE]  
>  TRIM no quita los caracteres de espacio en blanco, como los caracteres de tabulación o de salto de línea. Unicode proporciona puntos de código para muchos tipos distintos de espacios, pero su función solo reconoce el punto de código Unicode 0x0020. Cuando se convierten cadenas del juego de caracteres de doble byte (DBCS) a Unicode, éstas pueden incluir caracteres de espacio distintos de 0x0020 y la función no puede eliminarlos. Para eliminar cualquier tipo de espacio, puede utilizar el método Trim de Microsoft Visual Basic .NET en un script ejecutado desde el componente Script.  
  
## Sintaxis  
  
```  
  
TRIM(character_expression)  
```  
  
## Argumentos  
 *character_expression*  
 Expresión de caracteres de la que puede quitar espacios.  
  
## Tipos de resultado  
 DT_WSTR  
  
## Comentarios  
 TRIM devuelve un resultado NULL si el valor del argumento es NULL.  
  
 TRIM solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que TRIM realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
## Ejemplos de expresiones  
 Este ejemplo quita los espacios iniciales y finales de un literal de cadena. El resultado devuelto es "New York".  
  
```  
TRIM("   New York   ")  
```  
  
 Este ejemplo quita los espacios iniciales y finales del resultado de concatenar las columnas **FirstName** y **LastName** . La cadena vacía entre **FirstName** y **LastName** no se quita.  
  
```  
TRIM(FirstName + " "+ LastName)  
```  
  
## Vea también  
 [LTRIM &#40;expresión de SSIS&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)   
 [RTRIM &#40;expresión de SSIS&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  