---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4aa7e597bcfa80d7d45064c844986018d64617d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63190306"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt** no se recomienda en ODBC 3.0 y posterior. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite todos los valores *Option* definidos para **SQLFreeStmt**. No obstante, [SQLCloseCursor](sqlclosecursor.md), [SQLBindParameter](sqlbindparameter.md), [SQLBindCol](sqlbindcol.md), **SQLSetDescField**y [SQLFreeHandle](sqlfreehandle.md) reemplazan o duplican la función de **SQLFreeStmt** y se utilizan en su lugar.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLFreeStmt](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
