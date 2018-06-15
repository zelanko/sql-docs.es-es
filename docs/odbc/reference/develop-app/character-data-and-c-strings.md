---
title: Caracteres de datos y cadenas de C | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c23f124aeba138e0ffecc432f28fde4c11c7d1b2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912390"
---
# <a name="character-data-and-c-strings"></a>Datos de caracteres y cadenas de c.
Parámetros de entrada que hacen referencia a datos de caracteres de longitud variable (como nombres de columna, los parámetros dinámicos y los valores de atributo de cadena) tienen un parámetro de longitud asociada. Si la aplicación termina cadenas con el carácter null, tal y como es habitual en C, proporciona como argumento a la longitud en bytes de la cadena (sin incluir el terminador null) o SQL_NTS (String Null-Terminated). Un argumento de longitud no negativo especifica la longitud real de la cadena asociada. El argumento de longitud puede ser 0 para especificar una cadena de longitud cero, que es distinta de un valor NULL. El valor negativo SQL_NTS indica al controlador para determinar la longitud de la cadena, localizando el carácter de terminación null.  
  
 Cuando el controlador devuelve datos de caracteres a la aplicación, el controlador debe siempre null-finalícela. Esto ofrece la opción si va a administrar los datos como una cadena o una matriz de caracteres a la aplicación. Si el búfer de aplicación no es lo suficientemente grande como para devolver todos los datos de caracteres, el controlador lo trunca a la longitud de bytes del búfer menos el número de bytes requeridos por el carácter de terminación null, los datos truncados termina en null y lo almacena en el búfer. Por lo tanto, las aplicaciones siempre deben asignar espacio adicional para el carácter de terminación null de búferes utilizados para recuperar datos de caracteres. Por ejemplo, un búfer de bytes de 51 es necesaria para recuperar 50 caracteres de datos.  
  
 Debe prestar especial atención a la aplicación y el controlador al enviar o recuperar datos de caracteres long en partes con **SQLPutData** o **SQLGetData**. Si los datos se pasan como una serie de cadenas terminadas en null, los caracteres de terminación null en estas cadenas deben eliminarse antes de que los datos pueden reensamblarse.  
  
 Un número de programadores ODBC ha confundir los datos de caracteres y cadenas de C. Que se ha producido este es un artefacto de mediante el lenguaje de C al definir las funciones ODBC. Si una aplicación o el controlador ODBC utiliza otro idioma, recuerde que ODBC es independiente del lenguaje: esta confusión es menos probable que surgen.  
  
 Cuando las cadenas de C se utilizan para contener datos de caracteres, el carácter de terminación null no se considera parte de los datos y no se cuenta como parte de su longitud de bytes. Por ejemplo, se pueden almacenar lo datos de caracteres "ABC" como la cadena de C "ABC\0" o la matriz de caracteres {'A', 'B', 'C'}. La longitud de bytes de los datos es 3, si no se trata como una cadena o una matriz de caracteres.  
  
 Aunque las aplicaciones y controladores normalmente utilizan cadenas de C (matrices de caracteres terminada en null) para almacenar datos de caracteres, no hay ningún requisito para hacerlo. En C, los datos de caracteres también se pueden tratar como una matriz de caracteres (sin terminación null) y su longitud de bytes que se pasa por separado en el búfer de longitud/indicador.  
  
 Dado que se pueden contener datos de caracteres en una matriz no terminada null y su longitud de bytes pasa por separado, es posible incrustar caracteres nulos en los datos de caracteres. Sin embargo, el comportamiento de las funciones ODBC en este caso no está definido y es específico del controlador si un controlador encarga de ello correctamente. Por lo tanto, aplicaciones interoperables siempre deben administrar los datos de caracteres que pueden contener los caracteres nulos incrustados como datos binarios.
