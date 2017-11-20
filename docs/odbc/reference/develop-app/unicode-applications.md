---
title: Las aplicaciones de Unicode | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c99c74a1a294d7d43774fe9d53d169eece98d3ad
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="unicode-applications"></a>Aplicaciones de Unicode
Puede volver a compilar una aplicación como una aplicación de Unicode de dos maneras:  
  
-   Incluir el Unicode **#define** contenidos en el archivo de encabezado Sqlucode.h en la aplicación.  
  
-   Compile la aplicación con la opción del compilador Unicode. (Esta opción estará diferente para los compiladores diferentes.)  
  
 Para convertir una aplicación de ANSI a una aplicación de Unicode, escribir la aplicación para almacenar y pasar datos Unicode. Además, las llamadas a funciones que admiten argumentos SQLPOINTER deben convertirse para utilizar el recuento de bytes.  
  
 Después de que una aplicación se compila como una aplicación de Unicode, si la aplicación llama a una función API de ODBC (sin sufijo), el Administrador de controladores reconoce la aplicación como una aplicación Unicode y convierte la llamada de función a una función de Unicode (con el  *W* sufijo) si el controlador subyacente es compatible con Unicode. Cuando una aplicación ANSI realiza una función llamada sin un sufijo, el Administrador de controladores se convierte en ANSI si el controlador subyacente es compatible con ANSI. Si la aplicación y el controlador admiten la misma codificación de caracteres, el Administrador de controladores pasa las llamadas a través del controlador (con ciertas excepciones para las aplicaciones ANSI).  
  
 Una aplicación puede llamar a las funciones de Unicode (con la *W* sufijo) y funciones de ANSI (con o sin el *A* sufijo). Se pueden mezclar Unicode y ANSI llamadas a función. Si es la biblioteca de cursores que se usará, sin embargo, Unicode y ANSI llamadas a funciones no se pueden mezclar. La biblioteca de cursores es Unicode o ANSI, no una combinación.  
  
 Una aplicación puede escribirse de forma que puede compilarse como una aplicación Unicode o una aplicación de ANSI. En este caso, los tipos de datos de caracteres se pueden declarar como SQL_C_TCHAR. Se trata de una macro que inserta SQL_C_WCHAR si la aplicación se compila como una aplicación Unicode o inserta SQL_C_CHAR si se ha compilado como una aplicación de ANSI. El programador de aplicaciones debe tener cuidado de funciones que toman SQLPOINTER como su argumento, ya que cambia el tamaño del argumento de longitud (para tipos de datos de cadena) dependiendo de si la aplicación es ANSI o Unicode.  
  
 Puede llamar a una función de una de estas tres maneras: como una llamada de función exclusivas de Unicode (con la *W* sufijo), como una llamada de función solo ANSI (con la *A* sufijo), o como la llamada de función ODBC sin sufijo. Los argumentos de las tres formas de una función son idénticos. Sólo las funciones con SQLCHAR \* argumentos o argumentos SQLPOINTER que señalan a las cadenas requieren formularios Unicode y ANSI. Para las funciones que tienen argumentos que se pueden declarar como un tipo de caracteres, como **SQLBindCol** o **SQLGetData** (que no tiene formas Unicode y ANSI), el argumento se puede declarar como el tipo de Unicode el ANSI escriba, o en el caso de una C, la macro SQL_C_TCHAR el argumento de tipo. Para obtener más información, consulte [datos Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Una aplicación puede escribirse como una aplicación de Unicode, incluso si no hay controladores de Unicode están disponibles para que funcione con. El Administrador de controladores se asignarán los tipos de datos y funciones de Unicode a ANSI. Hay algunas restricciones a la Unicode para las asignaciones de ANSI que se pueden realizar. La existencia de un controlador de Unicode para que funcione con la aplicación de Unicode dará como resultado un mejor rendimiento y quitará las limitaciones inherentes en Unicode para asignaciones de ANSI.

