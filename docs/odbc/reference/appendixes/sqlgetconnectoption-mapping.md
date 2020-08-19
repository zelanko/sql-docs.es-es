---
description: Asignación de SQLGetConnectOption
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbb8578b881e8eb04ef3b699fa7030e4670fab4d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421479"
---
# <a name="sqlgetconnectoption-mapping"></a>Asignación de SQLGetConnectOption
Cuando una aplicación llama a **SQLGetConnectOption** a través de un controlador ODBC *3. x* , la llamada a  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 se asigna de la siguiente manera:  
  
-   Si *fOption* indica una opción de conexión definida por ODBC que devuelve una cadena, el administrador de controladores llama a  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Si *fOption* indica una opción de conexión definida por ODBC que devuelve un valor entero de 32 bits, el administrador de controladores llama a  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definida por el controlador, el administrador de controladores llama a  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 En los tres casos anteriores, el argumento *ConnectionHandle* se establece en el valor de *hdbc*, el argumento del *atributo* se establece en el valor de *fOption*y el argumento *ValuePtr* se establece en el mismo valor que *pvParam*.  
  
 En el caso de las opciones de conexión de cadenas definidas por ODBC, el administrador de controladores establece el argumento *BufferLength* en la llamada a **SQLGetConnectAttr** en la longitud máxima predefinida (SQL_MAX_OPTION_STRING_LENGTH); en el caso de una opción de conexión que no sea de cadena, *BufferLength* se establece en 0.  
  
 Para un controlador ODBC *3. x* , el administrador de controladores ya no comprueba si la *opción* está entre SQL_CONN_OPT_MIN y SQL_CONN_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START. El controlador debe comprobar la validez de los valores de opción.
