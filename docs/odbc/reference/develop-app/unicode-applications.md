---
title: Las aplicaciones de Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fc9cb98837d206d5279d1f14d4a57ce56782759
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633385"
---
# <a name="unicode-applications"></a>Aplicaciones de Unicode
Puede volver a compilar una aplicación como una aplicación de Unicode de dos maneras:  
  
-   Incluir el Unicode **#define** contenidos en el archivo de encabezado Sqlucode.h en la aplicación.  
  
-   Compile la aplicación con la opción del compilador Unicode. (Esta opción estará diferente para diferentes compiladores.)  
  
 Para convertir una aplicación de ANSI a una aplicación de Unicode, escribir la aplicación para almacenar y pasar datos Unicode. Además, las llamadas a funciones que admiten argumentos SQLPOINTER deben convertirse para usar el recuento de bytes.  
  
 Después de una aplicación se compila como una aplicación de Unicode, si la aplicación llama a una función de la API de ODBC (sin sufijo), el Administrador de controladores reconoce la aplicación como una aplicación de Unicode y convierte la llamada de función a una función de Unicode (con el  *W* sufijo) si el controlador subyacente es compatible con Unicode. Cuando una aplicación ANSI realiza una función llamada sin un sufijo, el Administrador de controladores lo convierte en ANSI si el controlador subyacente es compatible con ANSI. Si la aplicación y el controlador es compatible con la misma codificación de caracteres, el administrador del controlador pasa las llamadas a través del controlador (con algunas excepciones para las aplicaciones ANSI).  
  
 Una aplicación puede llamar a ambas funciones Unicode (con el *W* sufijo) y funciones de ANSI (con o sin el *A* sufijo). Unicode y ANSI llamadas a funciones se pueden combinar. Si es la biblioteca de cursores que se usará, sin embargo, las llamadas de función de Unicode y ANSI no se pueden mezclar. La biblioteca de cursores es Unicode o ANSI, no una combinación.  
  
 Forma que se puede compilar como una aplicación Unicode o una aplicación ANSI, se puede escribir una aplicación. En este caso, los tipos de datos de caracteres se pueden declarar como SQL_C_TCHAR. Se trata de una macro que inserta SQL_C_WCHAR si la aplicación se compila como una aplicación Unicode o inserta SQL_C_CHAR si se ha compilado como una aplicación de ANSI. El programador de aplicaciones debe tener cuidado de las funciones que toman SQLPOINTER como su argumento, ya que cambiará el tamaño del argumento de longitud (para tipos de datos de cadena) dependiendo de si la aplicación es ANSI o Unicode.  
  
 Una función se puede llamar en una de estas tres maneras: como una llamada de función exclusivas de Unicode (con el *W* sufijo), como una llamada de función solo ANSI (con el *A* sufijo), o como la llamada de función ODBC sin sufijo. Los argumentos de las tres formas de una función son idénticos. Solo las funciones con SQLCHAR \* argumentos o argumentos SQLPOINTER que señalan a las cadenas requieren formularios Unicode y ANSI. Para las funciones que tienen argumentos que se pueden declarar como un tipo de carácter, como **SQLBindCol** o **SQLGetData** (que no tienen formularios Unicode y ANSI), el argumento se puede declarar como el tipo de Unicode el ANSI escriba, o en el caso de una C, la macro SQL_C_TCHAR el argumento de tipo. Para obtener más información, consulte [datos Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Una aplicación puede escribirse como una aplicación de Unicode, incluso si no están disponibles para que funcione con controladores Unicode. El Administrador de controladores se asignarán los tipos de funciones y datos Unicode a ANSI. Hay algunas restricciones a Unicode para asignaciones de ANSI que se pueden realizar. La existencia de un controlador de Unicode para que funcione con la aplicación de Unicode dará como resultado un mejor rendimiento y quitará las limitaciones inherentes en Unicode para asignaciones de ANSI.
