---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5877a6cb7a99803f854338321e333c87037c2e90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67913583"
---
# <a name="fixed-length-bookmarks"></a>Marcadores de longitud fija
Si un controlador ODBC *3. x* debe trabajar con una aplicación ODBC *2. x* que usa marcadores de longitud fija, el controlador debe admitir lo siguiente:  
  
-   SQL_UB_ON como un valor para la opción de la instrucción SQL_USE_BOOKMARKS. (SQL_UB_ON está en desuso en ODBC *3. x*).  
  
-   La opción de instrucción SQL_GET_BOOKMARK.
