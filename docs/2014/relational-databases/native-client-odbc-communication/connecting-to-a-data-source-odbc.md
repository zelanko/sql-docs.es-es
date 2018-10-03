---
title: Conectarse a un origen de datos (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- checking connection states
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- SQLBrowseConnect function
- ODBC applications, connections
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLConnect function
- SQLDriveConnect function
- verifying connection states
- SQL Server Native Client ODBC driver, data sources
- SQL Server Native Client ODBC driver, connections
ms.assetid: ae30dd1d-06ae-452b-9618-8fd8cd7ba074
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0192e3b4bf295ad0590b26a6f3e77d94d76acd9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185725"
---
# <a name="connecting-to-a-data-source-odbc"></a>Conectar con un origen de datos (ODBC)
  Después de asignar el entorno y los identificadores de conexión y establecer los atributos de conexión, la aplicación se conecta al origen de datos o controlador. Hay tres funciones que puede utilizar para conectarse:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 Para obtener más información acerca de cómo realizar las conexiones a un origen de datos, incluidas las diversas opciones de cadena de conexión disponibles, consulte [Using Connection String Keywords with SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect** es la función de conexión más sencilla. Acepta tres parámetros: nombre del origen de datos, identificador de usuario y contraseña. Use **SQLConnect** cuando estos tres parámetros contienen toda la información necesaria para conectarse a la base de datos. Para ello, cree una lista de orígenes de datos mediante **SQLDataSources**; preguntar al usuario para un origen de datos, Id. de usuario y contraseña; y, a continuación, llame a **SQLConnect**.  
  
 **SQLConnect** supone que un nombre de origen de datos, Id. de usuario y contraseña son suficientes para conectarse a un origen de datos y que el origen de datos ODBC contiene toda la demás información el controlador ODBC necesita para realizar la conexión. A diferencia de [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) y [SQLBrowseConnect](../native-client-odbc-api/sqlbrowseconnect.md), **SQLConnect** no utiliza una cadena de conexión.  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect** se usa cuando se necesita más información que el nombre del origen de datos, el Id. de usuario y la contraseña. Uno de los parámetros para **SQLDriverConnect** es una cadena de conexión que contiene información específica del controlador. Puede usar **SQLDriverConnect** en lugar de **SQLConnect** por las razones siguientes:  
  
-   Para especificar la información específica del controlador durante la conexión.  
  
-   Para solicitar que el controlador solicite al usuario la información de conexión.  
  
-   Para conectarse sin utilizar un origen de datos ODBC.  
  
 El **SQLDriverConnect** cadena de conexión contiene una serie de pares de palabra clave y valor que especifique toda la información de conexión admitida por un controlador ODBC. Cada controlador admite las palabras clave de ODBC estándar (DSN, FILEDSN, DRIVER, UID, PWD y SAVEFILE) además de las palabras clave específicas del controlador para toda la información de conexión admitida por el controlador. **SQLDriverConnect** se puede usar para conectarse sin un origen de datos. Por ejemplo, una aplicación que está diseñada para realizar una conexión de "Sin DSN" a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede llamar a **SQLDriverConnect** con una cadena de conexión que define el Id. de inicio de sesión, contraseña, biblioteca de red, nombre del servidor para Conéctese a, y la base de datos predeterminada para usar.  
  
 Cuando se usa **SQLDriverConnect**, hay dos opciones para solicitar al usuario la información de conexión necesaria:  
  
-   Cuadro de diálogo de la aplicación  
  
     Puede crear un cuadro de diálogo de la aplicación que solicita información de conexión y, a continuación, llama a **SQLDriverConnect** con un identificador de ventana NULL y *DriverCompletion* establecido en SQL_DRIVER_NOPROMPT. Estos valores de parámetro evitan que el controlador ODBC abra su propio cuadro de diálogo. Se utiliza este método cuando es importante controlar la interfaz de usuario de la aplicación.  
  
-   Cuadro de diálogo del controlador  
  
     Puede codificar la aplicación para pasar un identificador de ventana válido **SQLDriverConnect** y establezca el *DriverCompletion* parámetro SQL_DRIVER_COMPLETE, SQL_DRIVER_PROMPT o SQL_DRIVER_COMPLETE_ Obligatorio. El controlador genera después un cuadro de diálogo para solicitar al usuario la información de conexión. Este método simplifica el código de aplicación.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**, como **SQLDriverConnect**, usa una cadena de conexión. Sin embargo, mediante el uso de **SQLBrowseConnect**, una aplicación puede construir una cadena de conexión completa de forma iterativa con el origen de datos en tiempo de ejecución. Esto permite a la aplicación hacer dos cosas:  
  
-   Construir sus propios cuadros de diálogo para solicitar esta información, reteniendo así el control sobre la interfaz de usuario.  
  
-   Buscar en el sistema los orígenes de datos que un controlador determinado puede utilizar, posiblemente en varios pasos.  
  
     Por ejemplo, el usuario podría buscar primero en la red los servidores y, después de elegir un servidor, buscar en el servidor las bases de datos accesibles para el controlador.  
  
 Cuando **SQLBrowseConnect** se completa una conexión correcta, devuelve una cadena de conexión que se puede usar en las llamadas subsiguientes a **SQLDriverConnect**.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client siempre devuelve SQL_SUCCESS_WITH_INFO en una correcta **SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**. Cuando una aplicación ODBC llama **SQLGetDiagRec** después de obtener SQL_SUCCESS_WITH_INFO, lo puede recibir los mensajes siguientes:  
  
 5701  
 Indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pone el contexto del usuario en la base de datos predeterminada definida en el origen de datos, o en la base de datos predeterminada definida para el identificador de inicio de sesión utilizado en la conexión si el origen de datos no tenía una base de datos predeterminada.  
  
 5703  
 Indica el lenguaje utilizado en el servidor.  
  
 En el ejemplo siguiente se muestra el mensaje devuelto por el administrador del sistema al realizarse una conexión correctamente:  
  
```  
szSqlState = "01000", *pfNativeError = 5701,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed database context to 'pubs'."  
szSqlState = "01000", *pfNativeError = 5703,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed language setting to 'us_english'."  
```  
  
 Puede omitir los mensajes 5701 y 5703; solo son informativos. No debe, sin embargo, omitir un código de retorno SQL_SUCCESS_WITH_INFO porque se pueden devolver mensajes distintos de 5701 ó 5703. Por ejemplo, si un controlador se conecta a un servidor que ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con los procedimientos almacenados de catálogo anticuados, uno de los errores devueltos a través de **SQLGetDiagRec** después de SQL_SUCCESS_WITH_INFO es:  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 La función de una aplicación para los errores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben llamar las conexiones **SQLGetDiagRec** hasta que devuelva SQL_NO_DATA. A continuación, debe actuar sobre los mensajes que no contengan un *pfNative* código de 5701 ó 5703.  
  
## <a name="see-also"></a>Vea también  
 [Comunicar con SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
