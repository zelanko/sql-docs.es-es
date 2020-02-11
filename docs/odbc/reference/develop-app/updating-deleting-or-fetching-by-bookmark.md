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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce43cb1d5563128e840aa3c0df26190524774a38
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091634"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Actualizar, eliminar o capturar marcador
Los marcadores se pueden utilizar para identificar los datos que se van a actualizar en el conjunto de resultados, eliminarse del conjunto de resultados o recuperarse del conjunto de resultados a los búferes del conjunto de filas. Estas operaciones se realizan mediante una llamada a **SQLBulkOperations** con un argumento de *opción* de SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK. Los marcadores utilizados en estas operaciones se almacenan en la columna 0 de los búferes del conjunto de filas. Al actualizar por marcador, los datos en los que se actualizan las columnas del conjunto de resultados se recuperan de los búferes del conjunto de filas. Para obtener más información, vea [actualizar datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
