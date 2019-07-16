---
title: Escritura de controladores ODBC 3.x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb403cef47f901cdb43bbb32c669ba68aa34913d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078905"
---
# <a name="writing-odbc-3x-drivers"></a>Controladores ODBC 3.x de escritura
En la tabla siguiente se muestra la compatibilidad de la función en una aplicación ODBC 3. *x* controlador y una aplicación ODBC y la asignación que se realiza mediante el Administrador de controladores cuando se llaman las funciones en una aplicación ODBC 3. *x* controlador.  
  
|Función|Compatible<br /><br /> por un<br /><br /> ODBC 3.*x*<br /><br /> ¿controlador?|Compatible<br /><br /> por un<br /><br /> ODBC 3.*x*<br /><br /> ¿aplicación?|Compatible o asignado<br /><br /> por ODBC 3. *x*<br /><br /> Administrador de controladores para<br /><br /> una aplicación ODBC 3. ¿ *x* controlador?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|Sin|No[1]|Sí|  
|**SQLAllocEnv**|Sin|No[1]|Sí|  
|**SQLAllocHandle**|Sí|Sí|Sin|  
|**SQLAllocStmt**|Sin|No[1]|Sí|  
|**SQLBindCol**|Sí|Sí|No|  
|**SQLBindParam**|Sin|Sí [2]|Sí|  
|**SQLBindParameter**|Sí|Sí|Sin|  
|**SQLBrowseConnect**|Sí|Sí|Sin|  
|**SQLBulkOperations**|Sí|Sí|No|  
|**SQLCancel**|Sí|Sí|Sin|  
|**SQLCloseCursor**|Sí|Sí|Sin|  
|**SQLColAttribute**|Sí|Sí|No|  
|**SQLColAttributes**|No[3]|No|Sí|  
|**SQLColumnPrivileges**|Sí|Sí|Sin|  
|**SQLColumns**|Sí|Sí|Sin|  
|**SQLConnect**|Sí|Sí|Sin|  
|**SQLCopyDesc**|Sí|Sí|Sí [4]|  
|**SQLDataSources**|No|Sí|Sí|  
|**SQLDescribeCol**|Sí|Sí|No|  
|**SQLDescribeParam**|Sí|Sí|Sin|  
|**SQLDisconnect**|Sí|Sí|Sin|  
|**SQLDriverConnect**|Sí|Sí|Sin|  
|**SQLDrivers**|No|Sí|Sí|  
|**SQLEndTran**|Sí|Sí|Sin|  
|**SQLError**|Sin|No[1]|Sí|  
|**SQLExecDirect**|Sí|Sí|No|  
|**SQLExecute**|Sí|Sí|Sin|  
|**SQLExtendedFetch**|Sí|Sin|Sin|  
|**SQLFetch**|Sí|Sí|No|  
|**SQLFetchScroll**|Sí|Sí|Sin|  
|**SQLForeignKeys**|Sí|Sí|No|  
|**SQLFreeConnect**|Sin|Sí [1]|Sí|  
|**SQLFreeEnv**|No|Sí [1]|Sí|  
|**SQLFreeHandle**|Sí|Sí|Sin|  
|**SQLFreeStmt**|Sí|Sí|No|  
|**SQLGetConnectAttr**|Sí|Sí|Sin|  
|**SQLGetConnectOption**|No[5]|No[1]|Sí|  
|**SQLGetCursorName**|Sí|Sí|No|  
|**SQLGetData**|Sí|Sí|Sin|  
|**SQLGetDescField**|Sí|Sí|Sin|  
|**SQLGetDescRec**|Sí|Sí|Sin|  
|**SQLGetDiagField**|Sí|Sí|Sin|  
|**SQLGetDiagRec**|Sí|Sí|No|  
|**SQLGetEnvAttr**|Sí|Sí|Sin|  
|**SQLGetFunctions**|No[6]|Sí|Sí|  
|**SQLGetInfo**|Sí|Sí|No|  
|**SQLGetStmtAttr**|Sí|Sí|Sin|  
|**SQLGetStmtOption**|No[5]|No[1]|Sí|  
|**SQLGetTypeInfo**|Sí|Sí|Sin|  
|**SQLMoreResults**|Sí|Sí|No|  
|**SQLNativeSql**|Sí|Sí|Sin|  
|**SQLNumParams**|Sí|Sí|Sin|  
|**SQLNumResultCols**|Sí|Sí|Sin|  
|**SQLParamData**|Sí|Sí|Sin|  
|**SQLParamOptions**|Sin|Sin|Sí|  
|**SQLPrepare**|Sí|Sí|No|  
|**SQLPrimaryKeys**|Sí|Sí|Sin|  
|**SQLProcedureColumns**|Sí|Sí|Sin|  
|**SQLProcedures**|Sí|Sí|Sin|  
|**SQLPutData**|Sí|Sí|Sin|  
|**SQLRowCount**|Sí|Sí|Sin|  
|**SQLSetConnectAttr**|Sí|Sí|Sin|  
|**SQLSetConnectOption**|No[5]|No[1]|Sí|  
|**SQLSetCursorName**|Sí|Sí|No|  
|**SQLSetDescField**|Sí|Sí|Sin|  
|**SQLSetDescRec**|Sí|Sí|No|  
|**SQLSetEnvAttr**|Sí|Sí|No|  
|**SQLSetPos**|Sí|Sí|No|  
|**SQLSetParam**|Sin|No|Sí|  
|**SQLSetScrollOption**|Sí|Sí|Sin|  
|**SQLSetStmtAttr**|Sí|Sí|No|  
|**SQLSetStmtOption**|No[5]|No[1]|Sí|  
|**SQLSpecialColumns**|Sí|Sí|No|  
|**SQLStatistics**|Sí|Sí|Sin|  
|**SQLTablePrivileges**|Sí|Sí|Sin|  
|**SQLTables**|Sí|Sí|Sin|  
|**SQLTransact**|No|No[1]|Sí|  
  
 [1] esta función está en desuso en ODBC 3. *x*. ODBC 3. *x* aplicaciones no deben utilizar esta función. Sin embargo, un grupo de abierto o aplicación compatible con ISO CLI puede llamar a esta función.  
  
 [2] ODBC 3. *x* las aplicaciones deben usar **SQLBindParameter** en lugar de **SQLBindParam**. Sin embargo, un grupo de abierto o aplicación compatible con ISO CLI puede llamar a esta función.  
  
 [3] los escritores de controlador deben tener en cuenta que la API ODBC 2. *x* atributos de columna SQL_COLUMN_PRECISION SQL_COLUMN_SCALE y SQL_COLUMN_LENGTH deben ser compatibles con **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** parcialmente se implementa mediante el Administrador de controladores cuando se está copiando un descriptor de a través de conexiones que pertenecen a distintos controladores. Los controladores necesarios para admitir **SQLCopyDesc** entre dos de sus propias conexiones. Las funciones como **SQLDrivers**, que se implementan únicamente por el Administrador de controladores, no se muestran en esta lista.  
  
 [5] en determinadas circunstancias, los controladores que necesite admitir esta función. Para obtener más información, consulte la página de referencia de la función.  
  
 [6], el controlador puede optar por admitir **SQLGetFunctions** si el conjunto de funciones que admite el controlador varía en función de la conexión a la conexión.
