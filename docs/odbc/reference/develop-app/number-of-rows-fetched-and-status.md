---
title: "Número de filas recuperadas y estado | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45d53845cdbda6ab7cec5e17fdeedf3c6d6cd832
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="number-of-rows-fetched-and-status"></a>Número de filas recuperadas y estado
Si se ha establecido el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR, especifica un búfer que devuelve el número de filas recuperadas por la llamada a **SQLFetch** o **SQLFetchScroll**y las filas de error. (Este número es un recuento de todas las filas que no tienen el estado SQL_ROW_NO_ROWS). Después de llamar a **SQLBulkOperations** o **SQLSetPos**, el búfer contiene el número de filas afectadas por una operación masiva realizada por la función. Si se ha establecido el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR, **SQLFetch** o **SQLFetchScroll** devuelve el *matriz de Estados de fila,* que proporciona el estado de cada uno fila devuelta. Ambos de los búferes señalados por estos campos asignados por la aplicación y rellena el controlador. Una aplicación debe asegurarse de que estos punteros sigan siendo válidos hasta que se cierra el cursor.  
  
 Las entradas en el estado de matriz de estado de la fila si cada fila se capturó correctamente, si se ha actualizado, agregan o eliminan desde que se capturó en último lugar, y si se produjo un error al capturar la fila. Si **SQLFetch** o **SQLFetchScroll** encuentra un error al recuperar una fila de un conjunto de filas de varias filas, o si **SQLBulkOperations** con un *operación*  argumento de SQL_FETCH_BY_BOOKMARK encuentra un error al realizar una captura de forma masiva, Establece el valor correspondiente en la matriz de Estados de fila para SQL_ROW_ERROR, continúa capturar las filas y devuelve SQL_SUCCESS_WITH_INFO. Para obtener más información acerca de control de errores y la matriz de Estados de fila, vea el [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) y [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) función descripciones.
