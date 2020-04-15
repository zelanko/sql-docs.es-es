---
title: Ejemplo de exploración de SQL Server ( SQL Server) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b15aa8e3d573660a312fceb5b9100a41f0384d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301986"
---
# <a name="sql-server-browsing-example"></a>Ejemplo de exploración de SQL Server
En el ejemplo siguiente se muestra cómo **SQLBrowseConnect** podría usarse para examinar las conexiones disponibles con un controlador para SQL Server. En primer lugar, la aplicación solicita un identificador de conexión:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 A continuación, la aplicación llama a **SQLBrowseConnect** y especifica el controlador de SQL Server, utilizando la descripción del controlador devuelta por **SQLDrivers:**  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Dado que se trata de la primera llamada a **SQLBrowseConnect**, el Administrador de controladores carga el controlador de SQL Server y llama a la función **SQLBrowseConnect** del controlador con los mismos argumentos que recibió de la aplicación.  
  
> [!NOTE]  
>  Si se conecta a un proveedor de origen de `Trusted_Connection=yes` datos que admite la autenticación de Windows, debe especificar en lugar de la información de ID de usuario y contraseña en la cadena de conexión.  
  
 El controlador determina que se trata de la primera llamada a **SQLBrowseConnect** y devuelve el segundo nivel de atributos de conexión: servidor, nombre de usuario, contraseña, nombre de aplicación e ID de estación de trabajo. Para el atributo server, devuelve una lista de nombres de servidor válidos. El código de retorno de **SQLBrowseConnect** es SQL_NEED_DATA. Aquí está la cadena de resultado del examinar:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Cada palabra clave de la cadena de resultado de exploración va seguida de dos puntos y una o más palabras antes del signo igual. Estas palabras son el nombre fácil de usar que una aplicación puede usar para crear un cuadro de diálogo. Las palabras clave **APP** y **WSID** están precedidas por un asterisco, lo que significa que son opcionales. Las palabras clave **SERVER**, **UID**y **PWD** no tienen como prefijo un asterisco; se deben proporcionar valores para ellos en la siguiente cadena de solicitud de exploración. El valor de la palabra clave **SERVER** puede ser uno de los servidores devueltos por **SQLBrowseConnect** o un nombre proporcionado por el usuario.  
  
 La aplicación llama a **SQLBrowseConnect** de nuevo, especificando el servidor verde y omitiendo las palabras clave **APP** y **WSID** y los nombres fáciles de usar después de cada palabra clave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 El controlador intenta conectarse al servidor verde. Si hay errores no fatales, como un par palabra clave-valor que falta, **SQLBrowseConnect** devuelve SQL_NEED_DATA y permanece en el mismo estado que antes del error. La aplicación puede llamar a **SQLGetDiagField** o **SQLGetDiagRec** para determinar el error. Si la conexión se realiza correctamente, el controlador devuelve SQL_NEED_DATA y devuelve la cadena de resultado de exploración:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Dado que los atributos de esta cadena son opcionales, la aplicación puede omitirlos. Sin embargo, la aplicación debe llamar a **SQLBrowseConnect** de nuevo. Si la aplicación decide omitir el nombre y el idioma de la base de datos, especifica una cadena de solicitud de exploración vacía. En este ejemplo, la aplicación elige la base de datos pubs y llama a **SQLBrowseConnect** una hora final, omitiendo la palabra clave **LANGUAGE** y el asterisco antes de la palabra clave **DATABASE:**  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Dado que el atributo **DATABASE** es el atributo de conexión final requerido por el controlador, el proceso de exploración se ha completado, la aplicación está conectada al origen de datos y **SQLBrowseConnect** devuelve SQL_SUCCESS. **SQLBrowseConnect** también devuelve la cadena de conexión completa como la cadena de resultado de exploración:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 La cadena de conexión final devuelta por el controlador no contiene los nombres fáciles de usar después de cada palabra clave, ni contiene palabras clave opcionales no especificadas por la aplicación. La aplicación puede usar esta cadena con **SQLDriverConnect** para volver a conectarse al origen de datos en el identificador de conexión actual (después de desconectarse) o para conectarse al origen de datos en un identificador de conexión diferente. Por ejemplo:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
