---
title: Lo que hace el controlador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f27efed55a2ae63b8c3726263077441bdacc49b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135721"
---
# <a name="what-the-driver-does"></a>Lo que hace el controlador
En la tabla siguiente se resume las funciones y atributos de instrucción un ODBC *3.x* controlador debe implementar para los cursores desplazables y de bloque.  
  
|Función o<br /><br /> atributo de instrucción|Comentarios|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Establece la dirección de la matriz de Estados de fila se rellena mediante **SQLFetch** y **SQLFetchScroll**. Esta matriz también se rellena mediante **SQLSetPos** si **SQLSetPos** se llama en el estado de la instrucción S6. Si **SQLSetPos** se llama en el estado S7, no se rellena esta matriz, pero la matriz señalada por el *RowStatusArray* argumento de **SQLExtendedFetch** se rellena. Para obtener más información, consulte [transiciones de instrucción](../../../odbc/reference/appendixes/statement-transitions.md) en el apéndice B: Tablas de transición de estado de ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Establece la dirección del búfer en el que **SQLFetch** y **SQLFetchScroll** devuelve el número de filas recuperadas. Si **SQLExtendedFetch** es llama, este búfer no se ha rellenado, pero la *RowCountPtr* argumento apunta al número de filas recuperadas.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Establece el tamaño del conjunto de filas usando **SQLFetch** y **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE|Establece el tamaño del conjunto de filas usando **SQLExtendedFetch**. ODBC *3.x* controladores implementan esto si desean trabajar con ODBC *2.x* aplicaciones que llaman a **SQLExtendedFetch** o **SQLSetPos**.|  
|**SQLBulkOperations**|Si un ODBC *3.x* controlador debería funcionar con ODBC *2.x* las aplicaciones que usan **SQLSetPos** con un *operación* de SQL_ADD, el controlador debe admitir **SQLSetPos** con un *operación* de SQL_ADD además **SQLBulkOperations** con un *operación* de SQL _AGREGAR.|  
|**SQLExtendedFetch**|Devuelve el conjunto de filas especificado. ODBC *3.x* controladores implementan esto si desean trabajar con ODBC *2.x* aplicaciones que llaman a **SQLExtendedFetch** o **SQLSetPos**. Estos son los detalles de implementación:<br /><br /> -El controlador recupera el tamaño del conjunto de filas desde el valor del atributo de instrucción SQL_ROWSET_SIZE.<br />-El controlador recupera la dirección de la matriz de Estados de fila de la *RowStatusArray* argumento, no el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. El *RowStatusArray* argumento en una llamada a **SQLExtendedFetch** no debe ser un puntero nulo. (Tenga en cuenta que en ODBC *3.x*, el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR puede ser un puntero nulo.)<br />-El controlador recupera la dirección del búfer de filas recuperadas desde la *RowCountPtr* argumento, no el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.<br />-El controlador devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras se capturan las filas mediante una llamada a **SQLExtendedFetch**. Un ODBC *3.x* controlador debería devolver SQLSTATE 01S01 (Error en la fila) solo cuando **SQLExtendedFetch** se llama, no cuando **SQLFetch** o **SQLFetchScroll** se llama. Para mantener la compatibilidad con versiones anteriores, cuando 01S01 SQLSTATE (Error en la fila) devuelto por **SQLExtendedFetch**, el Administrador de controladores no ordena los registros de estado en la cola de errores según las reglas descritas en el "secuencia de estado "Entradas" sección de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Devuelve el siguiente conjunto de filas. Estos son los detalles de implementación:<br /><br /> -El controlador recupera el tamaño del conjunto de filas desde el valor del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.<br />-El controlador recupera la dirección de la matriz de Estados de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />-El controlador recupera la dirección de las filas recuperadas búfer desde el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.<br />-La aplicación puede combinar las llamadas entre **SQLFetchScroll** y **SQLFetch**.<br />-   **SQLFetch** devuelve marcadores si está enlazada la columna 0.<br />-   **SQLFetch** se puede llamar para devolver más de una fila.<br />-El controlador no devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras se capturan las filas mediante una llamada a **SQLFetch**.|  
|**SQLFetchScroll**|Devuelve el conjunto de filas especificado. Estos son los detalles de implementación:<br /><br /> -El controlador recupera el tamaño del conjunto de filas desde el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.<br />-El controlador recupera la dirección de la matriz de Estados de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />-El controlador recupera la dirección de las filas recuperadas búfer desde el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.<br />-La aplicación puede combinar las llamadas entre **SQLFetchScroll** y **SQLFetch**.<br />-El controlador no devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras se capturan las filas mediante una llamada a **SQLFetchScroll**.|  
|**SQLSetPos**|Realiza varias operaciones posicionadas. Estos son los detalles de implementación:<br /><br /> -Se puede llamar en los Estados de instrucción S6 o S7. Para obtener más información, consulte [transiciones de instrucción](../../../odbc/reference/appendixes/statement-transitions.md) en el apéndice B: Tablas de transición de estado de ODBC.<br />-Si se llama estado de la instrucción S5 o S6, el controlador recupera el tamaño del conjunto de filas desde el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR y la dirección de la matriz de Estados de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />-Si se llama estado de la instrucción S7, el controlador recupera el tamaño del conjunto de filas desde el atributo de instrucción SQL_ROWSET_SIZE y la dirección de la matriz de Estados de fila de la *RowStatusArray* argumento de  **SQLExtendedFetch**.<br />-El controlador devuelve SQLSTATE 01S01 (Error en la fila) solo para indicar que se ha producido un error mientras se capturan las filas mediante una llamada a **SQLSetPos** para realizar una operación masiva cuando se llama a la función en estado S7. Para mantener la compatibilidad con versiones anteriores, si SQLSTATE 01S01 (Error en la fila) devuelto por **SQLSetPos**, el Administrador de controladores no ordena los registros de estado en la cola de errores según las reglas descritas en la "secuencia de registros de estado" sección de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />-Si el controlador debería funcionar con ODBC *2.x* aplicaciones que llaman a **SQLSetPos** con un *operación* argumento de SQL_ADD, el controlador debe admitir  **SQLSetPos** con un *operación* argumento de SQL_ADD.|
