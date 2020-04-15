---
title: SQLFetchScroll (Biblioteca de cursores) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5573b8afc49afec8b7afa4fc52590e7a6a9e2fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302056"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLFetchScroll** en la biblioteca de cursores. Para obtener información general acerca de **SQLFetchScroll**, vea [SQLFetchScroll (Función).](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
 La biblioteca de cursores implementa **SQLFetchScroll** llamando repetidamente a **SQLFetch** en el controlador. Transfiere los datos que recupera del controlador a los búferes de conjunto de filas proporcionados por la aplicación. También almacena en caché los datos en archivos de memoria y disco. Cuando una aplicación solicita un nuevo conjunto de filas, la biblioteca de cursores lo recupera según sea necesario del controlador (si no se ha capturado previamente) o de la memoria caché (si se ha capturado previamente). Por último, la biblioteca de cursores mantiene el estado de los datos almacenados en caché y devuelve esta información a la aplicación en la matriz de estado de fila.  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetchScroll** no se pueden mezclar con llamadas a **SQLFetch** o **SQLExtendedFetch**.  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetchScroll** se admiten tanto para ODBC 2. *x* y para ODBC 3. *x* controladores.  
  
## <a name="rowset-buffers"></a>Búferes de conjunto de filas  
 La biblioteca de cursores optimiza la transferencia de datos desde el controlador al búfer del conjunto de filas proporcionado por la aplicación si:  
  
-   La aplicación usa el enlace de fila.  
  
-   No hay bytes no utilizados entre los campos de la estructura que la aplicación declara contener una fila de datos.  
  
-   Los campos en los que **SQLFetch** o **SQLFetchScroll** devuelve la longitud/indicador de una columna sigue el búfer de esa columna y precede al búfer de la siguiente columna. Estos campos son opcionales.  
  
 Cuando la aplicación solicita un nuevo conjunto de filas, la biblioteca de cursores recupera datos de su caché y del controlador según sea necesario. Si los conjuntos de filas nuevos y antiguos se superponen, la biblioteca de cursores puede optimizar su rendimiento reutilizando los datos de las secciones superpuestas de los búferes del conjunto de filas. Por lo tanto, los cambios no guardados en los búferes del conjunto de filas se pierden a menos que los conjuntos de filas nuevos y antiguos se superpongan y los cambios se encuentran en las secciones superpuestas de los búferes del conjunto de filas. Para guardar los cambios, una aplicación envía una instrucción de actualización posicionada.  
  
 Tenga en cuenta que la biblioteca de cursores siempre actualiza los búferes de conjunto de filas con datos de la memoria caché cuando una aplicación llama a **SQLFetchScroll** con el *FetchOrientation* argumento establecido en SQL_FETCH_RELATIVE y el *FetchOffset* argumento establecido en 0.  
  
 La biblioteca de cursores admite la llamada a **SQLSetStmtAttr** con un *atributo* de SQL_ATTR_ROW_ARRAY_SIZE cambiar el tamaño del conjunto de filas mientras está abierto un cursor. El nuevo tamaño del conjunto de filas surtirá efecto la próxima vez que **SQLFetchScroll** se llame.  
  
## <a name="result-set-membership"></a>Membresía de conjunto de resultados  
 La biblioteca de cursores recupera datos del controlador solo cuando la aplicación los solicita. Según el origen de datos y la configuración del atributo de instrucción SQL_CONCURRENCY, esto tiene las siguientes consecuencias:  
  
-   Los datos recuperados por la biblioteca de cursores pueden diferir de los datos que estaban disponibles en el momento en que se ejecutó la instrucción. Por ejemplo, después de abrir el cursor, algunos controladores pueden recuperar filas insertadas en un punto más allá de la posición actual del cursor.  
  
-   Es posible que el origen de datos de la biblioteca de cursores bloquee los datos del conjunto de resultados y, por lo tanto, no estén disponibles para otros usuarios.  
  
 Después de que la biblioteca de cursores haya almacenado en caché una fila de datos, no puede detectar cambios en esa fila en el origen de datos subyacente (excepto para las actualizaciones y eliminaciones posicionadas que funcionan en la misma memoria caché del cursor). Esto ocurre porque, para las llamadas a **SQLFetchScroll**, la biblioteca de cursores nunca recupera datos del origen de datos. En su lugar, recupera los datos de su caché.  
  
## <a name="scrolling"></a>Desplazarse  
 La biblioteca de cursores admite los siguientes tipos de captura en **SQLFetchScroll**.  
  
|Tipo de cursor|Tipos de captura|  
|-----------------|-----------------|  
|Solo avance|SQL_FETCH_NEXT|  
|estática|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errors  
 Cuando **SQLFetchScroll** se llama y una de las llamadas a **SQLFetch** devuelve SQL_ERROR, la biblioteca de cursores continúa de la siguiente manera. Después de completar estos pasos, la biblioteca de cursores continúa el procesamiento.  
  
1.  Llama a **SQLGetDiagRec** para obtener información de error del controlador y lo publica como un registro de diagnóstico en el Administrador de controladores.  
  
2.  Establece el campo SQL_DIAG_ROW_NUMBER del registro de diagnóstico en el valor adecuado.  
  
3.  Establece el campo SQL_DIAG_COLUMN_NUMBER del registro de diagnóstico en el valor adecuado, si procede; de lo contrario, lo establece en 0.  
  
4.  Establece el valor de la fila en error en la matriz de estado de fila en SQL_ROW_ERROR.  
  
 Después de que la biblioteca de cursores haya llamado a **SQLFetch** varias veces en su implementación de **SQLFetchScroll**, cualquier error o advertencia devuelto por una de las llamadas a **SQLFetch** estará en un registro de diagnóstico y se puede recuperar mediante una llamada a **SQLGetDiagRec**. Si los datos se truncaron cuando se capturaron, los datos truncados ahora residirán en la memoria caché de la biblioteca de cursores. Las llamadas posteriores a **SQLFetchScroll** para desplazarse a una fila con datos truncados devolverán los datos truncados y no se generará ninguna advertencia porque los datos se recuperan de la memoria caché de la biblioteca de cursores. Para realizar un seguimiento de la longitud de los datos devueltos para que pueda determinar si los datos devueltos en un búfer se han truncado, una aplicación debe enlazar el búfer de longitud/indicador.  
  
## <a name="bookmark-operations"></a>Operaciones de marcadores  
 La biblioteca de cursores admite la llamada a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK. También admite la especificación de un desplazamiento en el *FetchOffset* argumento que se puede utilizar en la operación de marcador. Esta es la única operación de marcador que admite la biblioteca de cursores. La biblioteca de cursores no admite la llamada a **SQLBulkOperations**.  
  
 Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS y ha enlazado a la columna de marcador, la biblioteca de cursores genera un marcador de longitud fija y lo devuelve a la aplicación. La biblioteca de cursores crea y mantiene los marcadores que utiliza; no utiliza marcadores mantenidos en el origen de datos. Cuando **SQLFetchScroll** se llama para recuperar un bloque de datos que ya se ha obtenido del origen de datos, recupera los datos de la memoria caché de la biblioteca de cursores. Como resultado, el marcador utilizado en una llamada a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK debe crear y mantener la biblioteca de cursores.  
  
## <a name="interaction-with-other-functions"></a>Interacción con otras funciones  
 Una aplicación debe llamar a **SQLFetch** o **SQLFetchScroll** antes de preparar o ejecutar cualquier actualización o eliminación posicionada instrucciones.
