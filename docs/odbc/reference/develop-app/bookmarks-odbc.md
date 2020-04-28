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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8273c82b918024417e613ea44a2d26bafaf7d76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306326"
---
# <a name="bookmarks-odbc"></a>Marcadores (ODBC)
Un marcador es un valor utilizado para identificar una fila de datos. El significado del valor de marcador solamente lo conocen el controlador u origen de datos. Por ejemplo, podría ser tan simple como un número de fila o tan complejo como una dirección de disco. Los marcadores de ODBC son un poco diferentes de los marcadores en los libros reales. En un libro real, el lector coloca un marcador en una página específica y, a continuación, busca ese marcador para volver a la página. En ODBC, la aplicación solicita un marcador para una fila determinada, lo almacena y lo pasa de vuelta al cursor para volver a la fila. Por lo tanto, los marcadores de ODBC son similares a un lector que escribe un número de página, lo recuerda y, a continuación, vuelve a buscar la página.  
  
 Para determinar la compatibilidad de un controlador con los marcadores, una aplicación llama a **SQLGetInfo** con la opción SQL_BOOKMARK_PERSISTENCE. Los bits de este valor describen qué sobreviven los marcadores de operaciones, por ejemplo, si los marcadores siguen siendo válidos después de cerrarse el cursor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de marcador](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Recuperar marcadores](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Desplazamiento por marcador](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Actualizar, eliminar o capturar marcador](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Comparación de marcadores](../../../odbc/reference/develop-app/comparing-bookmarks.md)
