---
title: SQLFreeStmt | Documentos de Microsoft
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 56b902d8be50a1ce0a69c273d195659c3d835030
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Por lo general   
      **SQLFreeStmt** no se recomienda en ODBC 3.0 y posterior. Sin embargo si la aplicación debe volver a usar la instrucción debe tener **SQLFreeStmt** con el **SQL_RESET_PARAMS** y **SQL_UNBIND** opciones). También se pueden usar [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md), y [ SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) a reemplazan o duplican la función de **SQLFreeStmt** y debe usar en su lugar.  
  
 En general, resulta más eficaz volver a usar las instrucciones que to quitarlos y asignar unos nuevos. No obstante en algunas situaciones, como la reutilización de instrucciones, SQLFreeStmt debe utilizarse.  
  
## <a name="see-also"></a>Vea también  
 [SQLFreeStmt, función](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [Detalles de implementación de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
