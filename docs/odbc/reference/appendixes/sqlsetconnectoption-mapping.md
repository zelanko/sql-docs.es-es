---
title: Asignación de SQLSetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0351a6fa4621acb09d18a72b32ec2010a605ed9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769573"
---
# <a name="sqlsetconnectoption-mapping"></a>Asignación de SQLSetConnectOption
Cuando un ODBC 2. *x* aplicación llama a **SQLSetConnectOption** a través de una aplicación ODBC 3 *.x* controlador, la llamada a  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 se producirá como sigue:  
  
-   Si *fOption* indica un atributo de conexión definida por ODBC que requiere una cadena, las llamadas del Administrador de controladores  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Si *fOption* indica un atributo de conexión definida por ODBC que devuelve un valor entero de 32 bits, las llamadas del Administrador de controladores  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Si *fOption* indica un atributo de conexión definidos por el controlador, el Administrador de controladores de llamadas  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 En los tres casos anteriores, el *ConnectionHandle* argumento está establecido en el valor de *hdbc*, *atributo* argumento está establecido en el valor de *fOption* y el *ValuePtr* argumento está establecido en el mismo valor que *vParam*.  
  
 Dado que el Administrador de controladores no sabe si el atributo de conexión definidos por el controlador necesita una cadena o un valor entero de 32 bits, debe pasar un valor válido para el *BufferLength* argumento de **SQLSetConnectAttr**. Si el controlador ha definido una semántica especial para definidos por el controlador conectar atributos y debe llamarse usando **SQLSetConnectOption**, debe ser compatible con **SQLSetConnectOption**.  
  
 Si está un ODBC 2. *x* aplicación llama a **SQLSetConnectOption** para establecer una opción de instrucción específicos del controlador en una aplicación ODBC 3 *.x* controlador y la opción se definió en un ODBC 2. *x* versión del controlador, una nueva constante de manifiesto debe definirse para la opción en ODBC 3 *.x* controlador. Si se usa la constante de manifiesto anterior en la llamada a **SQLSetConnectOption**, el Administrador de controladores llamará **SQLSetConnectAttr** con el **StringLength** argumento establecido en 0.  
  
 Para una aplicación ODBC 3 *.x* controlador, el Administrador de controladores ya no comprueba si *fOption* es entre SQL_CONN_OPT_MIN y SQL_CONN_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Establecer opciones de la instrucción en el nivel de conexión  
 En ODBC 2. *x*, una aplicación podría llamar a **SQLSetConnectOption** para establecer una opción de instrucción. Cuando esté listo, el controlador establece la opción de instrucción de forma predeterminada para las instrucciones que asignan más adelante para esa conexión. Se está definido por controlador si el controlador establece la opción de instrucción para las instrucciones existentes asociados con la conexión especificada.  
  
 Esta capacidad está desusada en ODBC 3 *.x*. ODBC 3 *.x* controladores sólo necesitan admitir la configuración de ODBC 2. *x* atributos de instrucción en el nivel de conexión si desean trabajar con ODBC 2. *x* las aplicaciones que hacen esto. ODBC 3 *.x* aplicaciones nunca deben establecer los atributos de instrucción en el nivel de conexión. ODBC 3 *.x* atributos de instrucción no se puede establecer en el nivel de conexión, a excepción de los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son los atributos de conexión y los atributos de instrucción y pueden ser establecer en el nivel de conexión o el nivel de instrucción.
