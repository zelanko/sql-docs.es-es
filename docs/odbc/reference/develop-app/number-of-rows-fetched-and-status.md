---
title: Número de filas recuperadas y estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20e1632e8da765b0da2785bd846b67d13ebe01ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302366"
---
# <a name="number-of-rows-fetched-and-status"></a>Número de filas recuperadas y estado
Si se ha establecido el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR, especifica un búfer que devuelve el número de filas capturadas por la llamada a **SQLFetch** o **SQLFetchScroll**, y las filas de error. (Este número es un recuento de todas las filas que no tienen el estado SQL_ROW_NO_ROWS). Después de una llamada a **SQLBulkOperations** o **SQLSetPos**, el búfer contiene el número de filas afectadas por una operación masiva realizada por la función. Si se ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, **SQLFetch** o **SQLFetchScroll** devuelve la matriz de *Estado de fila,* que proporciona el estado de cada fila devuelta. Los dos búferes a los que apuntan estos campos son asignados por la aplicación y rellenados por el controlador. Una aplicación debe asegurarse de que estos punteros sigan siendo válidos hasta que se cierre el cursor.  
  
 Las entradas de la matriz de estado de fila especifican si cada fila se capturó correctamente, si se actualizó, agregó o eliminó desde que se recuperó por última vez, y si se produjo un error al capturar la fila. Si **SQLFetch** o **SQLFetchScroll** detecta un error al recuperar una fila de un conjunto de filas MultiRow, o si **SQLBulkOperations** con un argumento de *operación* de SQL_FETCH_BY_BOOKMARK encuentra un error mientras realiza una captura masiva, establece el valor correspondiente en la matriz de estado de fila en SQL_ROW_ERROR, continúa recuperando filas y devuelve SQL_SUCCESS_WITH_INFO. Para obtener más información sobre el control de errores y la matriz de estado de fila, vea las descripciones de las funciones [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) y [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) .
