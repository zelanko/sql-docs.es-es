---
title: Asignación de SQLSetScrollOptions | Documentos de Microsoft
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
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f33f43451d88d69e47f5f647fa2b5e10eb89a9db
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetscrolloptions-mapping"></a>Asignación de SQLSetScrollOptions
Cuando una aplicación llama **SQLSetScrollOptions** a través de una aplicación ODBC 3*.x* controlador y el controlador no admite **SQLSetScrollOptions**, la llamada a  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 dará como resultado como sigue:  
  
-   Una llamada a  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     con el *tipo de información* establecido en uno de los valores en la tabla siguiente, dependiendo del valor de la *KeysetSize* argumento en **SQLSetScrollOptions**.  
  
    |*Argumento de KeysetSize*|*Argumento de tipo de información*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Un valor mayor que el *RowsetSize* argumento|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Si el valor de la *KeysetSize* argumento no aparece en la tabla anterior, la llamada a **SQLSetScrollOptions** devuelve SQLSTATE S1107 (valor fuera del intervalo de filas) y no hay ninguno de los pasos siguientes lleva a cabo.  
  
     El Administrador de controladores, a continuación, comprueba si el bit correspondiente se establece el **InfoValuePtr* valor devuelto por la llamada a **SQLGetInfo**, según el valor de la *simultaneidad* argumento en **SQLSetScrollOptions**.  
  
    |*Simultaneidad* argumento|*Tipo de información* configuración|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Si el *simultaneidad* argumento no es uno de los valores en la tabla anterior, la llamada a **SQLSetScrollOptions** devuelve SQLSTATE S1108 (opción de simultaneidad fuera del intervalo) y no hay ninguno de los pasos siguientes lleva a cabo. Si el bit correspondiente (según se indica en la tabla anterior) no está establecido **InfoValuePtr* a uno de los valores correspondientes a la *simultaneidad* argumento, la llamada a  **SQLSetScrollOptions** devuelve SQLSTATE S1C00 (no compatible con el controlador) y ninguno de los siguientes pasos se llevan a cabo.  
  
-   Una llamada a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     con  *\*ValuePtr* establecido en uno de los valores en la tabla siguiente, según el valor de la *KeysetSize* argumento en **SQLSetScrollOptions**.  
  
    |*KeysetSize* argumento|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |Un valor mayor que el *RowsetSize* argumento|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   Una llamada a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     con  *\*ValuePtr* establecido en el *simultaneidad* argumento en **SQLSetScrollOptions**.  
  
-   Si el *KeysetSize* argumento en la llamada a **SQLSetScrollOptions** es positivo, una llamada a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     con  *\*ValuePtr* establecido en el *KeysetSize* argumento en **SQLSetScrollOptions**.  
  
-   Una llamada a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     con  *\*ValuePtr* establecido en el *RowsetSize* argumento en **SQLSetScrollOptions**.  
  
    > [!NOTE]  
    >  Cuando se asigna el Administrador de controladores **SQLSetScrollOptions** para una aplicación que trabaja con una aplicación ODBC 3*.x* controlador que no es compatible con **SQLSetScrollOptions**, el controlador El administrador establece la opción de instrucción SQL_ROWSET_SIZE, no el atributo de instrucción de SQL_ATTR_ROW_ARRAY_SIZE, para la *RowsetSize* argumento en **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** no se puede usar una aplicación al capturar varias filas mediante una llamada a **SQLFetch** o **SQLFetchScroll**. Se puede utilizar solo cuando se captura varias filas mediante una llamada a **SQLExtendedFetch**.
