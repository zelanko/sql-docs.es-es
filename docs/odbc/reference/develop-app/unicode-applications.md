---
title: Aplicaciones Unicode | Microsoft Docs
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
ms.openlocfilehash: 32b4125d0ecb1f15fab00119a8ef4ed361b6db72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087739"
---
# <a name="unicode-applications"></a>Aplicaciones de Unicode
Puede volver a compilar una aplicación como una aplicación Unicode de una de estas dos maneras:  
  
-   Incluya el **#define** Unicode contenido en el archivo de encabezado Sqlucode. h en la aplicación.  
  
-   Compile la aplicación con la opción Unicode del compilador. (Esta opción será diferente para los distintos compiladores).  
  
 Para convertir una aplicación ANSI en una aplicación Unicode, escriba la aplicación para almacenar y pasar datos Unicode. Además, las llamadas a funciones que admiten argumentos de SQLPOINTER se deben convertir para usar el recuento de bytes.  
  
 Después de compilar una aplicación como una aplicación Unicode, si la aplicación llama a una función de la API de ODBC (sin sufijo), el administrador de controladores reconoce la aplicación como una aplicación Unicode y convierte la llamada de función en una función Unicode (con el sufijo *W* ) si el controlador subyacente es compatible con Unicode. Cuando una aplicación ANSI realiza una llamada de función sin un sufijo, el administrador de controladores la convierte en ANSI si el controlador subyacente admite ANSI. Si tanto la aplicación como el controlador admiten la misma codificación de caracteres, el administrador de controladores pasa las llamadas a través del controlador (con ciertas excepciones para las aplicaciones ANSI).  
  
 Una aplicación puede llamar a las funciones Unicode (con el sufijo *W* ) y a las funciones ANSI (con o *sin el sufijo* ). Se pueden mezclar llamadas a funciones Unicode y ANSI. Sin embargo, si se va a utilizar la biblioteca de cursores, no se pueden mezclar llamadas a funciones Unicode y ANSI. La biblioteca de cursores es Unicode o ANSI, no una combinación.  
  
 Una aplicación se puede escribir de modo que se pueda compilar como una aplicación Unicode o ANSI. En este caso, los tipos de datos de caracteres se pueden declarar como SQL_C_TCHAR. Se trata de una macro que inserta SQL_C_WCHAR si la aplicación se compila como una aplicación Unicode o inserta SQL_C_CHAR si se compila como una aplicación ANSI. El programador de la aplicación debe tener cuidado con las funciones que toman SQLPOINTER como argumento, ya que el tamaño del argumento de longitud cambiará (para los tipos de datos de cadena) en función de si la aplicación es ANSI o Unicode.  
  
 Se puede llamar a una función de una de estas tres maneras: como una llamada de función solo Unicode (con el sufijo *W* ), como una llamada de función ANSI (con *el sufijo* ) o como la llamada a la función ODBC sin sufijo. Los argumentos para las tres formas de una función son idénticos. Solo las funciones con argumentos \* SQLCHAR o SQLPOINTER que apuntan a cadenas requieren formatos ANSI y Unicode. En el caso de las funciones que tienen argumentos que se pueden declarar como un tipo de carácter, como **SQLBindCol** o **SQLGetData** (que no tienen formatos Unicode y ANSI), el argumento se puede declarar como el tipo Unicode, el tipo ANSI o, en el caso de un argumento de tipo C, la macro SQL_C_TCHAR. Para obtener más información, vea [datos Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Una aplicación se puede escribir como una aplicación Unicode, incluso si no hay controladores Unicode disponibles para que funcione. El administrador de controladores asignará funciones y tipos de datos Unicode a ANSI. Existen algunas restricciones a las asignaciones de Unicode a ANSI que se pueden realizar. La existencia de un controlador Unicode para que funcione la aplicación Unicode dará como resultado un mejor rendimiento y eliminará las restricciones inherentes a las asignaciones de Unicode a ANSI.
