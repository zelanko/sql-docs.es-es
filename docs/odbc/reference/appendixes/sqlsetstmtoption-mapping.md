---
title: Asignación de SQLSetStmtOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc4ed430b301f2b191c0586c0a54af19a2d2d526
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091667"
---
# <a name="sqlsetstmtoption-mapping"></a>Asignación de SQLSetStmtOption
Cuando una aplicación llama **SQLSetStmtOption** a través de un ODBC *3.x* controlador, la llamada a  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 se producirá como sigue:  
  
-   Si *fOption* indica un atributo de instrucción definida por ODBC que es una cadena, las llamadas del Administrador de controladores  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Si *fOption* indica un atributo de instrucción definida por ODBC que devuelve un valor entero de 32 bits, las llamadas del Administrador de controladores  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Si *fOption* indica un atributo definido por el controlador de instrucción, el Administrador de controladores de llamadas  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 En los tres casos anteriores, el **StatementHandle** argumento está establecido en el valor de *hstmt*, *atributo* argumento está establecido en el valor de *fOption* y el *ValuePtr* argumento está establecido en el valor como *vParam*.  
  
 Dado que el Administrador de controladores no sabe si el atributo de instrucción definidos por el controlador necesita una cadena o un valor entero de 32 bits, debe pasar un valor válido para el *StringLength* argumento de **SQLSetStmtAttr**. Si el controlador ha definido una semántica especial para los atributos definidos por el controlador de instrucción y debe llamarse usando **SQLSetStmtOption**, debe ser compatible con **SQLSetStmtOption**.  
  
 Si una aplicación llama a **SQLSetStmtOption** para establecer una opción de instrucción específicos del controlador en un ODBC *3.x* controlador y la opción se definió en un ODBC *2.x* versión de la controlador, se debe definir una nueva constante de manifiesto para la opción de ODBC *3.x* controlador. Si se usa la constante de manifiesto anterior en la llamada a **SQLSetStmtOption**, el Administrador de controladores llamará **SQLSetStmtAttr** con el *StringLength* argumento establecido en 0.  
  
 Cuando una aplicación llama **SQLSetStmtAttr** establecer SQL_ATTR_USE_BOOKMARKS en SQL_UB_ON en un ODBC *3.x* controlador, el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se establece en SQL_UB_FIXED. SQL_UB_ON es la misma constante como SQL_UB_FIXED. El Administrador de controladores pasa SQL_UB_FIXED a través del controlador. SQL_UB_FIXED ha quedado obsoleto en ODBC *3.x*, pero un ODBC *3.x* controlador debe implementar para que funcione con ODBC *2.x* las aplicaciones que usan los marcadores de longitud fija.  
  
 Para un ODBC *3.x* controlador, el Administrador de controladores ya no comprueba si *opción* es entre SQL_STMT_OPT_MIN y SQL_STMT_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START.
