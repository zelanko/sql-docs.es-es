---
title: "Asignación de SQLSetConnectOption | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55ccf421e9db76c570608b4bfc380e0c48dc1f2d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetconnectoption-mapping"></a>Asignación de SQLSetConnectOption
Cuando un ODBC 2. *x* aplicación llama **SQLSetConnectOption** a través de una aplicación ODBC 3*.x* controlador, la llamada a  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 dará como resultado como sigue:  
  
-   Si *fOption* indica un atributo de conexión definida por ODBC que requiere una cadena, las llamadas de administrador de controladores  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Si *fOption* indica un atributo de conexión definida por ODBC que devuelve un valor entero de 32 bits, las llamadas de administrador de controladores  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Si *fOption* indica un atributo de conexión definidos por el controlador, el Administrador de controladores de llamadas  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 En los tres casos anteriores, el *IdentificadorConexión* argumento tiene asignado el valor de *hdbc*, *atributo* argumento tiene asignado el valor de *fOption* y el *ValuePtr* argumento tiene asignado el mismo valor que *vParam*.  
  
 Dado que el Administrador de controladores no sabe si el atributo de conexión definidos por el controlador necesita una cadena o un valor entero de 32 bits, debe pasar un valor válido para el *BufferLength* argumento de **SQLSetConnectAttr**. Si el controlador ha definido una semántica especial para definidos por el controlador conectar atributos y debe llamarse mediante **SQLSetConnectOption**, debe admitir **SQLSetConnectOption**.  
  
 Si está un ODBC 2. *x* aplicación llama **SQLSetConnectOption** para establecer una opción de instrucción específicos del controlador en una aplicación ODBC 3*.x* controlador y la opción se ha definido en una API ODBC 2. *x* versión del controlador, una nueva constante de manifiesto debe definirse de la opción de ODBC 3*.x* controlador. Si la constante de manifiesto anterior se utiliza en la llamada a **SQLSetConnectOption**, el Administrador de controladores llamará **SQLSetConnectAttr** con el **StringLength** establecido en 0.  
  
 Para una aplicación ODBC 3*.x* controlador, el Administrador de controladores ya no se comprueba para ver si *fOption* es entre SQL_CONN_OPT_MIN y SQL_CONN_OPT_MAX o es mayor que SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Establecer opciones de instrucción en el nivel de conexión  
 En ODBC 2. *x*, una aplicación puede llamar a **SQLSetConnectOption** para establecer una opción de instrucción. Cuando sucede esto, el controlador establece la opción de instrucción como valor predeterminado para cualquier instrucción posterior asignado para esa conexión. Se está definido por controlador si el controlador establece la opción de instrucción para cualquier instrucción existente asociado a la conexión especificada.  
  
 Esta capacidad está en desuso en ODBC 3*.x*. ODBC 3*.x* controladores sólo necesitan admitir configuración ODBC 2. *x* atributos de instrucción en el nivel de conexión si desean trabajar con ODBC 2. *x* las aplicaciones que hacen esto. ODBC 3*.x* aplicaciones nunca deben establecer los atributos de instrucción en el nivel de conexión. ODBC 3*.x* atributos de instrucción no se puede establecer en el nivel de conexión, a excepción de los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son atributos de conexión y los atributos de instrucción y puede ser Establezca en el nivel de conexión o en el nivel de instrucción.
