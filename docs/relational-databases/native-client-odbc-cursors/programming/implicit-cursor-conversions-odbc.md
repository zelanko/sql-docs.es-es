---
description: Conversiones de cursor implícitas (ODBC)
title: Conversiones de cursor IMPLÍCITAS (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b07b3bc1dd045b42e3e7a56f40f63504b0cf38f2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438575"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversiones de cursor implícitas (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Las aplicaciones pueden solicitar un tipo de cursor a través de [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) y, a continuación, ejecutar una instrucción SQL que no sea compatible con los cursores de servidor del tipo solicitado. Una llamada a **SQLExecute** o **SQLExecDirect** devuelve SQL_SUCCESS_WITH_INFO y **SQLGetDiagRec** devuelve:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 La aplicación puede determinar qué tipo de cursor se usa ahora llamando a **SQLGetStmtOption** establecido en SQL_CURSOR_TYPE. La conversión del tipo de cursor solamente se aplica a una instrucción. La siguiente **SQLExecDirect** o **SQLExecute** se realizará con la configuración original del cursor de la instrucción.  
  
## <a name="see-also"></a>Consulte también  
 [Detalles de la programación de cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
