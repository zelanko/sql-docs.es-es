---
title: SQLExtendedFetch (biblioteca de cursores) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c900dd244199051ef8c35baf5ae84a328cb3fb2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLExtendedFetch** función en la biblioteca de cursores. Para obtener información general sobre **SQLExtendedFetch**, consulte [SQLExtendedFetch función](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 La biblioteca de cursores implementa **SQLExtendedFetch** llamando repetidamente **SQLFetch** en el controlador.  
  
 La biblioteca de cursores admite las llamadas a **SQLExtendedFetch** con un *FetchOrientation* de SQL_FETCH_BOOKMARK.  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLExtendedFetch** no se pueden mezclar con llamadas a **SQLFetchScroll** o **SQLFetch**.
