---
title: Función conformidad | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45eb427b660496430334633b5d43ee8989211c0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069752"
---
# <a name="function-conformance"></a>Conformidad de función
En la tabla siguiente indica el nivel de cumplimiento de cada función ODBC, donde esto está bien definido.  
  
|Función|nivel de cumplimiento|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Core|  
|**SQLBindCol**|Core|  
|**SQLBindParameter**|Core [1]|  
|**SQLBrowseConnect**|Nivel 1|  
|**SQLBulkOperations**|Nivel 1|  
|**SQLCancel**|Core [1]|  
|**SQLCloseCursor**|Core|  
|**SQLColAttribute**|Core [1]|  
|**SQLColumnPrivileges**|Nivel 2|  
|**SQLColumns**|Core|  
|**SQLConnect**|Core|  
|**SQLCopyDesc**|Core|  
|**SQLDataSources**|Core|  
|**SQLDescribeCol**|Core [1]|  
|**SQLDescribeParam**|Nivel 2|  
|**SQLDisconnect**|Core|  
|**SQLDriverConnect**|Core|  
|**SQLDrivers**|Core|  
|**SQLEndTran**|Core [1]|  
|**SQLExecDirect**|Core|  
|**SQLExecute**|Core|  
|**SQLFetch**|Core|  
|**SQLFetchScroll**|Core [1]|  
|**SQLForeignKeys**|Nivel 2|  
|**SQLFreeHandle**|Core|  
|**SQLFreeStmt**|Core|  
|**SQLGetConnectAttr**|Core|  
|**SQLGetCursorName**|Core|  
|**SQLGetData**|Core|  
|**SQLGetDescField**|Core|  
|**SQLGetDescRec**|Core|  
|**SQLGetDiagField**|Core|  
|**SQLGetDiagRec**|Core|  
|**SQLGetEnvAttr**|Core|  
|**SQLGetFunctions**|Core|  
|**SQLGetInfo**|Core|  
|**SQLGetStmtAttr**|Core|  
|**SQLGetTypeInfo**|Core|  
|**SQLMoreResults**|Nivel 1|  
|**SQLNativeSql**|Core|  
|**SQLNumParams**|Core|  
|**SQLNumResultCols**|Core|  
|**SQLParamData**|Core|  
|**SQLPrepare**|Core|  
|**SQLPrimaryKeys**|Nivel 1|  
|**SQLProcedureColumns**|Nivel 1|  
|**SQLProcedures**|Nivel 1|  
|**SQLPutData**|Core|  
|**SQLRowCount**|Core|  
|**SQLSetConnectAttr**|Core [2]|  
|**SQLSetCursorName**|Core|  
|**SQLSetDescField**|Core [1]|  
|**SQLSetDescRec**|Core|  
|**SQLSetEnvAttr**|Core [2]|  
|**SQLSetPos**|Nivel 1 [1]|  
|**SQLSetStmtAttr**|Core [2]|  
|**SQLSpecialColumns**|Core [1]|  
|**SQLStatistics**|Core|  
|**SQLTablePrivileges**|Nivel 2|  
|**SQLTables**|Core|  
  
 [1] importantes características de esta función solo están disponibles en niveles más altos de conformidad.  
  
 [2] establecer determinados atributos en valores no predeterminados depende del nivel de cumplimiento. Para obtener más información, consulte la sección siguiente, [conformidad de atributo](../../../odbc/reference/develop-app/attribute-conformance.md).
