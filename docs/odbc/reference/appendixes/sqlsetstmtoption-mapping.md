---
title: "Asignación de SQLSetStmtOption | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3aba3d69d8bbb90b1296bf821b6552d25a05b7b2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetstmtoption-mapping"></a>Asignación de SQLSetStmtOption
Cuando una aplicación llama **SQLSetStmtOption** a través de una aplicación ODBC 3*.x* controlador, la llamada a  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 dará como resultado como sigue:  
  
-   Si *fOption* indica un atributo de instrucción definida por ODBC es una cadena, las llamadas de administrador de controladores  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Si *fOption* indica un atributo de instrucción definida por ODBC que devuelve un valor entero de 32 bits, las llamadas de administrador de controladores  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Si *fOption* indica un atributo de instrucción definidos por el controlador, el Administrador de controladores de llamadas  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 En los tres casos anteriores, el **StatementHandle** argumento tiene asignado el valor de *hstmt*, *atributo* argumento tiene asignado el valor de *fOption* y el *ValuePtr* argumento tiene asignado el valor como *vParam*.  
  
 Dado que el Administrador de controladores no sabe si el atributo de instrucción definidos por el controlador necesita una cadena o un valor entero de 32 bits, debe pasar un valor válido para el *StringLength* argumento de **SQLSetStmtAttr**. Si el controlador que ha definido una semántica especial para los atributos de instrucción definidos por el controlador y debe llamarse mediante **SQLSetStmtOption**, debe admitir **SQLSetStmtOption**.  
  
 Si una aplicación llama **SQLSetStmtOption** para establecer una opción de instrucción específicos del controlador en una aplicación ODBC 3*.x* controlador y la opción se ha definido en una API ODBC 2. *x* versión del controlador, una nueva constante de manifiesto debe definirse de la opción de ODBC 3*.x* controlador. Si la constante de manifiesto anterior se utiliza en la llamada a **SQLSetStmtOption**, el Administrador de controladores llamará **SQLSetStmtAttr** con el *StringLength* establecido en 0.  
  
 Cuando una aplicación llama **SQLSetStmtAttr** para establecer SQL_ATTR_USE_BOOKMARKS en SQL_UB_ON en una aplicación ODBC 3*.x* controlador, se establece el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS en SQL_UB_FIXED. SQL_UB_ON es la misma constante como SQL_UB_FIXED. El Administrador de controladores pasa SQL_UB_FIXED a través del controlador. SQL_UB_FIXED está en desuso en ODBC 3*.x*, pero una aplicación ODBC 3*.x* controlador debe implementar para que funcione con ODBC 2. *x* las aplicaciones que usan los marcadores de longitud fija.  
  
 Para una aplicación ODBC 3*.x* controlador, el Administrador de controladores ya no se comprueba para ver si *opción* es entre SQL_STMT_OPT_MIN y SQL_STMT_OPT_MAX o es mayor que SQL_CONNECT_OPT_DRVR_START.

