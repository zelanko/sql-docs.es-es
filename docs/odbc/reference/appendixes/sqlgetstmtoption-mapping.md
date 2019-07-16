---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2973455ff4ee7e8dc51b2cd07a6423c9b1c36346
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073810"
---
# <a name="sqlgetstmtoption-mapping"></a>Asignación de SQLGetStmtOption
Cuando una aplicación llama **SQLGetStmtOption** a un ODBC *3.x* controlador que no lo admite, la llamada a  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 se producirá como sigue:  
  
-   Si *fOption* indica una opción de instrucción definida por ODBC que devuelve una cadena, las llamadas del Administrador de controladores  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definida por ODBC que devuelve un valor entero de 32 bits, las llamadas del Administrador de controladores  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definidos por el controlador, el Administrador de controladores de llamadas  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 En los tres casos anteriores, el *StatementHandle* argumento está establecido en el valor de *hstmt*, *atributo* argumento está establecido en el valor de *fOption* y el *ValuePtr* argumento está establecido en el mismo valor que *pvParam*.  
  
 Para las opciones de conexión de cadena definida por ODBC, el Administrador de controladores establece el *BufferLength* argumento en la llamada a **SQLGetConnectAttr** a la longitud máxima predefinida (SQL_MAX_OPTION_STRING_LENGTH); para una opción de conexión que no son cadenas, *BufferLength* se establece en 0.  
  
 La opción de instrucción SQL_GET_BOOKMARK ha quedado obsoleto en ODBC *3.x*. Para un ODBC *3.x* para trabajar con ODBC *2.x* las aplicaciones que usan SQL_GET_BOOKMARK, debe admitir SQL_GET_BOOKMARK. Para un ODBC *3.x* para trabajar con ODBC *2.x* aplicaciones, debe admitir establecer SQL_USE_BOOKMARKS en SQL_UB_ON y debe exponer los marcadores de longitud fija. Si un ODBC *3.x* controlador admite solamente los marcadores de longitud variable, marcadores de longitud no se ha corregido, debe devolver HYC00 SQLSTATE (característica opcional no implementada) si un ODBC *2.x* aplicación intenta Establezca SQL_USE_BOOKMARKS en SQL_UB_ON.  
  
 Para un ODBC *3.x* controlador, el Administrador de controladores ya no se comprueba para ver si *opción* es entre SQL_STMT_OPT_MIN y SQL_STMT_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START. El controlador debe comprobarlo.
