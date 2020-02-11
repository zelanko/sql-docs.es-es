---
title: Datos de caracteres y cadenas de C | Microsoft Docs
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
ms.openlocfilehash: ed99ab72e3d5112588a0b1c93df34b01aff7acdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044919"
---
# <a name="character-data-and-c-strings"></a>Datos de caracteres y cadenas de c
Los parámetros de entrada que hacen referencia a los datos de caracteres de longitud variable (como los nombres de columna, los parámetros dinámicos y los valores de atributo de cadena) tienen un parámetro de longitud asociado. Si la aplicación termina cadenas con el carácter nulo, como es habitual en C, proporciona como argumento la longitud en bytes de la cadena (sin incluir el terminador null) o SQL_NTS (cadena terminada en null). Un argumento de longitud no negativa especifica la longitud real de la cadena asociada. El argumento de longitud puede ser 0 para especificar una cadena de longitud cero, que es distinta de un valor NULL. El valor negativo SQL_NTS indica al controlador que determine la longitud de la cadena buscando el carácter de terminación de NULL.  
  
 Cuando los datos de caracteres se devuelven desde el controlador a la aplicación, el controlador siempre debe terminar en NULL. Esto permite a la aplicación elegir si se deben controlar los datos como una cadena o una matriz de caracteres. Si el búfer de aplicación no es lo suficientemente grande como para devolver todos los datos de caracteres, el controlador lo trunca a la longitud de bytes del búfer menos el número de bytes necesario para el carácter de terminación null, termina en NULL los datos truncados y los almacena en el búfer. Por lo tanto, las aplicaciones deben asignar siempre espacio adicional para el carácter de terminación null en los búferes que se usan para recuperar datos de caracteres. Por ejemplo, se necesita un búfer de 51 bytes para recuperar 50 caracteres de datos.  
  
 La aplicación y el controlador deben tener especial cuidado al enviar o recuperar datos de caracteres largos en partes con **SQLPutData** o **SQLGetData**. Si los datos se pasan como una serie de cadenas terminadas en null, se deben eliminar los caracteres de terminación null de estas cadenas antes de que se puedan reensamblar los datos.  
  
 Varios programadores de ODBC han confundido datos de caracteres y cadenas de C. Que esto se ha producido es un artefacto de usar el lenguaje C al definir funciones ODBC. Si una aplicación o un controlador ODBC utiliza otro lenguaje, recuerde que ODBC es independiente del lenguaje; es menos probable que se produzca esta confusión.  
  
 Cuando se usan cadenas de C para contener datos de caracteres, el carácter de terminación NULL no se considera parte de los datos y no se cuenta como parte de su longitud de bytes. Por ejemplo, los datos de caracteres "ABC" se pueden conservar como la cadena de C "ABC\0" o la matriz de caracteres {"A", "B", "C"}. La longitud de bytes de los datos es 3, independientemente de si se trata como una cadena o como una matriz de caracteres.  
  
 Aunque las aplicaciones y los controladores suelen usar cadenas de C (matrices de caracteres terminadas en null) para contener datos de caracteres, no hay ningún requisito para hacerlo. En C, los datos de caracteres también se pueden tratar como una matriz de caracteres (sin terminación nula) y su longitud de bytes se pasa por separado en el búfer de longitud/indicador.  
  
 Dado que los datos de caracteres se pueden mantener en una matriz no terminada en NULL y su longitud de bytes se pasa por separado, es posible incrustar caracteres nulos en los datos de caracteres. Sin embargo, el comportamiento de las funciones ODBC en este caso es undefined y es específico del controlador si un controlador lo controla correctamente. Por lo tanto, las aplicaciones interoperables siempre deben controlar los datos de caracteres que pueden contener caracteres nulos incrustados como datos binarios.
