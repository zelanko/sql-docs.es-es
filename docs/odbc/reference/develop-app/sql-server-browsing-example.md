---
description: Ejemplo de exploración de SQL Server
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14016832989c6fcba1dc39bc64434e72b049c18a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424567"
---
# <a name="sql-server-browsing-example"></a>Ejemplo de exploración de SQL Server
En el ejemplo siguiente se muestra cómo se puede usar **SQLBrowseConnect** para examinar las conexiones disponibles con un controlador para SQL Server. En primer lugar, la aplicación solicita un identificador de conexión:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 A continuación, la aplicación llama a **SQLBrowseConnect** y especifica el controlador SQL Server, mediante la descripción del controlador devuelta por **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Dado que se trata de la primera llamada a **SQLBrowseConnect**, el administrador de controladores carga el controlador de SQL Server y llama a la función **SQLBrowseConnect** del controlador con los mismos argumentos que recibió de la aplicación.  
  
> [!NOTE]  
>  Si se va a conectar a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar `Trusted_Connection=yes` en lugar de la información de ID. de usuario y contraseña en la cadena de conexión.  
  
 El controlador determina que se trata de la primera llamada a **SQLBrowseConnect** y devuelve el segundo nivel de atributos de conexión: servidor, nombre de usuario, contraseña, nombre de la aplicación e identificador de la estación de trabajo. En el caso del atributo Server, devuelve una lista de nombres de servidor válidos. El código de retorno de **SQLBrowseConnect** es SQL_NEED_DATA. Esta es la cadena de resultado de la exploración:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Cada palabra clave de la cadena de resultado de la exploración va seguida de dos puntos y una o varias palabras antes del signo igual. Estas palabras son el nombre descriptivo que puede utilizar una aplicación para crear un cuadro de diálogo. Las palabras clave **App** y **WSID** están precedidas por un asterisco, lo que significa que son opcionales. Las palabras clave **Server**, **UID**y **pwd** no tienen un asterisco como prefijo. se deben proporcionar valores para ellos en la siguiente cadena de solicitud de examen. El valor de la palabra clave **Server** puede ser uno de los servidores devueltos por **SQLBrowseConnect** o un nombre proporcionado por el usuario.  
  
 La aplicación llama a **SQLBrowseConnect** de nuevo, especificando el servidor verde y omitiendo las palabras clave **App** y **WSID** y los nombres descriptivos después de cada palabra clave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 El controlador intenta conectarse al servidor verde. Si hay algún error no irrecuperable, como un par de palabra clave-valor que falta, **SQLBrowseConnect** devuelve SQL_NEED_DATA y permanece en el mismo estado que tenía antes del error. La aplicación puede llamar a **SQLGetDiagField** o **SQLGetDiagRec** para determinar el error. Si la conexión es correcta, el controlador devuelve SQL_NEED_DATA y devuelve la cadena de resultado de la exploración:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Dado que los atributos de esta cadena son opcionales, la aplicación puede omitirlos. Sin embargo, la aplicación debe volver a llamar a **SQLBrowseConnect** . Si la aplicación decide omitir el nombre y el idioma de la base de datos, especifica una cadena de solicitud de exploración vacía. En este ejemplo, la aplicación elige la base de datos pubs y llama a **SQLBrowseConnect** una hora final, omitiendo la palabra clave **Language** y el asterisco antes de la palabra clave **Database** :  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Dado que el atributo de **base** de datos es el atributo de conexión final requerido por el controlador, el proceso de exploración se completa, la aplicación se conecta al origen de datos y **SQLBrowseConnect** devuelve SQL_SUCCESS. **SQLBrowseConnect** también devuelve la cadena de conexión completa como la cadena de resultado de la exploración:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 La cadena de conexión final devuelta por el controlador no contiene los nombres descriptivos después de cada palabra clave, ni contiene palabras clave opcionales no especificadas por la aplicación. La aplicación puede utilizar esta cadena con **SQLDriverConnect** para volver a conectar con el origen de datos en el identificador de conexión actual (después de desconectar) o para conectarse al origen de datos en un identificador de conexión diferente. Por ejemplo:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
