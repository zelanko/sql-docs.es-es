---
title: Asignación de SQLGetStmtOption ? Microsoft Docs
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
ms.openlocfilehash: 68819269d41407f2ce9dee172c889f7d7f286793
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300605"
---
# <a name="sqlgetstmtoption-mapping"></a>Asignación de SQLGetStmtOption
Cuando una aplicación llama a **SQLGetStmtOption** a un controlador ODBC *3.x* que no lo admite, la llamada a  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 resultará de la siguiente manera:  
  
-   Si *fOption* indica una opción de instrucción definida por ODBC que devuelve una cadena, el Administrador de controladores llama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definida por ODBC que devuelve un valor entero de 32 bits, el Administrador de controladores llama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definida por el controlador, el Administrador de controladores llama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 En los tres casos anteriores, el argumento *StatementHandle* se establece en el valor *de hstmt*, el argumento *Attribute* se establece en el valor de *fOption*y el argumento *ValuePtr* se establece en el mismo valor que *pvParam*.  
  
 Para las opciones de conexión de cadena definida por ODBC, el Administrador de controladores establece el *BufferLength* argumento en la llamada a **SQLGetConnectAttr** a la longitud máxima predefinida (SQL_MAX_OPTION_STRING_LENGTH); para una opción de conexión sin cadena, *BufferLength* se establece en 0.  
  
 La opción de instrucción SQL_GET_BOOKMARK ha quedado en desuso en ODBC *3.x*. Para que un controlador ODBC *3.x* funcione con aplicaciones ODBC *2.x* que usan SQL_GET_BOOKMARK, debe admitir SQL_GET_BOOKMARK. Para que un controlador ODBC *3.x* funcione con aplicaciones ODBC *2.x,* debe admitir la configuración SQL_USE_BOOKMARKS en SQL_UB_ON y debe exponer marcadores de longitud fija. Si un controlador ODBC *3.x* solo admite marcadores de longitud variable, no marcadores de longitud fija, debe devolver SQLSTATE HYC00 (característica opcional no implementada) si una aplicación ODBC *2.x* intenta establecer SQL_USE_BOOKMARKS en SQL_UB_ON.  
  
 Para un controlador ODBC *3.x,* el Administrador de controladores ya no comprueba si *Option* está entre SQL_STMT_OPT_MIN y SQL_STMT_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START. El conductor debe comprobar esto.
