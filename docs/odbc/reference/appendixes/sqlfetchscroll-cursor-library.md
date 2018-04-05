---
title: SQLFetchScroll (biblioteca de cursores) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b07be3c354a67a6d27a355383e5550a203a6fe27
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLFetchScroll** función en la biblioteca de cursores. Para obtener información general sobre **SQLFetchScroll**, consulte [función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 La biblioteca de cursores implementa **SQLFetchScroll** llamando repetidamente **SQLFetch** en el controlador. Transfiere los datos que recupera desde el controlador a los búferes de conjunto de filas proporcionados por la aplicación. También almacena en caché los datos de archivos de disco y memoria. Cuando una aplicación solicita un nuevo conjunto de filas, la biblioteca de cursores recupera según sea necesario desde el controlador (si se ha no se ha capturado previamente) o la memoria caché (si se ha capturado previamente). Por último, la biblioteca de cursores mantiene el estado de los datos en caché y devuelve esta información a la aplicación en la matriz de Estados de fila.  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetchScroll** no se pueden mezclar con llamadas a **SQLFetch** o **SQLExtendedFetch**.  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetchScroll** son compatibles para ODBC 2. *x* y para ODBC 3. *x* controladores.  
  
## <a name="rowset-buffers"></a>Búferes de conjunto de filas  
 La biblioteca de cursores optimiza a la transferencia de datos desde el controlador en el búfer de conjunto de filas proporcionado por la aplicación si:  
  
-   La aplicación utiliza el enlace.  
  
-   No hay ningún byte sin usar entre los campos en la estructura de que la aplicación se declara para contener una fila de datos.  
  
-   Los campos en el que **SQLFetch** o **SQLFetchScroll** devuelve el indicador de longitud de una columna sigue el búfer para esa columna y precede el búfer de la columna siguiente. Estos campos son opcionales.  
  
 Cuando la aplicación solicita un nuevo conjunto de filas, la biblioteca de cursores recupera los datos desde la memoria caché y desde el controlador según sea necesario. Si se superponen los conjuntos de filas nuevas y antiguas, la biblioteca de cursores puede optimizar su rendimiento mediante la reutilización de los datos de las secciones de los búferes de conjunto de filas que se superponen. Por lo tanto, se pierden los cambios no guardados en los búferes del conjunto de filas a menos que se superponen los conjuntos de filas nuevas y antiguas y los cambios en las secciones de los búferes de conjunto de filas que se superponen. Para guardar los cambios, una aplicación envía una instrucción de actualización por posición.  
  
 Tenga en cuenta que la biblioteca de cursores siempre actualiza los búferes de conjunto de filas con los datos de la memoria caché cuando una aplicación llama **SQLFetchScroll** con el *FetchOrientation* establecido en SQL_FETCH_RELATIVE y el *FetchOffset* establecido en 0.  
  
 La biblioteca de cursores admite las llamadas a **SQLSetStmtAttr** con una *atributo* de SQL_ATTR_ROW_ARRAY_SIZE para cambiar el tamaño de conjunto de filas mientras el cursor está abierto. El nuevo tamaño de conjunto de filas surtirán efecto la próxima vez que **SQLFetchScroll** se llama.  
  
## <a name="result-set-membership"></a>Pertenencia a un conjunto de resultados  
 La biblioteca de cursores recupera datos desde el controlador solo cuando la aplicación lo solicita. Según el origen de datos y la configuración del atributo de instrucción SQL_CONCURRENCY, esto tiene las siguientes consecuencias:  
  
-   Los datos recuperados por la biblioteca de cursores pueden diferir de los datos que estaban disponibles en el momento en que se ejecutó la instrucción. Por ejemplo, una vez que se abre el cursor, se pueden recuperar filas insertadas en un momento posterior a la posición del cursor actual algunos controladores.  
  
-   Los datos del conjunto de resultados podrían estar bloqueados por el origen de datos para la biblioteca de cursores y, por tanto, no esté disponible para otros usuarios.  
  
 Después de la biblioteca de cursores ha almacenado en caché de una fila de datos, porque no puede detectar cambios en las filas en el origen de datos subyacente (excepto las actualizaciones por posición y las eliminaciones en funcionamiento en caché del mismo cursor). Esto ocurre porque, para las llamadas a **SQLFetchScroll**, la biblioteca de cursores nunca vuelve a obtener datos del origen de datos. En su lugar, vuelve a obtener datos desde la memoria caché.  
  
## <a name="scrolling"></a>Desplazamiento  
 La biblioteca de cursores es compatible con los siguientes tipos de captura en **SQLFetchScroll**.  
  
|Tipo de cursor|Tipos de recuperación|  
|-----------------|-----------------|  
|Solo avance|SQL_FETCH_NEXT|  
|Estático|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errores  
 Cuando **SQLFetchScroll** se llama y una de las llamadas a **SQLFetch** devuelve SQL_ERROR, los ingresos de la biblioteca de cursor como se indica a continuación. Después de completar estos pasos, la biblioteca de cursores continúa el procesamiento.  
  
1.  Llamadas **SQLGetDiagRec** para obtener información de error desde el controlador y se expone como un registro de diagnóstico en el Administrador de controladores.  
  
2.  Establece el campo SQL_DIAG_ROW_NUMBER en el registro de diagnóstico en el valor adecuado.  
  
3.  Establece el campo SQL_DIAG_COLUMN_NUMBER en el registro de diagnóstico en el valor adecuado, si procede; en caso contrario, establece en 0.  
  
4.  Establece el valor de la fila de error en la matriz de Estados de fila a SQL_ROW_ERROR.  
  
 Después del cursor se llamado biblioteca **SQLFetch** varias veces en su implementación de **SQLFetchScroll**, cualquier error o advertencia devuelta por una de las llamadas a **SQLFetch** estará en un registro de diagnóstico y se pueden recuperar mediante una llamada a **SQLGetDiagRec**. Si se truncaron los datos al que se capturó, los datos truncados ahora residen en memoria caché de la biblioteca de cursores. Las llamadas subsiguientes a **SQLFetchScroll** para desplazarse a una fila con datos truncados devolverá los datos truncados y no se generará ninguna advertencia porque se capturan los datos de caché de la biblioteca de cursores. Para realizar un seguimiento de la longitud de los datos devueltos para que pueda determinar si se ha truncado los datos devueltos en un búfer, una aplicación debe enlazar el búfer de longitud/indicador.  
  
## <a name="bookmark-operations"></a>Operaciones de marcador  
 La biblioteca de cursores admite las llamadas a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK. También admite la especificación de un desplazamiento en el *FetchOffset* argumento que se puede usar en la operación de marcador. Esta es la única operación de marcador es compatible con la biblioteca de cursores. La biblioteca de cursores no permite llamar a **SQLBulkOperations**.  
  
 Si la aplicación ha establecido el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS y se ha enlazado a la columna de marcador, la biblioteca de cursores genera un marcador de longitud fija y lo devuelve a la aplicación. La biblioteca de cursores crea y mantiene los marcadores que usa; no usa marcadores que se mantiene en el origen de datos. Cuando **SQLFetchScroll** se llama para recuperar un bloque de datos que ya se hayan extraído del origen de datos, recupera los datos de la caché de la biblioteca de cursores. Como resultado, se utiliza el marcador en una llamada a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK debe ser creadas y mantenidas por la biblioteca de cursores.  
  
## <a name="interaction-with-other-functions"></a>Interacción con otras funciones  
 Una aplicación debe llamar a **SQLFetch** o **SQLFetchScroll** antes de que se prepara o ejecuta cualquiera coloca instrucciones update o delete.
