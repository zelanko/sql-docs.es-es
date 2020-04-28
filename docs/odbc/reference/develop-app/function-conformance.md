---
title: Conformidad de funciones | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33cd0ad4269ed59e31c8ab343ddbb01806afce04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305596"
---
# <a name="function-conformance"></a>Conformidad de función
En la tabla siguiente se indica el nivel de conformidad de cada función ODBC, donde está bien definido.  
  
|Función|Nivel de cumplimiento|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Principal|  
|**SQLBindCol**|Principal|  
|**SQLBindParameter**|Núcleo [1]|  
|**SQLBrowseConnect**|Nivel 1|  
|**SQLBulkOperations**|Nivel 1|  
|**SQLCancel**|Núcleo [1]|  
|**SQLCloseCursor**|Principal|  
|**SQLColAttribute**|Núcleo [1]|  
|**SQLColumnPrivileges**|Nivel 2|  
|**SQLColumns**|Principal|  
|**SQLConnect**|Principal|  
|**SQLCopyDesc**|Principal|  
|**SQLDataSources**|Principal|  
|**SQLDescribeCol**|Núcleo [1]|  
|**SQLDescribeParam**|Nivel 2|  
|**SQLDisconnect**|Principal|  
|**SQLDriverConnect**|Principal|  
|**SQLDrivers**|Principal|  
|**SQLEndTran**|Núcleo [1]|  
|**SQLExecDirect**|Principal|  
|**SQLExecute**|Principal|  
|**SQLFetch**|Principal|  
|**SQLFetchScroll**|Núcleo [1]|  
|**SQLForeignKeys**|Nivel 2|  
|**SQLFreeHandle**|Principal|  
|**SQLFreeStmt**|Principal|  
|**SQLGetConnectAttr**|Principal|  
|**SQLGetCursorName**|Principal|  
|**SQLGetData**|Principal|  
|**SQLGetDescField**|Principal|  
|**SQLGetDescRec**|Principal|  
|**SQLGetDiagField**|Principal|  
|**SQLGetDiagRec**|Principal|  
|**SQLGetEnvAttr**|Principal|  
|**SQLGetFunctions**|Principal|  
|**SQLGetInfo**|Principal|  
|**SQLGetStmtAttr**|Principal|  
|**SQLGetTypeInfo**|Principal|  
|**SQLMoreResults**|Nivel 1|  
|**SQLNativeSql**|Principal|  
|**SQLNumParams**|Principal|  
|**SQLNumResultCols**|Principal|  
|**SQLParamData**|Principal|  
|**SQLPrepare**|Principal|  
|**SQLPrimaryKeys**|Nivel 1|  
|**SQLProcedureColumns**|Nivel 1|  
|**SQLProcedures**|Nivel 1|  
|**SQLPutData**|Principal|  
|**SQLRowCount**|Principal|  
|**SQLSetConnectAttr**|Núcleo [2]|  
|**SQLSetCursorName**|Principal|  
|**SQLSetDescField**|Núcleo [1]|  
|**SQLSetDescRec**|Principal|  
|**SQLSetEnvAttr**|Núcleo [2]|  
|**SQLSetPos**|Nivel 1 [1]|  
|**SQLSetStmtAttr**|Núcleo [2]|  
|**SQLSpecialColumns**|Núcleo [1]|  
|**SQLStatistics**|Principal|  
|**SQLTablePrivileges**|Nivel 2|  
|**SQLTables**|Principal|  
  
 [1] las características importantes de esta función solo están disponibles en niveles de cumplimiento superiores.  
  
 [2] establecer ciertos atributos en valores no predeterminados depende del nivel de cumplimiento. Para obtener más información, vea la sección siguiente, [cumplimiento de atributos](../../../odbc/reference/develop-app/attribute-conformance.md).
