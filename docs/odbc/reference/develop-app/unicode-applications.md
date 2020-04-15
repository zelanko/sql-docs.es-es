---
title: Aplicaciones Unicode ????????? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94bd5211c878904453624adb2acd0fe435ebc812
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298951"
---
# <a name="unicode-applications"></a>Aplicaciones de Unicode
Puede volver a compilar una aplicación como una aplicación Unicode de una de estas dos maneras:  
  
-   Incluya el **#define** Unicode contenido en el archivo de encabezado Sqlucode.h de la aplicación.  
  
-   Compile la aplicación con la opción Unicode del compilador. (Esta opción será diferente para diferentes compiladores.)  
  
 Para convertir una aplicación ANSI en una aplicación Unicode, escriba la aplicación para almacenar y pasar datos Unicode. Además, las llamadas a funciones que admiten argumentos SQLPOINTER se deben convertir para usar el recuento de bytes.  
  
 Después de compilar una aplicación como una aplicación Unicode, si la aplicación llama a una función de API ODBC (sin sufijo), el Administrador de controladores reconoce la aplicación como una aplicación Unicode y convierte la llamada de función en una función Unicode (con el sufijo *W)* si el controlador subyacente admite Unicode. Cuando una aplicación ANSI realiza una llamada de función sin sufijo, el Administrador de controladores la convierte a ANSI si el controlador subyacente admite ANSI. Si tanto la aplicación como el controlador admiten la misma codificación de caracteres, el administrador de controladores pasa las llamadas al controlador (con ciertas excepciones para las aplicaciones ANSI).  
  
 Una aplicación puede llamar a funciones Unicode (con el sufijo *W)* y a funciones ANSI (con o sin el sufijo *A).* Las llamadas a funciones Unicode y ANSI se pueden mezclar. Sin embargo, si se va a utilizar la biblioteca de cursores, las llamadas a funciones Unicode y ANSI no se pueden mezclar. La biblioteca de cursores es Unicode o ANSI, no una mezcla.  
  
 Una aplicación se puede escribir de forma que se pueda compilar como una aplicación Unicode o una aplicación ANSI. En este caso, los tipos de datos de caracteres se pueden declarar como SQL_C_TCHAR. Se trata de una macro que inserta SQL_C_WCHAR si la aplicación se compila como una aplicación Unicode o inserta SQL_C_CHAR si se compila como una aplicación ANSI. El programador de aplicaciones debe tener cuidado con las funciones que toman SQLPOINTER como argumento, porque el tamaño del argumento length cambiará (para los tipos de datos de cadena) dependiendo de si la aplicación es ANSI o Unicode.  
  
 Se puede llamar a una función de una de tres maneras: como una llamada de función solo Unicode (con el sufijo *W),* como una llamada de función solo ANSI (con el sufijo *A)* o como la llamada de función ODBC sin sufijo. Los argumentos de las tres formas de una función son idénticos. Solo las funciones \* con argumentos SQLCHAR o argumentos SQLPOINTER que apuntan a cadenas requieren formularios Unicode y ANSI. Para las funciones que tienen argumentos que se pueden declarar como un tipo de carácter, como **SQLBindCol** o **SQLGetData** (que no tienen formularios Unicode y ANSI), el argumento se puede declarar como el tipo Unicode, el tipo ANSI o, en el caso de un argumento de tipo C, la macro de SQL_C_TCHAR. Para obtener más información, consulte [Datos Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Una aplicación se puede escribir como una aplicación Unicode incluso si no hay controladores Unicode disponibles para que funcione. El Administrador de controladores asignará funciones Unicode y tipos de datos a ANSI. Hay algunas restricciones a las asignaciones Unicode a ANSI que se pueden realizar. La existencia de un controlador Unicode para que la aplicación Unicode funcione dará como resultado un mejor rendimiento y se eliminarán las restricciones inherentes a las asignaciones Unicode a ANSI.
