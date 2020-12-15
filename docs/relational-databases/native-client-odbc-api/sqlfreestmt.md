---
description: SQLFreeStmt
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 956ce78ae72c39e1986955fcc562c4a2472eb4a1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465196"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Suelen   
      **SQLFreeStmt** no se recomienda en ODBC 3.0 y posterior. Sin embargo, si la aplicación necesita volver a usar la instrucción, debe seguir usando **SQLFreeStmt** con las opciones **SQL_RESET_PARAMS** y **SQL_UNBIND** ). También puede usar [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)y [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para reemplazar o duplicar la función de **SQLFreeStmt** y debe utilizarlos en su lugar.  
  
 En general, es más eficaz reutilizar las instrucciones que eliminarlas y asignar otras nuevas. Sin embargo, en algunas situaciones, como la reutilización de instrucciones, se debe usar SQLFreeStmt.  
  
## <a name="see-also"></a>Consulte también  
 [SQLFreeStmt función)](../../odbc/reference/syntax/sqlfreestmt-function.md)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
