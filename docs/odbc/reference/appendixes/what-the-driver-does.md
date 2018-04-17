---
title: Lo que hace el controlador | Documentos de Microsoft
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
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 312fbf529a9173b05c926cc1315740a2e8532bbd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="what-the-driver-does"></a>Lo que hace el controlador
En la tabla siguiente se resume las funciones y los atributos de instrucción una aplicación ODBC 3*.x* controlador debe implementar para bloqueo y los cursores desplazables.  
  
|Función o<br /><br /> atributo de instrucción|Comentarios|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Establece la dirección de la matriz de Estados de fila se rellena por **SQLFetch** y **SQLFetchScroll**. Esta matriz también se rellena por **SQLSetPos** si **SQLSetPos** se llama en el estado de instrucción S6. Si **SQLSetPos** se llama en estado S7, no se rellena esta matriz, pero la matriz señalada por el *RowStatusArray* argumento de **SQLExtendedFetch** se rellena. Para obtener más información, consulte [instrucción transiciones](../../../odbc/reference/appendixes/statement-transitions.md) en tablas de transición de estado de apéndice B: ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Establece la dirección del búfer en el que **SQLFetch** y **SQLFetchScroll** devuelve el número de filas recuperadas. Si **SQLExtendedFetch** es llama, este búfer no se ha rellenado, pero la *RowCountPtr* argumento señala el número de filas recuperadas.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Establece el tamaño del conjunto de filas usado por **SQLFetch** y **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE|Establece el tamaño del conjunto de filas usado por **SQLExtendedFetch**. ODBC 3*.x* controladores hacerlo si desean trabajar con ODBC 2. *x* aplicaciones que llaman a **SQLExtendedFetch** o **SQLSetPos**.|  
|**SQLBulkOperations**|Si una aplicación ODBC 3*.x* controlador debería trabajar con ODBC 2. *x* las aplicaciones que utilizan **SQLSetPos** con una *operación* de SQL_ADD, el controlador debe admitir **SQLSetPos** con un  *Operación* de SQL_ADD además **SQLBulkOperations** con una *operación* de SQL_ADD.|  
|**SQLExtendedFetch**|Devuelve el conjunto de filas especificado. ODBC 3*.x* controladores hacerlo si desean trabajar con ODBC 2. *x* aplicaciones que llaman a **SQLExtendedFetch** o **SQLSetPos**. Éstos son los detalles de implementación:<br /><br /> -El controlador recupera el tamaño de conjunto de filas desde el valor del atributo de instrucción SQL_ROWSET_SIZE.<br />-El controlador recupera la dirección de la matriz de Estados de fila de la *RowStatusArray* argumento, no el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. El *RowStatusArray* argumento en una llamada a **SQLExtendedFetch** no debe ser un puntero nulo. (Tenga en cuenta que en ODBC 3*.x*, el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR puede ser un puntero nulo.)<br />-El controlador recupera la dirección del búfer de filas recuperadas desde la *RowCountPtr* argumento, no el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.<br />-El controlador devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras se capturan filas mediante una llamada a **SQLExtendedFetch**. Una aplicación ODBC 3*.x* controlador debería devolver SQLSTATE 01S01 (Error en la fila) solo cuando **SQLExtendedFetch** se llama, no cuando **SQLFetch** o **SQLFetchScroll** se llama. Para conservar la compatibilidad con versiones anteriores, cuando SQLSTATE 01S01 (Error en la fila) se devuelve por **SQLExtendedFetch**, el Administrador de controladores no ordena los registros de estado en la cola de error según las reglas descritas en la "secuencia de estado Registra"sección de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Devuelve el siguiente conjunto de filas. Éstos son los detalles de implementación:<br /><br /> -El controlador recupera el tamaño de conjunto de filas desde el valor del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.<br />-El controlador recupera la dirección de la matriz de Estados de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />-El controlador recupera la dirección de las filas recuperadas búfer desde el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.<br />-La aplicación puede mezclar llamadas entre **SQLFetchScroll** y **SQLFetch**.<br />-   **SQLFetch** devuelve marcadores si está enlazada la columna 0.<br />-   **SQLFetch** puede llamarse para devolver más de una fila.<br />-El controlador no devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras se capturan filas mediante una llamada a **SQLFetch**.|  
|**SQLFetchScroll**|Devuelve el conjunto de filas especificado. Éstos son los detalles de implementación:<br /><br /> -El controlador recupera el tamaño de conjunto de filas desde el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.<br />-El controlador recupera la dirección de la matriz de Estados de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />-El controlador recupera la dirección de las filas recuperadas búfer desde el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.<br />-La aplicación puede mezclar llamadas entre **SQLFetchScroll** y **SQLFetch**.<br />-El controlador no devuelve SQLSTATE 01S01 (Error en la fila) para indicar que se ha producido un error mientras se capturan filas mediante una llamada a **SQLFetchScroll**.|  
|**SQLSetPos**|Lleva a cabo diversas operaciones por posición. Éstos son los detalles de implementación:<br /><br /> -Se puede llamar en Estados de instrucción S6 o S7. Para obtener más información, consulte [instrucción transiciones](../../../odbc/reference/appendixes/statement-transitions.md) en tablas de transición de estado de apéndice B: ODBC.<br />-Si esto se llama en un estado de instrucción S5 o S6, el controlador recupera el tamaño de conjunto de filas desde el atributo de instrucción de SQL_ATTR_ROWS_FETCHED_PTR y la dirección de la matriz de Estados de fila del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.<br />-Si esto se denomina en estado de instrucción S7, el controlador recupera el tamaño de conjunto de filas desde el atributo de instrucción de SQL_ROWSET_SIZE y la dirección de la matriz de Estados de fila de la *RowStatusArray* argumento de  **SQLExtendedFetch**.<br />-El controlador devuelve SQLSTATE 01S01 (Error en la fila) solo para indicar que se ha producido un error mientras se capturan filas mediante una llamada a **SQLSetPos** para realizar una operación masiva cuando se llama a la función en estado S7. Para conservar la compatibilidad con versiones anteriores, si SQLSTATE 01S01 (Error en la fila) se devuelve por **SQLSetPos**, el Administrador de controladores no ordena los registros de estado en la cola de error según las reglas descritas en la "secuencia de registros de estado" sección de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />-Si el controlador debe trabajar con ODBC 2. *x* aplicaciones que llaman a **SQLSetPos** con una *operación* argumento de SQL_ADD, el controlador debe admitir **SQLSetPos** con un  *Operación* argumento de SQL_ADD.|
