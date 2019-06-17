---
title: Información de conexión específicos del controlador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3852e713e517828e83e74bf7fb291ef20865532
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238703"
---
# <a name="driver-specific-connection-information"></a>Información de conexión específicos del controlador
**SQLConnect** se da por supuesto que un nombre de origen de datos, Id. de usuario y contraseña son suficientes para conectarse a un origen de datos y que se puede almacenar todos los demás información de conexión en el sistema. Con frecuencia esto no es el caso. Por ejemplo, es posible que un controlador, un identificador de usuario y contraseña para iniciar sesión en un servidor y un identificador de usuario diferente y una contraseña para iniciar sesión en un sistema DBMS. Dado que **SQLConnect** acepta un Id. de usuario único y una contraseña, esto significa que el otro Id. de usuario y la contraseña deben almacenarse con la información de origen de datos en el sistema si **SQLConnect** va a usar. Esto es una posible infracción de seguridad y debe evitarse, a menos que la contraseña se cifra.  
  
 **SQLDriverConnect** permite definir una cantidad arbitraria de información de conexión en los pares palabra clave-valor de la cadena de conexión al controlador. Por ejemplo, suponga que un controlador requiere un nombre de origen de datos, un Id. de usuario y una contraseña para el servidor y un Id. de usuario y una contraseña para el DBMS. Podría preguntar al usuario para los identificadores y contraseñas y cree el siguiente conjunto de pares de palabra clave y valor, un programa personalizado que utiliza siempre el origen de datos XYZ Corp o *cadena de conexión,* para pasar a **SQLDriverConnect**:  
  
> [!NOTE]  
>  Si se conecta a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar `Trusted_Connection=yes` en lugar de la información de identificador y la contraseña de usuario en la cadena de conexión.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 El **DSN** palabra clave (nombre de origen de datos) da nombre al origen de datos, el **UID** y **PWD** palabras clave que especifican el identificador de usuario y la contraseña para el servidor y el **UIDDBMS**  y **PWDDBMS** palabras clave especifican el Id. de usuario y la contraseña para el DBMS. Tenga en cuenta que el punto y coma final es opcional. **SQLDriverConnect** analiza esta cadena; usa el nombre del origen de datos XYZ Corp para recuperar información de conexión adicional desde el sistema, como la dirección del servidor; e inicia sesión en el servidor y el DBMS con los identificadores de usuario especificado y las contraseñas.  
  
 En los pares palabra clave-valor **SQLDriverConnect** debe seguir ciertas reglas de sintaxis. ¿Las palabras clave y sus valores no deben contener el **[]{}(),? \*=! @** caracteres. El valor de la **DSN** palabra clave no puede constar sólo de espacios en blanco y no debe contener espacios en blanco iniciales. Debido a la gramática del registro, los nombres de origen de datos y las palabras clave no pueden contener la barra diagonal inversa (\\) caracteres. No se permiten espacios alrededor del signo igual en el par de palabra clave y valor.  
  
 El **FILEDSN** palabra clave puede utilizarse en una llamada a **SQLDriverConnect** para especificar el nombre de un archivo que contiene información de origen de datos (consulte [conectarse utilizando archivo de orígenes de datos](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), más adelante en esta sección). El **SAVEFILE** palabra clave puede utilizarse para especificar el nombre de un archivo de DSN en el que se realizan los pares palabra clave-valor de una conexión correcta mediante la llamada a **SQLDriverConnect** se guardarán. Para obtener más información acerca de los orígenes de datos de archivo, consulte el [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.
