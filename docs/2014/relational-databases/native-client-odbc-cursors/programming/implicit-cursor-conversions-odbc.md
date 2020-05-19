---
title: Conversiones de cursor IMPLÍCITAS (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 99395f9a8dbcb812f5a7764634d42489526875af
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705611"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversiones de cursor implícitas (ODBC)
  Las aplicaciones pueden solicitar un tipo de cursor a través de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) y, a continuación, ejecutar una instrucción SQL que no sea compatible con los cursores de servidor del tipo solicitado. Una llamada a **SQLExecute** o **SQLExecDirect** devuelve SQL_SUCCESS_WITH_INFO y **SQLGetDiagRec** devuelve:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 La aplicación puede determinar qué tipo de cursor se usa ahora llamando a **SQLGetStmtOption** establecido en SQL_CURSOR_TYPE. La conversión del tipo de cursor solamente se aplica a una instrucción. La siguiente **SQLExecDirect** o **SQLExecute** se realizará con la configuración original del cursor de la instrucción.  
  
## <a name="see-also"></a>Consulte también  
 [Detalles de la programación de cursores &#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
