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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45eb427b660496430334633b5d43ee8989211c0f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069752"
---
# <a name="function-conformance"></a>Conformidad de función
En la tabla siguiente se indica el nivel de conformidad de cada función ODBC, donde está bien definido.  
  
|Función|Nivel de cumplimiento|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Core|  
|**SQLBindCol**|Core|  
|**SQLBindParameter**|Núcleo [1]|  
|**SQLBrowseConnect**|Nivel 1|  
|**SQLBulkOperations**|Nivel 1|  
|**SQLCancel**|Núcleo [1]|  
|**SQLCloseCursor**|Core|  
|**SQLColAttribute**|Núcleo [1]|  
|**SQLColumnPrivileges**|Nivel 2|  
|**SQLColumns**|Core|  
|**SQLConnect**|Core|  
|**SQLCopyDesc**|Core|  
|**SQLDataSources**|Core|  
|**SQLDescribeCol**|Núcleo [1]|  
|**SQLDescribeParam**|Nivel 2|  
|**SQLDisconnect**|Core|  
|**SQLDriverConnect**|Core|  
|**SQLDrivers**|Core|  
|**SQLEndTran**|Núcleo [1]|  
|**SQLExecDirect**|Core|  
|**SQLExecute**|Core|  
|**SQLFetch**|Core|  
|**SQLFetchScroll**|Núcleo [1]|  
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
|**SQLSetConnectAttr**|Núcleo [2]|  
|**SQLSetCursorName**|Core|  
|**SQLSetDescField**|Núcleo [1]|  
|**SQLSetDescRec**|Core|  
|**SQLSetEnvAttr**|Núcleo [2]|  
|**SQLSetPos**|Nivel 1 [1]|  
|**SQLSetStmtAttr**|Núcleo [2]|  
|**SQLSpecialColumns**|Núcleo [1]|  
|**SQLStatistics**|Core|  
|**SQLTablePrivileges**|Nivel 2|  
|**SQLTables**|Core|  
  
 [1] las características importantes de esta función solo están disponibles en niveles de cumplimiento superiores.  
  
 [2] establecer ciertos atributos en valores no predeterminados depende del nivel de cumplimiento. Para obtener más información, vea la sección siguiente, [cumplimiento de atributos](../../../odbc/reference/develop-app/attribute-conformance.md).
