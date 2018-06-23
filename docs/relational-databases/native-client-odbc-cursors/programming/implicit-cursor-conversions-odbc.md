---
title: Conversiones de Cursor implícitas (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9bb02c47c6da08a26b911b6407b5efeeeb204c13
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696206"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversiones de cursor implícitas (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Las aplicaciones pueden solicitar un tipo de cursor a través de [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) y, a continuación, ejecutar una instrucción SQL que no es compatible con los cursores de servidor del tipo solicitado. Una llamada a **SQLExecute** o **SQLExecDirect** devuelve SQL_SUCCESS_WITH_INFO y **SQLGetDiagRec** devuelve:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 La aplicación puede determinar qué tipo de cursor ahora está usándola mediante una llamada a **SQLGetStmtOption** establecido en SQL_CURSOR_TYPE. La conversión del tipo de cursor solamente se aplica a una instrucción. La siguiente **SQLExecDirect** o **SQLExecute** se hará mediante la configuración original de cursor de instrucción.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de la programación de cursor &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
