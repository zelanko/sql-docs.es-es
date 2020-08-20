---
description: Marcadores de longitud fija
title: Marcadores de longitud fija | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d357ba96141c658889628941c7f9492db5fd6b66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466181"
---
# <a name="fixed-length-bookmarks"></a>Marcadores de longitud fija
Si un controlador ODBC *3. x* debe trabajar con una aplicación ODBC *2. x* que usa marcadores de longitud fija, el controlador debe admitir lo siguiente:  
  
-   SQL_UB_ON como un valor para la opción de la instrucción SQL_USE_BOOKMARKS. (SQL_UB_ON está en desuso en ODBC *3. x*).  
  
-   La opción de instrucción SQL_GET_BOOKMARK.
