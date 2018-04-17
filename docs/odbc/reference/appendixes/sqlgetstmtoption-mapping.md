---
title: Asignación de SQLGetStmtOption | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ce6b64f9151808e8b02f3036638d7322d3012938
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetstmtoption-mapping"></a>Asignación de SQLGetStmtOption
Cuando una aplicación llama **SQLGetStmtOption** a una aplicación ODBC 3*.x* controlador que no lo admite, la llamada a  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 dará como resultado como sigue:  
  
-   Si *fOption* indica una opción de instrucción definida por ODBC que devuelve una cadena, las llamadas de administrador de controladores  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definida por ODBC que devuelve un valor entero de 32 bits, las llamadas de administrador de controladores  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Si *fOption* indica una opción de instrucción definidos por el controlador, el Administrador de controladores de llamadas  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 En los tres casos anteriores, el *StatementHandle* argumento tiene asignado el valor de *hstmt*, *atributo* argumento tiene asignado el valor de *fOption* y el *ValuePtr* argumento tiene asignado el mismo valor que *pvParam*.  
  
 Opciones de conexión de la cadena definida por ODBC, el Administrador de controladores establece la *BufferLength* argumento en la llamada a **SQLGetConnectAttr** a la longitud máxima predefinida (SQL_MAX_OPTION_STRING_LENGTH); para una opción de conexión que no son cadenas, *BufferLength* se establece en 0.  
  
 La opción de instrucción SQL_GET_BOOKMARK está en desuso en ODBC 3*.x*. Para una aplicación ODBC 3*.x* controlador para trabajar con ODBC 2. *x* las aplicaciones que utilizan SQL_GET_BOOKMARK, debe admitir SQL_GET_BOOKMARK. Para una aplicación ODBC 3*.x* controlador para trabajar con ODBC 2. *x* de las aplicaciones, deben admitir establecer SQL_USE_BOOKMARKS en SQL_UB_ON y debe exponer los marcadores de longitud fija. Si una aplicación ODBC 3*.x* controlador admite solamente los marcadores de longitud variable, marcadores de longitud no fija, debe devolver HYC00 SQLSTATE (característica opcional no implementada) si una API ODBC 2. *x* aplicación intenta establecer SQL_USE_BOOKMARKS a SQL_UB_ON.  
  
 Para una aplicación ODBC 3*.x* controlador, el Administrador de controladores ya no se comprueba para ver si *opción* es entre SQL_STMT_OPT_MIN y SQL_STMT_OPT_MAX o es mayor que SQL_CONNECT_OPT_DRVR_START. El controlador debe comprobarlo.
