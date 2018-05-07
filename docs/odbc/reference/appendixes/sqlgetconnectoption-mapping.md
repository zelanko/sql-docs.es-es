---
title: Asignación de SQLGetConnectOption | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ec36a536732299337efde3cf58cc98fbf4c46e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetconnectoption-mapping"></a>Asignación de SQLGetConnectOption
Cuando una aplicación llama **SQLGetConnectOption** a través de una aplicación ODBC 3 *.x* controlador, la llamada a  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 se asigna como sigue:  
  
-   Si *fOption* indica una opción de conexión definida por ODBC que devuelve una cadena, las llamadas de administrador de controladores  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Si *fOption* indica una opción de conexión definida por ODBC que devuelve un valor entero de 32 bits, las llamadas de administrador de controladores  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definidos por el controlador, el Administrador de controladores de llamadas  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 En los tres casos anteriores, el *IdentificadorConexión* argumento tiene asignado el valor de *hdbc*, *atributo* argumento tiene asignado el valor de *fOption* y el *ValuePtr* argumento tiene asignado el mismo valor que *pvParam*.  
  
 Opciones de conexión de la cadena definida por ODBC, el Administrador de controladores establece la *BufferLength* argumento en la llamada a **SQLGetConnectAttr** a la longitud máxima predefinida (SQL_MAX_OPTION_STRING_LENGTH); para una opción de conexión que no son cadenas, *BufferLength* se establece en 0.  
  
 Para una aplicación ODBC 3 *.x* controlador, el Administrador de controladores ya no se comprueba para ver si *opción* es entre SQL_CONN_OPT_MIN y SQL_CONN_OPT_MAX o es mayor que SQL_CONNECT_OPT_DRVR_START. El controlador debe comprobar la validez de los valores de opción.
