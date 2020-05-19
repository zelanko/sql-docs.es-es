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
manager: craigg
ms.openlocfilehash: 9b7fbc3754121418ea2059ea511f3b247dcff8dd
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706090"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt** no se recomienda en ODBC 3.0 y posterior. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite todos los valores *Option* definidos para **SQLFreeStmt**. No obstante, [SQLCloseCursor](sqlclosecursor.md), [SQLBindParameter](sqlbindparameter.md), [SQLBindCol](sqlbindcol.md), **SQLSetDescField**y [SQLFreeHandle](sqlfreehandle.md) reemplazan o duplican la función de **SQLFreeStmt** y se utilizan en su lugar.  
  
## <a name="see-also"></a>Consulte también  
 [SQLFreeStmt función)](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
