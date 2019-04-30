---
title: SQLSetScrollOptions Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5520554b509b0c25d62e4a191e16ad3524a02652
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297458"
---
# <a name="sqlsetscrolloptions-mapping"></a>Asignación de SQLSetScrollOptions
Cuando una aplicación llama **SQLSetScrollOptions** a través de una aplicación ODBC 3 *.x* controlador y el controlador no admite **SQLSetScrollOptions**, la llamada a  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 se producirá como sigue:  
  
-   Una llamada a  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     con el *InfoType* argumento establecido en uno de los valores en la tabla siguiente, dependiendo del valor de la *KeysetSize* argumento en **SQLSetScrollOptions**.  
  
    |*Argumento KeysetSize*|*Argumento de tipo de información*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Un valor mayor que el *RowsetSize* argumento|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Si el valor de la *KeysetSize* argumento no aparece en la tabla anterior, la llamada a **SQLSetScrollOptions** devuelve SQLSTATE S1107 (valor fuera del intervalo de filas) y ninguno de los pasos siguientes puede realizar.  
  
     El Administrador de controladores, a continuación, comprueba si el bit correspondiente está establecido el **InfoValuePtr* valor devuelto por la llamada a **SQLGetInfo**, según el valor de la *desimultaneidad* argumento en **SQLSetScrollOptions**.  
  
    |*Simultaneidad* argumento|*InfoType* configuración|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Si el *simultaneidad* argumento no es uno de los valores en la tabla anterior, la llamada a **SQLSetScrollOptions** devuelve SQLSTATE S1108 (opción de simultaneidad fuera del intervalo) y ninguno de los pasos siguientes puede realizar. Si el bit correspondiente (como se indica en la tabla anterior) no está establecido **InfoValuePtr* a uno de los valores correspondientes a la *simultaneidad* argumento, la llamada a  **SQLSetScrollOptions** devuelve SQLSTATE S1C00 (no compatible con el controlador) y ninguno de los siguientes pasos se llevan a cabo.  
  
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
    >  Cuando se asigna el Administrador de controladores **SQLSetScrollOptions** para una aplicación que funciona con una aplicación ODBC 3 *.x* controlador que no es compatible con **SQLSetScrollOptions**, el controlador El administrador establece la opción de instrucción SQL_ROWSET_SIZE, no el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE, a la *RowsetSize* argumento en **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** no se puede usar una aplicación al recuperar varias filas mediante una llamada a **SQLFetch** o **SQLFetchScroll**. Puede usarse solo cuando al capturar varias filas mediante una llamada a **SQLExtendedFetch**.
