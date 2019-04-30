---
title: SQLFetchScroll (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db7dc5482347ad9b7f194b3c9c8c6cd7fc3f9f6a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199598"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLFetchScroll** función en la biblioteca de cursores. Para obtener información general sobre **SQLFetchScroll**, consulte [función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 La biblioteca de cursores implementa **SQLFetchScroll** llamando repetidamente **SQLFetch** en el controlador. Transfiere los datos que se recupera desde el controlador a los búferes de conjunto de filas proporcionados por la aplicación. También almacena en caché los datos de archivos de disco y memoria. Cuando una aplicación solicita un nuevo conjunto de filas, la biblioteca de cursores recupera según sea necesario desde el controlador (si lo ha no se ha capturado previamente) o la memoria caché (si se ha capturado previamente). Por último, la biblioteca de cursores mantiene el estado de los datos en caché y devuelve esta información a la aplicación en la matriz de Estados de fila.  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetchScroll** no se pueden mezclar con las llamadas a **SQLFetch** o **SQLExtendedFetch**.  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetchScroll** son compatibles para ODBC 2. *x* y para ODBC 3. *x* controladores.  
  
## <a name="rowset-buffers"></a>Búferes del conjunto de filas  
 La biblioteca de cursores optimiza a la transferencia de datos desde el controlador en el búfer del conjunto de filas proporcionado por la aplicación si:  
  
-   La aplicación usa el enlace.  
  
-   No hay ningún byte sin usar entre los campos de la estructura de que la aplicación se declara para almacenar una fila de datos.  
  
-   Los campos en el que **SQLFetch** o **SQLFetchScroll** devuelve el indicador de longitud para una columna sigue el búfer para esa columna y precede el búfer para la columna siguiente. Estos campos son opcionales.  
  
 Cuando la aplicación solicita un nuevo conjunto de filas, la biblioteca de cursores recupera los datos desde su caché y desde el controlador según sea necesario. Si se superponen los conjuntos de filas nuevos y antiguos, la biblioteca de cursores puede optimizar su rendimiento mediante la reutilización de los datos de las secciones de los búferes del conjunto de filas que se superponen. Por lo tanto, se perderán los cambios no guardados a los búferes de conjunto de filas a menos que se superponen los conjuntos de filas nuevos y antiguos y los cambios en las secciones de los búferes del conjunto de filas que se superponen. Para guardar los cambios, una aplicación envía una instrucción de actualización posicionada.  
  
 Tenga en cuenta que la biblioteca de cursores siempre actualiza los búferes del conjunto de filas con datos de la memoria caché cuando una aplicación llama a **SQLFetchScroll** con el *FetchOrientation* establecido en SQL_FETCH_RELATIVE y el *FetchOffset* argumento establecido en 0.  
  
 Admite las llamadas a la biblioteca de cursores **SQLSetStmtAttr** con un *atributo* de SQL_ATTR_ROW_ARRAY_SIZE para cambiar el tamaño del conjunto de filas mientras está abierto un cursor. El nuevo tamaño del conjunto de filas surtirá efecto la próxima vez **SQLFetchScroll** se llama.  
  
## <a name="result-set-membership"></a>Pertenencia al conjunto de resultados  
 La biblioteca de cursores recupera los datos desde el controlador sólo cuando la aplicación lo solicita. Según el origen de datos y el valor del atributo de instrucción SQL_CONCURRENCY, esto tiene las siguientes consecuencias:  
  
-   Los datos recuperados por la biblioteca de cursores pueden diferir de los datos que estaban disponibles en el momento en que se ha ejecutado la instrucción. Por ejemplo, una vez que se abrió el cursor, se pueden recuperar las filas insertadas en un momento posterior a la posición del cursor actual algunos controladores.  
  
-   Los datos del conjunto de resultados podrían estar bloqueados por el origen de datos para la biblioteca de cursores y, por tanto, no esté disponible para otros usuarios.  
  
 Después de la biblioteca de cursores ha almacenado en caché una fila de datos, no puede detectar los cambios en esa fila en el origen de datos subyacente (excepto las actualizaciones posicionadas y eliminaciones en la memoria caché del mismo cursor). Esto ocurre porque, para las llamadas a **SQLFetchScroll**, la biblioteca de cursores nunca vuelve a obtener datos del origen de datos. En su lugar, vuelve a obtener datos desde la memoria caché.  
  
## <a name="scrolling"></a>El desplazamiento  
 La biblioteca de cursores es compatible con los siguientes tipos de captura en **SQLFetchScroll**.  
  
|Tipo de cursor|Tipos de recuperación|  
|-----------------|-----------------|  
|Solo avance|SQL_FETCH_NEXT|  
|Estático|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errores  
 Cuando **SQLFetchScroll** se llama y una de las llamadas a **SQLFetch** devuelve SQL_ERROR, que avanza el cursor biblioteca como sigue. Después de completar estos pasos, la biblioteca de cursores continúa el procesamiento.  
  
1.  Las llamadas **SQLGetDiagRec** para obtener información de error desde el controlador y se publica como un registro de diagnóstico en el Administrador de controladores.  
  
2.  Establece el campo SQL_DIAG_ROW_NUMBER en el registro de diagnóstico en el valor adecuado.  
  
3.  Establece el campo SQL_DIAG_COLUMN_NUMBER en el registro de diagnóstico en el valor adecuado, si es aplicable; en caso contrario, establece en 0.  
  
4.  Establece el valor de la fila de error de la matriz de estado de la fila que SQL_ROW_ERROR.  
  
 Después del cursor se ha llamado biblioteca **SQLFetch** varias veces en su implementación de **SQLFetchScroll**, cualquier error o advertencia devuelto por una de las llamadas a **SQLFetch** estará en un registro de diagnóstico y se puede recuperar mediante una llamada a **SQLGetDiagRec**. Si se truncaron los datos al que se capturó, los datos truncados ahora residen en memoria caché de la biblioteca de cursores. Las llamadas subsiguientes a **SQLFetchScroll** para desplazarse a una fila con datos truncados devolverá los datos truncados y no se generará ninguna advertencia porque se capturan los datos de caché de la biblioteca de cursores. Para realizar un seguimiento de la longitud de los datos devueltos para que pueda determinar si se ha truncado los datos devueltos en un búfer, una aplicación debe enlazar el búfer de longitud/indicador.  
  
## <a name="bookmark-operations"></a>Operaciones de marcador  
 Admite las llamadas a la biblioteca de cursores **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK. También admite la especificación de un desplazamiento en el *FetchOffset* argumento que se puede usar en la operación de marcador. Esta es la única operación de marcador es compatible con la biblioteca de cursores. La biblioteca de cursores no se admite llamar a **SQLBulkOperations**.  
  
 Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS y se ha enlazado a la columna de marcador, la biblioteca de cursores genera un marcador de longitud fija y lo devuelve a la aplicación. La biblioteca de cursores crea y mantiene los marcadores que usa; no usa marcadores que se mantiene en el origen de datos. Cuando **SQLFetchScroll** se llama para recuperar un bloque de datos que ya se han obtenido del origen de datos, recupera los datos de la caché de la biblioteca de cursores. Como resultado, se utiliza el marcador en una llamada a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK deben ser creadas y mantenidas por la biblioteca de cursores.  
  
## <a name="interaction-with-other-functions"></a>Interacción con otras funciones  
 Una aplicación debe llamar a **SQLFetch** o **SQLFetchScroll** antes de que se prepara o ejecuta cualquiera coloca instrucciones update o delete.
