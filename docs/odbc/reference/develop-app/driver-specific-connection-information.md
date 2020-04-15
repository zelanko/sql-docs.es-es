---
title: Información de conexión específica del conductor (Driver-Specific Connection Information) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16c8c5fc4fd3ac63aa3613b41e530446dffec118
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305796"
---
# <a name="driver-specific-connection-information"></a>Información de conexión específicos del controlador
**SQLConnect** supone que un nombre de origen de datos, un identificador de usuario y una contraseña son suficientes para conectarse a un origen de datos y que toda la otra información de conexión se puede almacenar en el sistema. Con frecuencia no es así. Por ejemplo, un controlador puede necesitar un ID de usuario y una contraseña para iniciar sesión en un servidor y un ID de usuario y una contraseña diferentes para iniciar sesión en un DBMS. Dado que **SQLConnect** acepta un único ID de usuario y contraseña, esto significa que el otro ID de usuario y contraseña deben almacenarse con la información del origen de datos en el sistema si se va a utilizar **SQLConnect.** Esto es una posible violación de la seguridad y debe evitarse a menos que la contraseña esté cifrada.  
  
 **SQLDriverConnect** permite al controlador definir una cantidad arbitraria de información de conexión en los pares palabra clave-valor de la cadena de conexión. Por ejemplo, supongamos que un controlador requiere un nombre de origen de datos, un ID de usuario y una contraseña para el servidor, y un ID de usuario y una contraseña para el DBMS. Un programa personalizado que siempre utiliza el origen de datos XYZ Corp podría solicitar al usuario ID y contraseñas y crear el siguiente conjunto de pares palabra clave-valor, o cadena de *conexión,* para pasar a **SQLDriverConnect:**  
  
> [!NOTE]  
>  Si se conecta a un proveedor de origen de `Trusted_Connection=yes` datos que admite la autenticación de Windows, debe especificar en lugar de la información de ID de usuario y contraseña en la cadena de conexión.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 La palabra clave **DSN** (Nombre de origen de datos) nombra el origen de datos, las palabras clave **UID** y **PWD** especifican el ID de usuario y la contraseña para el servidor, y las palabras clave **UIDDBMS** y **PWDDBMS** especifican el ID de usuario y la contraseña para el DBMS. Observe que el punto y coma final es opcional. **SQLDriverConnect** analiza esta cadena; utiliza el nombre del origen de datos XYZ Corp para recuperar información de conexión adicional del sistema, como la dirección del servidor; e inicia sesión en el servidor y DBMS utilizando los ID de usuario y las contraseñas especificados.  
  
 Los pares palabra clave-valor en **SQLDriverConnect** deben seguir ciertas reglas de sintaxis. Las palabras clave y sus valores no deben contener el **[]{}(),;? \*Caracteres** de la cuenta. El valor de la palabra clave **DSN** no puede constar únicamente de espacios en blanco y no debe contener espacios en blanco iniciales. Debido a la gramática del Registro, las palabras\\clave y los nombres de origen de datos no pueden contener el carácter de barra diagonal inversa ( ). No se permiten espacios alrededor del signo igual en el par palabra clave-valor.  
  
 La palabra clave **FILEDSN** se puede utilizar en una llamada a **SQLDriverConnect** para especificar el nombre de un archivo que contiene información del origen de datos (consulte Conexión mediante [orígenes](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)de datos de archivo , más adelante en esta sección). La palabra clave **SAVEFILE** se puede utilizar para especificar el nombre de un archivo .dsn en el que se guardarán los pares palabra clave-valor de una conexión correcta realizada por la llamada a **SQLDriverConnect.** Para obtener más información acerca de los orígenes de datos de archivo, vea la descripción de la función [SQLDriverConnect.](../../../odbc/reference/syntax/sqldriverconnect-function.md)
