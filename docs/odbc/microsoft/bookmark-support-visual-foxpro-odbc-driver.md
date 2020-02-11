---
title: Compatibilidad con marcadores (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], bookmarks
- Visual FoxPro ODBC driver [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: feb7ec20-3e0c-4a47-8feb-7dd9f23efdf6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6f6bd1e8b2bea09822b46a325d1531a7b087a71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138097"
---
# <a name="bookmark-support-visual-foxpro-odbc-driver"></a>Compatibilidad con marcadores (controlador ODBC de Visual FoxPro)
El controlador ODBC de Visual FoxPro admite marcadores simples. Cuando se llama a [SQLGetInfo](../../odbc/microsoft/sqlgetinfo-visual-foxpro-odbc-driver.md) con el SQL_BOOKMARK_PERSISTENCE *InfoType*, el valor devuelto es SQL_BP_SCROLL.  
  
 Para obtener más información sobre los marcadores, vea [marcadores (ODBC)](../../odbc/reference/develop-app/bookmarks-odbc.md).
