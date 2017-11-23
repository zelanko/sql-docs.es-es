---
title: Marcadores de longitud fija | Documentos de Microsoft
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
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20f9d91887f020cd6753ed8be684e5caa32ba99c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="fixed-length-bookmarks"></a>Marcadores de longitud fija
Si una aplicación ODBC 3*.x* controlador debería funcionar con una API ODBC 2. *x* aplicación que usa marcadores de longitud fija, el controlador deben admitir lo siguiente:  
  
-   SQL_UB_ON como un valor para la opción de instrucción SQL_USE_BOOKMARKS. (SQL_UB_ON está en desuso en ODBC 3*.x*.)  
  
-   La opción de instrucción SQL_GET_BOOKMARK.
