---
title: Marcadores (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9eecd202a17a0a08e8607ebec0caaa31b7b3ca9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199206"
---
# <a name="bookmarks-odbc"></a>Marcadores (ODBC)
Un marcador es un valor utilizado para identificar una fila de datos. El significado del valor de marcador solamente lo conocen el controlador u origen de datos. Por ejemplo, podría ser tan simple como un número de fila o tan complejo como una dirección de disco. Los marcadores en ODBC son un poco diferentes de marcadores en los libros en pantalla real. En un libro real, el lector coloca un marcador en una página específica y, a continuación, busca ese marcador regresar a la página. En ODBC, la aplicación solicita un marcador para una fila determinada, lo almacena y lo pasa de vuelta al cursor para volver a la fila. Por lo tanto, los marcadores en ODBC son similares a anotar un número de página, un lector recordarla y, a continuación, busque la página.  
  
 Para determinar la compatibilidad de un controlador de marcadores, una aplicación llama a **SQLGetInfo** con la opción SQL_BOOKMARK_PERSISTENCE. Los bits de este valor describen lo que sobreviven marcadores de operaciones, como si los marcadores están siendo válidos después de cerrar el cursor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de marcador](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Recuperar marcadores](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Desplazamiento por marcador](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Actualizar, eliminar o capturar marcador](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Comparación de marcadores](../../../odbc/reference/develop-app/comparing-bookmarks.md)
