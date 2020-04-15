---
title: Lo que hace el conductor Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0438478f5aa625ffdd4d3bcd1c0a6f0f80d3367
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301396"
---
# <a name="what-the-driver-does"></a>Lo que hace el controlador
En la tabla siguiente se resume qué funciones y atributos de instrucción debe implementar un controlador ODBC *3.x* para cursores de bloque y desplazables.  
  
|Función o<br /><br /> atributo de instrucción|Comentarios|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Establece la dirección de la matriz de estado de fila rellenada por **SQLFetch** y **SQLFetchScroll**. **SQLSetPos** también rellena esta matriz si se llama a **SQLSetPos** en el estado de instrucción S6. Si **SQLSetPos** se llama en el estado S7, esta matriz no se rellena, pero se rellena la matriz señalada por el *RowStatusArray* argumento de **SQLExtendedFetch.** Para obtener más información, vea Transiciones de [instrucción](../../../odbc/reference/appendixes/statement-transitions.md) en el Apéndice B: Tablas de transición de estado ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Establece la dirección del búfer en el que **SQLFetch** y **SQLFetchScroll** devuelven el número de filas recuperadas. Si se llama a **SQLExtendedFetch,** este búfer no se rellena, pero el *RowCountPtr* argumento apunta al número de filas recuperadas.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Establece el tamaño del conjunto de filas utilizado por **SQLFetch** y **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE|Establece el tamaño del conjunto de filas utilizado por **SQLExtendedFetch**. Los controladores ODBC *3.x* implementan esto si desean trabajar con aplicaciones ODBC *2.x* que llaman a **SQLExtendedFetch** o **SQLSetPos**.|  
|**SQLBulkOperations**|Si un controlador ODBC *3.x* debe trabajar con aplicaciones ODBC *2.x* que usan **SQLSetPos** con una *operación* de SQL_ADD, el controlador debe admitir **SQLSetPos** con una *operación* de SQL_ADD además de **SQLBulkOperations** con una *operación* de SQL_ADD.|  
|**SQLExtendedFetch**|Devuelve el conjunto de filas especificado. Los controladores ODBC *3.x* implementan esto si desean trabajar con aplicaciones ODBC *2.x* que llaman a **SQLExtendedFetch** o **SQLSetPos**. Los siguientes son detalles de implementación:<br /><br /> - El controlador recupera el tamaño del conjunto de filas del valor del atributo de instrucción SQL_ROWSET_SIZE.<br />- El controlador recupera la dirección de la matriz de estado de fila del argumento *RowStatusArray,* no del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. El *RowStatusArray* argumento en una llamada a **SQLExtendedFetch** no debe ser un puntero nulo. (Tenga en cuenta que en ODBC *3.x*, el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR puede ser un puntero nulo.)<br />- El controlador recupera la dirección del búfer de filas recuperadas de la *RowCountPtr* argumento, no el SQL_ATTR_ROWS_FETCHED_PTR atributo de instrucción.<br />- El controlador devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras las filas se recuperaban mediante una llamada a **SQLExtendedFetch**. Un controlador ODBC *3.x* debe devolver SQLSTATE 01S01 (Error en fila) solo cuando se llama a **SQLExtendedFetch,** no cuando **sqlFetch** o **SQLFetchScroll** se llama. Para conservar la compatibilidad con versiones anteriores, cuando **SQLExtendedFetch**devuelve SQLSTATE 01S01 (Error en fila), el Administrador de controladores no ordena registros de estado en la cola de errores según las reglas indicadas en la sección "Secuencia de registros de estado" de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Devuelve el siguiente conjunto de filas. Los siguientes son detalles de implementación:<br /><br /> - El controlador recupera el tamaño del conjunto de filas del valor del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.<br />- El controlador recupera la dirección de la matriz de estado de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />- El controlador recupera la dirección del búfer de filas recuperadas del atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.<br />- La aplicación puede mezclar llamadas entre **SQLFetchScroll** y **SQLFetch**.<br />-   **SQLFetch** devuelve marcadores si la columna 0 está enlazada.<br />-   **SQLFetch** se puede llamar para devolver más de una fila.<br />- El controlador no devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras las filas se recuperaban mediante una llamada a **SQLFetch**.|  
|**SQLFetchScroll**|Devuelve el conjunto de filas especificado. Los siguientes son detalles de implementación:<br /><br /> - El controlador recupera el tamaño del conjunto de filas del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.<br />- El controlador recupera la dirección de la matriz de estado de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />- El controlador recupera la dirección del búfer de filas recuperadas del atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.<br />- La aplicación puede mezclar llamadas entre **SQLFetchScroll** y **SQLFetch**.<br />- El controlador no devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras las filas se recuperaban mediante una llamada a **SQLFetchScroll**.|  
|**SQLSetPos**|Realiza varias operaciones posicionadas. Los siguientes son detalles de implementación:<br /><br /> - Esto se puede llamar en los estados de declaración S6 o S7. Para obtener más información, consulte [Transiciones](../../../odbc/reference/appendixes/statement-transitions.md) de instrucciones en el Apéndice B: Tablas de transición de estado ODBC.<br />- Si se llama a esto en el estado de instrucción S5 o S6, el controlador recupera el tamaño del conjunto de filas del atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR y la dirección de la matriz de estado de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />- Si se llama a esto en el estado de instrucción S7, el controlador recupera el tamaño del conjunto de filas del atributo de instrucción SQL_ROWSET_SIZE y la dirección de la matriz de estado de fila del argumento *RowStatusArray* de **SQLExtendedFetch**.<br />- El controlador devuelve SQLSTATE 01S01 (Error en fila) sólo para indicar que se ha producido un error mientras las filas se recuperaban mediante una llamada a **SQLSetPos** para realizar una operación masiva cuando se llama a la función en el estado S7. Para conservar la compatibilidad con versiones anteriores, si **SQLSetPos**devuelve SQLSTATE 01S01 (Error en fila), el Administrador de controladores no ordena registros de estado en la cola de errores según las reglas indicadas en la sección "Secuencia de registros de estado" de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />- Si el controlador debe trabajar con aplicaciones ODBC *2.x* que llaman a **SQLSetPos** con un *Operación* argumento de SQL_ADD, el controlador debe admitir **SQLSetPos** con un *Operación* argumento de SQL_ADD.|
