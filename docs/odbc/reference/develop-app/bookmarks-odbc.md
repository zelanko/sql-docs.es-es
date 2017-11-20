---
title: Marcadores (ODBC) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 791350c93e2570ad8615e5b378e9979870e02acf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="bookmarks-odbc"></a>Marcadores (ODBC)
Un marcador es un valor utilizado para identificar una fila de datos. El significado del valor de marcador solamente lo conocen el controlador u origen de datos. Por ejemplo, podría ser tan simple como un número de fila o tan complejo como una dirección de disco. Los marcadores en ODBC son ligeramente distintos de marcadores en los libros reales. En un libro real, el lector situará un marcador en una página específica y, a continuación, busca este marcador regresar a la página. En ODBC, la aplicación solicita un marcador para una fila determinada, lo almacena y lo pasa de vuelta al cursor para volver a la fila. Por lo tanto, marcadores en ODBC son similares a un lector de escribir un número de página, teniendo en cuenta y, a continuación, examinar de nuevo la página.  
  
 Para determinar la compatibilidad del controlador de marcadores, llama a una aplicación **SQLGetInfo** con la opción SQL_BOOKMARK_PERSISTENCE. Los bits de este valor describen lo que sobreviven marcadores de operaciones, como si los marcadores están siendo válidos después de que se cierra el cursor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de marcador](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Recuperar marcadores](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Desplazamiento por marcador](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Actualizar, eliminar o capturar marcador](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Comparación de marcadores](../../../odbc/reference/develop-app/comparing-bookmarks.md)

