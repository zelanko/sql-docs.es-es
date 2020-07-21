---
title: Actualizar, eliminar o capturar por marcador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e94a98bb577ef906afbb04539761fd07d15f772
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286155"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Actualizar, eliminar o capturar marcador
Los marcadores se pueden utilizar para identificar los datos que se van a actualizar en el conjunto de resultados, eliminarse del conjunto de resultados o recuperarse del conjunto de resultados a los búferes del conjunto de filas. Estas operaciones se realizan mediante una llamada a **SQLBulkOperations** con un argumento de *opción* de SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK. Los marcadores utilizados en estas operaciones se almacenan en la columna 0 de los búferes del conjunto de filas. Al actualizar por marcador, los datos en los que se actualizan las columnas del conjunto de resultados se recuperan de los búferes del conjunto de filas. Para obtener más información, vea [actualizar datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
