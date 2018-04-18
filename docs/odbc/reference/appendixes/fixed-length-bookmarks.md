---
title: Marcadores de longitud fija | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 797a23c4fea5692cd01ce9fd05b56aeac27c3329
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="fixed-length-bookmarks"></a>Marcadores de longitud fija
Si una aplicación ODBC 3*.x* controlador debería funcionar con una API ODBC 2. *x* aplicación que usa marcadores de longitud fija, el controlador deben admitir lo siguiente:  
  
-   SQL_UB_ON como un valor para la opción de instrucción SQL_USE_BOOKMARKS. (SQL_UB_ON está en desuso en ODBC 3*.x*.)  
  
-   La opción de instrucción SQL_GET_BOOKMARK.
