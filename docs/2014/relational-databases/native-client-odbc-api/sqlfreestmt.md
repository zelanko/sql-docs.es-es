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
author: rothja
ms.author: jroth
ms.openlocfilehash: d38237b53ed994fd3272f9e129564320f88c6e37
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022397"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt** no se recomienda en ODBC 3.0 y posterior. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite todos los valores *Option* definidos para **SQLFreeStmt**. No obstante, [SQLCloseCursor](sqlclosecursor.md), [SQLBindParameter](sqlbindparameter.md), [SQLBindCol](sqlbindcol.md), **SQLSetDescField**y [SQLFreeHandle](sqlfreehandle.md) reemplazan o duplican la función de **SQLFreeStmt** y se utilizan en su lugar.  
  
## <a name="see-also"></a>Consulte también  
 [SQLFreeStmt función)](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
