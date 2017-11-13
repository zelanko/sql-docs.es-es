---
title: Escribir controladores ODBC 3.x | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41ca6ddf1535899ed8e5e0f065cf2f5f0ca19dca
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="writing-odbc-3x-drivers"></a>Controladores ODBC 3.x de escritura
En la siguiente tabla muestra la compatibilidad de la función en una aplicación ODBC 3. *x* controlador y una aplicación ODBC y la asignación que se realiza mediante el Administrador de controladores cuando se llaman a las funciones en una aplicación ODBC 3. *x* controlador.  
  
|Función|Admitida<br /><br /> por un<br /><br /> ODBC 3. *x*<br /><br /> ¿controlador?|Admitida<br /><br /> por un<br /><br /> ODBC 3. *x*<br /><br /> ¿aplicación?|Asignado/compatible<br /><br /> por ODBC 3. *x*<br /><br /> Administrador de controladores para<br /><br /> una aplicación ODBC 3. ¿ *x* controlador?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|No|No [1]|Sí|  
|**SQLAllocEnv**|No|No [1]|Sí|  
|**SQLAllocHandle**|Sí|Sí|No|  
|**SQLAllocStmt**|No|No [1]|Sí|  
|**SQLBindCol**|Sí|Sí|No|  
|**SQLBindParam**|No|Sí [2]|Sí|  
|**SQLBindParameter**|Sí|Sí|No|  
|**SQLBrowseConnect**|Sí|Sí|No|  
|**SQLBulkOperations**|Sí|Sí|No|  
|**SQLCancel**|Sí|Sí|No|  
|**SQLCloseCursor**|Sí|Sí|No|  
|**SQLColAttribute**|Sí|Sí|No|  
|**SQLColAttributes**|No [3]|No|Sí|  
|**SQLColumnPrivileges**|Sí|Sí|No|  
|**SQLColumns**|Sí|Sí|No|  
|**SQLConnect**|Sí|Sí|No|  
|**SQLCopyDesc**|Sí|Sí|Sí [4]|  
|**SQLDataSources**|No|Sí|Sí|  
|**SQLDescribeCol**|Sí|Sí|No|  
|**SQLDescribeParam**|Sí|Sí|No|  
|**SQLDisconnect**|Sí|Sí|No|  
|**SQLDriverConnect**|Sí|Sí|No|  
|**SQLDrivers**|No|Sí|Sí|  
|**SQLEndTran**|Sí|Sí|No|  
|**SQLError**|No|No [1]|Sí|  
|**SQLExecDirect**|Sí|Sí|No|  
|**SQLExecute**|Sí|Sí|No|  
|**SQLExtendedFetch**|Sí|No|No|  
|**SQLFetch**|Sí|Sí|No|  
|**SQLFetchScroll**|Sí|Sí|No|  
|**SQLForeignKeys**|Sí|Sí|No|  
|**SQLFreeConnect**|No|Sí [1]|Sí|  
|**SQLFreeEnv**|No|Sí [1]|Sí|  
|**SQLFreeHandle**|Sí|Sí|No|  
|**SQLFreeStmt**|Sí|Sí|No|  
|**SQLGetConnectAttr**|Sí|Sí|No|  
|**SQLGetConnectOption**|No [5]|No [1]|Sí|  
|**SQLGetCursorName**|Sí|Sí|No|  
|**SQLGetData**|Sí|Sí|No|  
|**SQLGetDescField**|Sí|Sí|No|  
|**SQLGetDescRec**|Sí|Sí|No|  
|**SQLGetDiagField**|Sí|Sí|No|  
|**SQLGetDiagRec**|Sí|Sí|No|  
|**SQLGetEnvAttr**|Sí|Sí|No|  
|**SQLGetFunctions**|No [6]|Sí|Sí|  
|**SQLGetInfo**|Sí|Sí|No|  
|**SQLGetStmtAttr**|Sí|Sí|No|  
|**SQLGetStmtOption**|No [5]|No [1]|Sí|  
|**SQLGetTypeInfo**|Sí|Sí|No|  
|**SQLMoreResults**|Sí|Sí|No|  
|**SQLNativeSql**|Sí|Sí|No|  
|**SQLNumParams**|Sí|Sí|No|  
|**SQLNumResultCols**|Sí|Sí|No|  
|**SQLParamData**|Sí|Sí|No|  
|**SQLParamOptions**|No|No|Sí|  
|**SQLPrepare**|Sí|Sí|No|  
|**SQLPrimaryKeys**|Sí|Sí|No|  
|**SQLProcedureColumns**|Sí|Sí|No|  
|**SQLProcedures**|Sí|Sí|No|  
|**SQLPutData**|Sí|Sí|No|  
|**SQLRowCount**|Sí|Sí|No|  
|**SQLSetConnectAttr**|Sí|Sí|No|  
|**SQLSetConnectOption**|No [5]|No [1]|Sí|  
|**SQLSetCursorName**|Sí|Sí|No|  
|**SQLSetDescField**|Sí|Sí|No|  
|**SQLSetDescRec**|Sí|Sí|No|  
|**SQLSetEnvAttr**|Sí|Sí|No|  
|**SQLSetPos**|Sí|Sí|No|  
|**SQLSetParam**|No|No|Sí|  
|**SQLSetScrollOption**|Sí|Sí|No|  
|**SQLSetStmtAttr**|Sí|Sí|No|  
|**SQLSetStmtOption**|No [5]|No [1]|Sí|  
|**SQLSpecialColumns**|Sí|Sí|No|  
|**SQLStatistics**|Sí|Sí|No|  
|**SQLTablePrivileges**|Sí|Sí|No|  
|**SQLTables**|Sí|Sí|No|  
|**SQLTransact**|No|No [1]|Sí|  
  
 [1] esta función está desusada en ODBC 3. *x*. ODBC 3. *x* aplicaciones no deben utilizar esta función. Sin embargo, una aplicación compatible con ISO CLI o Open Group puede llamar a esta función.  
  
 [2] ODBC 3. *x* las aplicaciones deben utilizar **SQLBindParameter** en lugar de **SQLBindParam**. Sin embargo, una aplicación compatible con ISO CLI o Open Group puede llamar a esta función.  
  
 [3] escritores de controlador deben tener en cuenta que la API ODBC 2. *x* atributos de columna SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE y SQL_COLUMN_LENGTH deben ser compatibles con **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** parcialmente se implementa mediante el Administrador de controladores cuando se está copiando un descriptor a través de conexiones que pertenecen a distintos controladores. Los controladores necesarios para admitir **SQLCopyDesc** a través de dos de sus propias conexiones. Las funciones como **SQLDrivers**, que se implementan únicamente por el Administrador de controladores, no se muestran en esta lista.  
  
 [5] en determinadas circunstancias, los controladores que necesite admitir esta función. Para obtener más información, consulte la página de referencia de esta función.  
  
 [6], el controlador puede optar por admitir **SQLGetFunctions** si el conjunto de funciones que el controlador admite varía en función de la conexión para la conexión.

