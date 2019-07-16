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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc1f556873221faa3f86c5272120a786f6f25025
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086335"
---
# <a name="number-of-rows-fetched-and-status"></a>Número de filas recuperadas y estado
Si se ha establecido el atributo SQL_ATTR_ROWS_FETCHED_PTR la instrucción, especifica un búfer que devuelve el número de filas recuperadas por la llamada a **SQLFetch** o **SQLFetchScroll**y las filas de error. (Este número es un recuento de todas las filas que no tienen el estado SQL_ROW_NO_ROWS). Después de llamar a **SQLBulkOperations** o **SQLSetPos**, el búfer contiene el número de filas afectadas por una operación masiva realizada por la función. Si se ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, **SQLFetch** o **SQLFetchScroll** devuelve el *matriz de Estados de fila,* que proporciona el estado de cada fila devuelta. Ambos de los búferes apuntados a estos campos asignados por la aplicación y rellenados por el controlador. Una aplicación debe asegurarse de que estos punteros siguen siendo válidos hasta que se cierra el cursor.  
  
 Las entradas en el estado de matriz de estado de fila si cada fila se capturó correctamente, si se actualizó, agregan o eliminan desde que se capturó por última vez, y si se ha producido un error al capturar la fila. Si **SQLFetch** o **SQLFetchScroll** encuentra un error al recuperar una fila de un conjunto de filas de varias filas, o si **SQLBulkOperations** con un *operación*  argumento de SQL_FETCH_BY_BOOKMARK encuentra un error al realizar una captura de forma masiva, Establece el valor correspondiente de la matriz de estado de la fila que SQL_ROW_ERROR, continúa la captura de filas y devuelve SQL_SUCCESS_WITH_INFO. Para obtener más información acerca de la matriz de Estados de fila y de control de errores, vea el [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) y [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) función descripciones.
