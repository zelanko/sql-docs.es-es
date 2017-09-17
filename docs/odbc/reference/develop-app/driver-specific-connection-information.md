---
title: "Información de conexión específicos del controlador | Documentos de Microsoft"
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
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9e1624febc9b53c654c1b01f5aafb601b97b3cbf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="driver-specific-connection-information"></a>Información de conexión específicos del controlador
**SQLConnect** se da por supuesto que un nombre de origen de datos, el Id. de usuario y la contraseña son suficientes para conectarse a un origen de datos y que todos los demás información de conexión se puede almacenar en el sistema. Esto sucede con frecuencia no. Por ejemplo, un controlador que tenga un identificador de usuario y contraseña para iniciar sesión en un servidor y un identificador de usuario diferente y una contraseña para iniciar sesión en un DBMS. Dado que **SQLConnect** acepta un Id. de usuario único y una contraseña, esto significa que el otro Id. de usuario y la contraseña deben almacenarse con la información de origen de datos en el sistema si **SQLConnect** va a usar. Esto es una posible infracción de seguridad y debe evitarse, a menos que la contraseña se cifra.  
  
 **SQLDriverConnect** permite al controlador definir una cantidad arbitraria de información de conexión en los pares de palabra clave y valor de la cadena de conexión. Por ejemplo, suponga que un controlador requiere un nombre de origen de datos, un Id. de usuario y una contraseña para el servidor y un Id. de usuario y una contraseña para el DBMS. Un programa personalizado que utiliza siempre el origen de datos XYX Corp podría preguntar al usuario para los identificadores y las contraseñas y generar el siguiente conjunto de pares de palabra clave y valor, o *cadena de conexión,* para pasar a **SQLDriverConnect**:  
  
> [!NOTE]  
>  Si se conecta a un proveedor de origen de datos que admita la autenticación de Windows, debe especificar `Trusted_Connection=yes` en lugar de la información de identificador y la contraseña de usuario en la cadena de conexión.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 El **DSN** palabra clave (nombre de origen de datos) nombre al origen de datos, el **UID** y **PWD** palabras clave que especifican el Id. de usuario y la contraseña para el servidor y el **UIDDBMS ** y **PWDDBMS** palabras clave especifica el Id. de usuario y la contraseña del DBMS. Tenga en cuenta que el punto y coma final es opcional. **SQLDriverConnect** analiza esta cadena; utiliza el nombre del origen de datos XYX Corp para recuperar la información de conexión adicionales del sistema, como la dirección del servidor; e inicia una sesión en el servidor y el DBMS con los identificadores de usuario especificado y las contraseñas.  
  
 Pares de palabra clave y valor en **SQLDriverConnect** deben seguir ciertas reglas de sintaxis. ¿Las palabras clave y sus valores no deben contener el **[] {} (),? \*=! @** caracteres. El valor de la **DSN** palabra clave no puede constar únicamente de espacios en blanco y no debe contener espacios en blanco iniciales. Debido a la gramática del registro, los nombres de origen de datos y palabras clave no pueden contener la barra diagonal inversa (\\) caracteres. No se permiten espacios alrededor del signo igual en el par de palabra clave y valor.  
  
 El **FILEDSN** palabra clave puede utilizarse en una llamada a **SQLDriverConnect** para especificar el nombre de un archivo que contiene información de origen de datos (vea [conectarse utilizando archivo orígenes de datos](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), más adelante en esta sección). El **SAVEFILE** palabra clave puede utilizarse para especificar el nombre de un archivo .dsn en los que los pares de palabra clave y valor de una conexión correcta realizan por la llamada a **SQLDriverConnect** se guardarán. Para obtener más información acerca de los orígenes de datos de archivo, consulte la [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.
