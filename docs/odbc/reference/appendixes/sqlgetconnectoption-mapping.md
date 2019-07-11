---
title: Asignación de SQLGetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ccfebb99d6f98f1c6c2e5eea4650e1433e536d97
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792451"
---
# <a name="sqlgetconnectoption-mapping"></a>Asignación de SQLGetConnectOption
Cuando una aplicación llama **SQLGetConnectOption** a través de un ODBC *3.x* controlador, la llamada a  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 se asigna como sigue:  
  
-   Si *fOption* indica una opción de conexión definida por ODBC que devuelve una cadena, las llamadas del Administrador de controladores  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Si *fOption* indica una opción de conexión definida por ODBC que devuelve un valor entero de 32 bits, las llamadas del Administrador de controladores  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definidos por el controlador, el Administrador de controladores de llamadas  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 En los tres casos anteriores, el *ConnectionHandle* argumento está establecido en el valor de *hdbc*, *atributo* argumento está establecido en el valor de *fOption* y el *ValuePtr* argumento está establecido en el mismo valor que *pvParam*.  
  
 Para las opciones de conexión de cadena definida por ODBC, el Administrador de controladores establece el *BufferLength* argumento en la llamada a **SQLGetConnectAttr** a la longitud máxima predefinida (SQL_MAX_OPTION_STRING_LENGTH); para una opción de conexión que no son cadenas, *BufferLength* se establece en 0.  
  
 Para un ODBC *3.x* controlador, el Administrador de controladores ya no comprueba si *opción* es entre SQL_CONN_OPT_MIN y SQL_CONN_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START. El controlador debe comprobar la validez de los valores de opción.
