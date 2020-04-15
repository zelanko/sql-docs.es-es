---
title: Conformidad de la función ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305596"
---
# <a name="function-conformance"></a>Conformidad de función
La tabla siguiente indica el nivel de conformidad de cada función ODBC, donde está bien definido.  
  
|Función|Nivel de cumplimiento|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Core|  
|**SQLBindCol**|Core|  
|**SQLBindParameter**|Núcleo[1]|  
|**SQLBrowseConnect**|Nivel 1|  
|**SQLBulkOperations**|Nivel 1|  
|**SQLCancel**|Núcleo[1]|  
|**SQLCloseCursor**|Core|  
|**SQLColAttribute**|Núcleo[1]|  
|**SQLColumnPrivileges**|Nivel 2|  
|**SQLColumns**|Core|  
|**SQLConnect**|Core|  
|**SQLCopyDesc**|Core|  
|**SQLDataSources**|Core|  
|**SQLDescribeCol**|Núcleo[1]|  
|**SQLDescribeParam**|Nivel 2|  
|**SQLDisconnect**|Core|  
|**SQLDriverConnect**|Core|  
|**SQLDrivers**|Core|  
|**SQLEndTran**|Núcleo[1]|  
|**SQLExecDirect**|Core|  
|**SQLExecute**|Core|  
|**SQLFetch**|Core|  
|**SQLFetchScroll**|Núcleo[1]|  
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
|**SQLSetConnectAttr**|Núcleo[2]|  
|**SQLSetCursorName**|Core|  
|**SQLSetDescField**|Núcleo[1]|  
|**SQLSetDescRec**|Core|  
|**SQLSetEnvAttr**|Núcleo[2]|  
|**SQLSetPos**|Nivel 1[1]|  
|**SQLSetStmtAttr**|Núcleo[2]|  
|**SQLSpecialColumns**|Núcleo[1]|  
|**SQLStatistics**|Core|  
|**SQLTablePrivileges**|Nivel 2|  
|**SQLTables**|Core|  
  
 [1] Las características significativas de esta función solo están disponibles en niveles de conformidad más altos.  
  
 [2] Establecer ciertos atributos en valores no predeterminados depende del nivel de conformidad. Para obtener más información, consulte la sección siguiente, Conformidad de [atributos](../../../odbc/reference/develop-app/attribute-conformance.md).
