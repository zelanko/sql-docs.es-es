---
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b985db3cb58a7029a3b5ec489d2e23b0c1292919
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786729"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Suelen   
      **SQLFreeStmt** no se recomienda en ODBC 3.0 y posterior. Sin embargo, si la aplicación necesita volver a usar la instrucción, debe seguir usando **SQLFreeStmt** con las opciones **SQL_RESET_PARAMS** y **SQL_UNBIND** ). También puede usar [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)y [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para reemplazar o duplicar la función de **SQLFreeStmt** y debe utilizarlos en su lugar.  
  
 En general, es más eficaz reutilizar las instrucciones que eliminarlas y asignar otras nuevas. Sin embargo, en algunas situaciones, como la reutilización de instrucciones, se debe usar SQLFreeStmt.  
  
## <a name="see-also"></a>Vea también  
   de la [función SQLFreeStmt](https://go.microsoft.com/fwlink/?LinkId=59346)  
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
