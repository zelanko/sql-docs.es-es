---
title: Escritura de controladores ODBC 3.x Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62f2a701fd5ac94c92d41494a4fd1ab023edaf25
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300365"
---
# <a name="writing-odbc-3x-drivers"></a>Controladores ODBC 3.x de escritura
En la tabla siguiente se muestra la compatibilidad de funciones en un ODBC 3. *x* controlador y una aplicación ODBC, y la asignación realizada por el Administrador de controladores cuando se llama a las funciones en un ODBC 3. *x* conductor.  
  
|Función|Compatible<br /><br /> por un<br /><br /> ODBC 3. *x*<br /><br /> ¿Conductor?|Compatible<br /><br /> por un<br /><br /> ODBC 3. *x*<br /><br /> ¿Aplicación?|Asignado/soportado<br /><br /> por el ODBC 3. *x*<br /><br /> Gerente de conductores para<br /><br /> un ODBC 3. *x* conductor?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|No|No[1]|Sí|  
|**SQLAllocEnv**|No|No[1]|Sí|  
|**SQLAllocHandle**|Sí|Sí|No|  
|**SQLAllocStmt**|No|No[1]|Sí|  
|**SQLBindCol**|Sí|Sí|No|  
|**SQLBindParam**|No|Sí[2]|Sí|  
|**SQLBindParameter**|Sí|Sí|No|  
|**SQLBrowseConnect**|Sí|Sí|No|  
|**SQLBulkOperations**|Sí|Sí|No|  
|**SQLCancel**|Sí|Sí|No|  
|**SQLCloseCursor**|Sí|Sí|No|  
|**SQLColAttribute**|Sí|Sí|No|  
|**SQLColAttributes**|No[3]|No|Sí|  
|**SQLColumnPrivileges**|Sí|Sí|No|  
|**SQLColumns**|Sí|Sí|No|  
|**SQLConnect**|Sí|Sí|No|  
|**SQLCopyDesc**|Sí|Sí|Sí[4]|  
|**SQLDataSources**|No|Sí|Sí|  
|**SQLDescribeCol**|Sí|Sí|No|  
|**SQLDescribeParam**|Sí|Sí|No|  
|**SQLDisconnect**|Sí|Sí|No|  
|**SQLDriverConnect**|Sí|Sí|No|  
|**SQLDrivers**|No|Sí|Sí|  
|**SQLEndTran**|Sí|Sí|No|  
|**SQLError**|No|No[1]|Sí|  
|**SQLExecDirect**|Sí|Sí|No|  
|**SQLExecute**|Sí|Sí|No|  
|**SQLExtendedFetch**|Sí|No|No|  
|**SQLFetch**|Sí|Sí|No|  
|**SQLFetchScroll**|Sí|Sí|No|  
|**SQLForeignKeys**|Sí|Sí|No|  
|**SQLFreeConnect**|No|Sí[1]|Sí|  
|**SQLFreeEnv**|No|Sí[1]|Sí|  
|**SQLFreeHandle**|Sí|Sí|No|  
|**SQLFreeStmt**|Sí|Sí|No|  
|**SQLGetConnectAttr**|Sí|Sí|No|  
|**SQLGetConnectOption**|No[5]|No[1]|Sí|  
|**SQLGetCursorName**|Sí|Sí|No|  
|**SQLGetData**|Sí|Sí|No|  
|**SQLGetDescField**|Sí|Sí|No|  
|**SQLGetDescRec**|Sí|Sí|No|  
|**SQLGetDiagField**|Sí|Sí|No|  
|**SQLGetDiagRec**|Sí|Sí|No|  
|**SQLGetEnvAttr**|Sí|Sí|No|  
|**SQLGetFunctions**|No[6]|Sí|Sí|  
|**SQLGetInfo**|Sí|Sí|No|  
|**SQLGetStmtAttr**|Sí|Sí|No|  
|**SQLGetStmtOption**|No[5]|No[1]|Sí|  
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
|**SQLSetConnectOption**|No[5]|No[1]|Sí|  
|**SQLSetCursorName**|Sí|Sí|No|  
|**SQLSetDescField**|Sí|Sí|No|  
|**SQLSetDescRec**|Sí|Sí|No|  
|**SQLSetEnvAttr**|Sí|Sí|No|  
|**SQLSetPos**|Sí|Sí|No|  
|**SQLSetParam**|No|No|Sí|  
|**SQLSetScrollOption**|Sí|Sí|No|  
|**SQLSetStmtAttr**|Sí|Sí|No|  
|**SQLSetStmtOption**|No[5]|No[1]|Sí|  
|**SQLSpecialColumns**|Sí|Sí|No|  
|**SQLStatistics**|Sí|Sí|No|  
|**SQLTablePrivileges**|Sí|Sí|No|  
|**SQLTables**|Sí|Sí|No|  
|**SQLTransact**|No|No[1]|Sí|  
  
 [1] Esta función está en desuso en ODBC 3. *x*. ODBC 3. *x* las aplicaciones no deben utilizar esta función. Sin embargo, una aplicación compatible con Open Group o ISO CLI puede llamar a esta función.  
  
 [2] ODBC 3. *x* las aplicaciones deben usar **SQLBindParameter** en lugar de **SQLBindParam**. Sin embargo, una aplicación compatible con Open Group o ISO CLI puede llamar a esta función.  
  
 [3] Los escritores de controladores deben tener en cuenta que el ODBC 2. *x* los atributos de columna SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE y SQL_COLUMN_LENGTH deben admitirse con **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** se implementa parcialmente por el Administrador de controladores cuando se copia un descriptor entre conexiones que pertenecen a controladores diferentes. Los controladores son necesarios para admitir **SQLCopyDesc** en dos de sus propias conexiones. Funciones como **SQLDrivers**, que se implementan únicamente por el Administrador de controladores, no aparecen en esta lista.  
  
 [5] Bajo ciertas circunstancias, los conductores pueden necesitar apoyar esta función. Para obtener más información, consulte la página de referencia de esta función.  
  
 [6] El controlador puede optar por admitir **SQLGetFunctions** si el conjunto de funciones que admite el controlador varía de una conexión a una conexión.
