---
title: Asignación de SQLSetConnectOption ( SQLSetConnectOption Mapping) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 757b50c7e18133e02b4cf6addaa327b2053f5439
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287475"
---
# <a name="sqlsetconnectoption-mapping"></a>Asignación de SQLSetConnectOption
Cuando un ODBC 2. *x* aplicación llama a **SQLSetConnectOption** a través de un controlador ODBC 3 *.x,* la llamada a  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 resultará de la siguiente manera:  
  
-   Si *fOption* indica un atributo de conexión definido por ODBC que requiere una cadena, el Administrador de controladores llama  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Si *fOption* indica un atributo de conexión definido por ODBC que devuelve un valor entero de 32 bits, el Administrador de controladores llama  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Si *fOption* indica un atributo de conexión definido por el controlador, el Administrador de controladores llama  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 En los tres casos anteriores, el *connectionHandle* argumento se establece en el valor en *hdbc*, el *Attribute* argumento se establece en el valor en *fOption*y el *ValuePtr* argumento se establece en el mismo valor que *vParam*.  
  
 Dado que el Administrador de controladores no sabe si el atributo de conexión definido por el controlador necesita una cadena o un valor entero de 32 bits, tiene que pasar un valor válido para el argumento *BufferLength* de **SQLSetConnectAttr**. Si el controlador ha definido una semántica especial para los atributos de conexión definidos por el controlador y se debe llamar mediante **SQLSetConnectOption**, debe admitir **SQLSetConnectOption**.  
  
 Si un ODBC 2. *x* aplicación llama a **SQLSetConnectOption** para establecer una opción de instrucción específica del controlador en un controlador ODBC 3 *.x* y la opción se definió en un ODBC 2. *x* versión del controlador, se debe definir una nueva constante de manifiesto para la opción en el controlador ODBC 3 *.x.* Si se utiliza la constante de manifiesto anterior en la llamada a **SQLSetConnectOption**, el Administrador de controladores llamará a **SQLSetConnectAttr** con el **StringLength** argumento establecido en 0.  
  
 Para un controlador ODBC 3 *.x,* el Administrador de controladores ya no comprueba si *fOption* está entre SQL_CONN_OPT_MIN y SQL_CONN_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Configuración de las opciones de instrucción en el nivel de conexión  
 En ODBC 2. *x*, una aplicación podría llamar a **SQLSetConnectOption** para establecer una opción de instrucción. Cuando se hace esto, el controlador establece la opción de instrucción como valor predeterminado para las instrucciones asignadas más adelante para esa conexión. Está definido por el controlador si el controlador establece la opción de instrucción para las instrucciones existentes asociadas con la conexión especificada.  
  
 Esta capacidad ha quedado en desuso en ODBC 3 *.x*. Los controladores ODBC 3 *.x* solo necesitan admitir la configuración de ODBC 2. *x* atributos de instrucción en el nivel de conexión si quieren trabajar con ODBC 2. *x* aplicaciones que hacen esto. Las aplicaciones ODBC 3 *.x* nunca deben establecer atributos de instrucción en el nivel de conexión. Los atributos de instrucción *.x* de ODBC 3 no se pueden establecer en el nivel de conexión, con la excepción de los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son atributos de conexión y atributos de instrucción, y se pueden establecer en el nivel de conexión o en el nivel de instrucción.
