---
description: Asignación de SQLSetStmtOption
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f2c4a65ade202003d454988372895ba40fb6eeef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424886"
---
# <a name="sqlsetstmtoption-mapping"></a>Asignación de SQLSetStmtOption
Cuando una aplicación llama a **SQLSetStmtOption** a través de un controlador ODBC *3. x* , la llamada a  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 el resultado será el siguiente:  
  
-   Si *fOption* indica un atributo de instrucción definido por ODBC que es una cadena, el administrador de controladores llama a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Si *fOption* indica un atributo de instrucción definido por ODBC que devuelve un valor entero de 32 bits, el administrador de controladores llama a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Si *fOption* indica un atributo de instrucción definido por el controlador, el administrador de controladores llama a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 En los tres casos anteriores, el argumento **StatementHandle** se establece en el valor de *hstmt*, el argumento del *atributo* se establece en el valor de *fOption*y el argumento *ValuePtr* se establece en el valor como *vParam*.  
  
 Dado que el administrador de controladores no sabe si el atributo de instrucción definido por el controlador necesita una cadena o un valor entero de 32 bits, debe pasar un valor válido para el argumento *StringLength* de **SQLSetStmtAttr**. Si el controlador tiene una semántica especial definida para los atributos de instrucción definidos por el controlador y debe llamarse mediante **SQLSetStmtOption**, debe admitir **SQLSetStmtOption**.  
  
 Si una aplicación llama a **SQLSetStmtOption** para establecer una opción de instrucción específica del controlador en un controlador ODBC *3. x* y la opción se definió en una versión ODBC *2. x* del controlador, se debe definir una nueva constante de manifiesto para la opción en el controlador ODBC *3. x* . Si se usa la constante de manifiesto antigua en la llamada a **SQLSetStmtOption**, el administrador de controladores llamará a **SQLSetStmtAttr** con el argumento *StringLength* establecido en 0.  
  
 Cuando una aplicación llama a **SQLSetStmtAttr** para establecer SQL_ATTR_USE_BOOKMARKS en SQL_UB_ON en un controlador ODBC *3. x* , el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se establece en SQL_UB_FIXED. SQL_UB_ON es la misma constante que SQL_UB_FIXED. El administrador de controladores pasa SQL_UB_FIXED a través del controlador. SQL_UB_FIXED ha quedado en desuso en ODBC *3. x*, pero un controlador ODBC *3. x* debe implementarlo para que funcione con aplicaciones ODBC *2. x* que usan marcadores de longitud fija.  
  
 Para un controlador ODBC *3. x* , el administrador de controladores ya no comprueba si la *opción* está entre SQL_STMT_OPT_MIN y SQL_STMT_OPT_MAX, o es mayor que SQL_CONNECT_OPT_DRVR_START.
