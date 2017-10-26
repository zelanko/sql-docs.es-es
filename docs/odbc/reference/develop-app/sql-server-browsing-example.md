---
title: Examen de ejemplo SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f344ce0a3830bbd79d6674cfd4d5961b973939e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sql-server-browsing-example"></a>Ejemplo de exploración de SQL Server
El siguiente ejemplo se muestra cómo **SQLBrowseConnect** podría utilizarse para examinar las conexiones disponibles con un controlador de SQL Server. En primer lugar, la aplicación solicita un identificador de conexión:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 Siguiente, la aplicación llama **SQLBrowseConnect** y especifica el controlador de SQL Server, utilizando la descripción del controlador devuelto por **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Puesto que esta es la primera llamada a **SQLBrowseConnect**, el Administrador de controladores, se carga el controlador de SQL Server y llama al controlador **SQLBrowseConnect** función con los mismos argumentos que recibió de la aplicación.  
  
> [!NOTE]  
>  Si se conecta a un proveedor de origen de datos que admita la autenticación de Windows, debe especificar `Trusted_Connection=yes` en lugar de la información de identificador y la contraseña de usuario en la cadena de conexión.  
  
 El controlador determina que se trata de la primera llamada a **SQLBrowseConnect** y devuelve el segundo nivel de atributos de conexión: servidor, nombre de usuario, contraseña, nombre de la aplicación e Id. de estación de trabajo. Para el atributo de servidor, devuelve una lista de nombres de servidor válido. El código de retorno **SQLBrowseConnect** es SQL_NEED_DATA. Aquí es la cadena de resultado de exploración:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Cada palabra clave en la cadena de resultado de examinar va seguido de dos puntos y una o varias palabras antes del signo igual. Estas palabras son el nombre descriptivo que una aplicación puede utilizar para crear un cuadro de diálogo. El **aplicación** y **WSID** palabras clave van precedida por un asterisco, lo que significa que son opcionales. El **SERVER**, **UID**, y **PWD** palabras clave no está precedida por un asterisco; valores se deben proporcionar para ellos en la siguiente cadena de solicitud de exploración. El valor de la **SERVER** palabra clave puede tener uno de los servidores devueltos por **SQLBrowseConnect** o un nombre proporcionado por el usuario.  
  
 La aplicación llama **SQLBrowseConnect** nuevo, especificando el servidor verde y se omiten los **aplicación** y **WSID** palabras clave y los nombres descriptivos después de cada palabra clave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 El controlador intenta conectarse al servidor de color verde. Si hay errores graves, como un par de palabra clave y valor que falta, **SQLBrowseConnect** devuelve SQL_NEED_DATA y permanece en el mismo estado que estaba antes del error. La aplicación puede llamar a **SQLGetDiagField** o **SQLGetDiagRec** para determinar el error. Si la conexión es correcta, el controlador devuelve SQL_NEED_DATA y devuelve la cadena de resultado de exploración:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Dado que los atributos de la cadena son opcionales, la aplicación puede omitirlas. Sin embargo, la aplicación debe llamar a **SQLBrowseConnect** nuevo. Si la aplicación decide omitir el nombre de la base de datos y el idioma, especifica una cadena de solicitud vacío Examinar. En este ejemplo, la aplicación elige la base de datos pubs y llama **SQLBrowseConnect** una hora final, si se omite la **LENGUAJE** palabra clave y el asterisco antes de la **delabasededatos**palabra clave:  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Dado que la **base de datos** es el atributo de conexión final requerido por el controlador, el proceso de exploración es completando, la aplicación está conectada al origen de datos, y **SQLBrowseConnect** Devuelve SQL_SUCCESS. **SQLBrowseConnect** también devuelve la cadena de conexión completa como la cadena de resultado de exploración:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 La cadena de conexión final devuelta por el controlador no contiene los nombres descriptivos después de cada palabra clave ni contiene palabras clave opcionales que no está especificado por la aplicación. La aplicación puede utilizar esta cadena con **SQLDriverConnect** para volver a conectarse al origen de datos en el identificador de conexión actual (después de desconectarse) o para conectarse al origen de datos en un identificador de conexión diferentes. Por ejemplo:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```

