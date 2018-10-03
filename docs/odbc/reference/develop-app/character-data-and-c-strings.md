---
title: Caracteres de datos y cadenas de C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df2afd988e46692f816c22e69a31b33833129ff1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809393"
---
# <a name="character-data-and-c-strings"></a>Datos de caracteres y cadenas de c
Parámetros de entrada que hacen referencia a los datos de caracteres de longitud variable (por ejemplo, los nombres de columna, los parámetros dinámicos y los valores de atributo de cadena) tienen un parámetro de longitud asociada. Si la aplicación termina las cadenas con el carácter null, como suele suceder en C, proporciona como argumento en la longitud en bytes de la cadena (sin incluir el terminador null) o SQL_NTS (Null-Terminated cadena). Un argumento de longitud no negativo, especifica la longitud real de la cadena asociada. El argumento de longitud puede ser 0 para especificar una cadena de longitud cero, que es distinta de un valor NULL. El valor negativo SQL_NTS dirige el controlador para determinar la longitud de la cadena localizando el carácter de terminación null.  
  
 Cuando se devuelven los datos de caracteres desde el controlador a la aplicación, el controlador debe siempre null-terminarlo. Esto ofrece la opción de si controlar los datos como una cadena o una matriz de caracteres a la aplicación. Si el búfer de aplicación no es lo suficientemente grande como para devolver todos los datos de caracteres, el controlador lo trunca a la longitud de bytes del búfer menos el número de bytes requeridos por el carácter de terminación null, los datos truncados termina en null y lo almacena en el búfer. Por lo tanto, las aplicaciones siempre deben asignar espacio adicional para el carácter de terminación null de búferes que utiliza para recuperar datos de caracteres. Por ejemplo, un búfer de bytes 51 es necesario para recuperar los 50 caracteres de datos.  
  
 Debe prestar especial atención a la aplicación y el controlador al enviar o recuperar datos de caracteres long en partes con **SQLPutData** o **SQLGetData**. Si los datos se pasan como una serie de cadenas terminadas en null, se deben quitar los caracteres de terminación null en estas cadenas antes de pueden volver a montarlas los datos.  
  
 Datos de caracteres y cadenas de C, dispone de confundir un número de programadores ODBC. Que se ha producido este es un artefacto de usar el lenguaje C al definir funciones de ODBC. Si una aplicación o el controlador ODBC utiliza otro idioma, recuerde que ODBC es independiente del lenguaje, esta confusión es menos probable que surgen.  
  
 Cuando las cadenas de C se utilizan para almacenar datos de caracteres, el carácter de terminación null no se considera parte de los datos y no se cuenta como parte de su longitud en bytes. Por ejemplo, se puede mantener lo datos de caracteres "ABC" como la cadena "ABC\0" de C o la matriz de caracteres {'A', 'B', 'C'}. La longitud de bytes de los datos es 3, si se trata como una cadena o una matriz de caracteres.  
  
 Aunque las aplicaciones y controladores normalmente utilizan cadenas de C (matrices de caracteres terminada en null) para almacenar datos de caracteres, no hay ningún requisito para hacer esto. En C, datos de caracteres también se pueden tratar como una matriz de caracteres (sin terminación null) y su longitud de bytes que se pasa por separado en el búfer de longitud/indicador.  
  
 Dado que se pueden contener datos de caracteres en una matriz de no terminación nula y su longitud de bytes se pasa por separado, es posible insertar caracteres nulos en los datos de caracteres. Sin embargo, el comportamiento de las funciones ODBC no está definido en este caso, y es específico del controlador si un controlador encarga de ello correctamente. Por lo tanto, aplicaciones interoperables siempre deben administrar los datos de caracteres que pueden contener caracteres nulos incrustados como datos binarios.
