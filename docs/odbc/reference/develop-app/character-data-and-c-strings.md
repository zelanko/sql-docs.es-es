---
title: Datos de caracteres y cadenas de C ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7bb25022d4e0c0559f2a8f77b89a4ba26aeba33a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307495"
---
# <a name="character-data-and-c-strings"></a>Datos de caracteres y cadenas de c
Los parámetros de entrada que hacen referencia a datos de caracteres de longitud variable (como nombres de columna, parámetros dinámicos y valores de atributo de cadena) tienen un parámetro de longitud asociado. Si la aplicación termina cadenas con el carácter nulo, como es típico en C, proporciona como argumento la longitud en bytes de la cadena (sin incluir el null-terminator) o SQL_NTS (Null-Terminated String). Un argumento de longitud no negativa especifica la longitud real de la cadena asociada. El argumento length puede ser 0 para especificar una cadena de longitud cero, que es distinta de un valor NULL. El valor negativo SQL_NTS indica al controlador que determine la longitud de la cadena localizando el carácter de terminación nula.  
  
 Cuando se devuelven datos de caracteres desde el controlador a la aplicación, el controlador siempre debe terminarlo en null. Esto proporciona a la aplicación la opción de controlar los datos como una cadena o una matriz de caracteres. Si el búfer de aplicación no es lo suficientemente grande como para devolver todos los datos de caracteres, el controlador los trunca a la longitud de bytes del búfer menos el número de bytes requeridos por el carácter de terminación nula, termina en null los datos truncados y los almacena en el búfer. Por lo tanto, las aplicaciones siempre deben asignar espacio adicional para el carácter de terminación nula en los búferes utilizados para recuperar datos de caracteres. Por ejemplo, se necesita un búfer de 51 bytes para recuperar 50 caracteres de datos.  
  
 Tanto la aplicación como el controlador deben tener especial cuidado al enviar o recuperar datos de caracteres largos en partes con **SQLPutData** o **SQLGetData**. Si los datos se pasan como una serie de cadenas terminadas en null, los caracteres de terminación nula de estas cadenas se deben quitar antes de que los datos se puedan volver a ensamblar.  
  
 Varios programadores ODBC han confundido los datos de caracteres y las cadenas C. Que esto se ha producido es un artefacto de uso del lenguaje C al definir funciones ODBC. Si un controlador ODBC o una aplicación utiliza otro lenguaje (recuerde que ODBC es independiente del lenguaje- es menos probable que surja esta confusión.  
  
 Cuando se utilizan cadenas C para contener datos de caracteres, el carácter de terminación nula no se considera parte de los datos y no se cuenta como parte de su longitud de byte. Por ejemplo, los datos de caracteres "ABC" se pueden mantener como la cadena C "ABC-0" o la matriz de caracteres "A", "B", "C". La longitud de bytes de los datos es 3, independientemente de si se trata como una cadena o una matriz de caracteres.  
  
 Aunque las aplicaciones y los controladores suelen utilizar cadenas C (matrices de caracteres terminadas en null) para contener datos de caracteres, no hay ningún requisito para hacerlo. En C, los datos de caracteres también se pueden tratar como una matriz de caracteres (sin terminación nula) y su longitud de byte se pasa por separado en el búfer de longitud/indicador.  
  
 Dado que los datos de caracteres se pueden mantener en una matriz no terminada en null y su longitud de byte se pasa por separado, es posible incrustar caracteres nulos en datos de caracteres. Sin embargo, el comportamiento de las funciones ODBC en este caso es indefinido y es específico del controlador si un controlador controla esto correctamente. Por lo tanto, las aplicaciones interoperables siempre deben controlar los datos de caracteres que pueden contener caracteres nulos incrustados como datos binarios.
