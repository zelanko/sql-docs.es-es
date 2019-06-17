---
title: Ejemplo de exploración de SQL Server | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8dc57d738c1d5726d2208b930c5d4fadcd93b39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149318"
---
# <a name="sql-server-browsing-example"></a>Ejemplo de exploración de SQL Server
El ejemplo siguiente se muestra cómo **SQLBrowseConnect** podría utilizarse para examinar las conexiones disponibles con un controlador para SQL Server. En primer lugar, la aplicación solicita un identificador de conexión:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 A continuación, la aplicación llama a **SQLBrowseConnect** y especifica el controlador de SQL Server, utilizando la descripción del controlador devuelta por **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Se trata de la primera llamada a **SQLBrowseConnect**, el Administrador de controladores se carga el controlador de SQL Server y se llama al controlador **SQLBrowseConnect** canónica con los mismos argumentos que recibió de la aplicación.  
  
> [!NOTE]  
>  Si se conecta a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar `Trusted_Connection=yes` en lugar de la información de identificador y la contraseña de usuario en la cadena de conexión.  
  
 El controlador determina que se trata de la primera llamada a **SQLBrowseConnect** y devuelve el segundo nivel de los atributos de conexión: servidor, nombre de usuario, contraseña, nombre de la aplicación y el identificador de estación de trabajo Para el atributo de servidor, devuelve una lista de nombres de servidor válido. El código de retorno de **SQLBrowseConnect** es SQL_NEED_DATA. Esta es la cadena de resultado de examinar:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Cada palabra clave en la cadena de resultado de examinar va seguido de dos puntos y una o varias palabras antes del signo igual. Estas palabras son el nombre descriptivo que una aplicación puede usar para crear un cuadro de diálogo. El **aplicación** y **WSID** palabras clave van precedidas por un asterisco, lo que significa que son opcionales. El **SERVER**, **UID**, y **PWD** palabras clave no están precedidas por un asterisco; los valores se deben proporcionar para ellos en la siguiente cadena de solicitud de exploración. El valor de la **SERVER** palabra clave puede ser uno de los servidores devueltos por **SQLBrowseConnect** o un nombre proporcionado por el usuario.  
  
 La aplicación llama a **SQLBrowseConnect** de nuevo, especificando el servidor de color verde y omitir el **aplicación** y **WSID** las palabras clave y los nombres descriptivos después de cada palabra clave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 El controlador intenta conectarse al servidor verde. Si hay algún error recuperable, como un par de palabra clave y valor que falta, **SQLBrowseConnect** devuelve SQL_NEED_DATA y permanece en el mismo estado que tenía antes del error. La aplicación puede llamar a **SQLGetDiagField** o **SQLGetDiagRec** para determinar el error. Si la conexión es correcta, el controlador devuelve SQL_NEED_DATA y devuelve la cadena de resultado de examinar:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Dado que los atributos de esta cadena son opcionales, la aplicación puede omitirlas. Sin embargo, la aplicación debe llamar a **SQLBrowseConnect** nuevo. Si elige la aplicación omitir el nombre de la base de datos y el idioma, especifica una cadena de solicitud vacío Examinar. En este ejemplo, la aplicación elige la base de datos pubs y llama a **SQLBrowseConnect** una última vez, si se omite el **LENGUAJE** palabra clave y el asterisco delante de la **delabasededatos**palabra clave:  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Dado que el **base de datos** es el atributo de conexión final requerido por el controlador, el proceso de exploración completada, la aplicación está conectada al origen de datos, y **SQLBrowseConnect** Devuelve SQL_SUCCESS. **SQLBrowseConnect** también devuelve la cadena de conexión completa como la cadena de resultado de examinar:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 La cadena de conexión final devuelta por el controlador no contiene los nombres descriptivos después de cada palabra clave ni contiene palabras clave opcionales no especificadas por la aplicación. La aplicación puede utilizar esta cadena con **SQLDriverConnect** para volver a conectarse al origen de datos en el identificador de conexión actual (después de desconectar) o para conectarse al origen de datos en un identificador de conexión diferentes. Por ejemplo:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
