---
title: Actualizar, eliminar o marcador de filas | Documentos de Microsoft
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
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2e31884db8fda0ef62458d2c77408cc889a2a4c0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Actualizar, eliminar o capturar marcador
Marcadores pueden usarse para identificar los datos que se actualizará en el conjunto de resultados que se eliminan del resultado establecer o el conjunto de resultados a los búferes de conjunto de filas que se captura. Estas operaciones se realizan mediante una llamada a **SQLBulkOperations** con una *opción* argumento de SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK. Los marcadores que se utilizan en estas operaciones se almacenan en la columna 0 de los búferes de conjunto de filas. Al actualizar por marcador, se actualizan los datos que son el resultado de las columnas de conjunto a se recupera de los búferes de conjunto de filas. Para obtener más información, consulte [actualizar los datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
