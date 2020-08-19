---
description: Asignación de SQLGetStmtOption
title: Asignación de SQLGetStmtOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01d099c4802c05f8e5bd1e093987f2c3993ac9c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448985"
---
# <a name="sqlgetstmtoption-mapping"></a>Asignación de SQLGetStmtOption
Cuando una aplicación llama a **SQLGetStmtOption** a un controlador ODBC *3. x* que no lo admite, la llamada a  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 el resultado será el siguiente:  
  
-   Si *fOption* indica una opción de instrucción definida por ODBC que devuelve una cadena, el administrador de controladores llama a  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definida por ODBC que devuelve un valor entero de 32 bits, el administrador de controladores llama a  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definida por el controlador, el administrador de controladores llama a  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 En los tres casos anteriores, el argumento *StatementHandle* se establece en el valor de *hstmt*, el argumento del *atributo* se establece en el valor de *fOption*y el argumento *ValuePtr* se establece en el mismo valor que *pvParam*.  
  
 En el caso de las opciones de conexión de cadenas definidas por ODBC, el administrador de controladores establece el argumento *BufferLength* en la llamada a **SQLGetConnectAttr** en la longitud máxima predefinida (SQL_MAX_OPTION_STRING_LENGTH); en el caso de una opción de conexión que no sea de cadena, *BufferLength* se establece en 0.  
  
 La opción de instrucción SQL_GET_BOOKMARK está en desuso en ODBC *3. x*. Para que un controlador ODBC *3. x* funcione con aplicaciones ODBC *2. x* que utilicen SQL_GET_BOOKMARK, debe ser compatible con SQL_GET_BOOKMARK. Para que un controlador ODBC *3. x* funcione con aplicaciones ODBC *2. x* , debe admitir la configuración de SQL_USE_BOOKMARKS en SQL_UB_ON y debe exponer marcadores de longitud fija. Si un controlador ODBC *3. x* solo admite marcadores de longitud variable, no marcadores de longitud fija, debe devolver SQLSTATE HYC00 (característica opcional no implementada) si una aplicación ODBC *2. x* intenta establecer SQL_USE_BOOKMARKS en SQL_UB_ON.  
  
 Para un controlador ODBC *3. x* , el administrador de controladores ya no comprueba si la *opción* está entre SQL_STMT_OPT_MIN y SQL_STMT_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START. El controlador debe comprobarlo.
