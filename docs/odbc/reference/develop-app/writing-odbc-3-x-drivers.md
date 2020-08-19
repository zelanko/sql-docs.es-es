---
description: Controladores ODBC 3.x de escritura
title: Escribiendo controladores ODBC 3. x | Microsoft Docs
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
ms.openlocfilehash: c5fec9b94dbcf60868c44e49d92bddb4bb73e9cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421349"
---
# <a name="writing-odbc-3x-drivers"></a>Controladores ODBC 3.x de escritura
En la tabla siguiente se muestra la compatibilidad con funciones en ODBC 3. controlador *x* y una aplicación ODBC, así como la asignación que realiza el administrador de controladores cuando se llama a las funciones en un ODBC 3. controlador *x* .  
  
|Función|Compatible<br /><br /> por un<br /><br /> ODBC 3. *x*<br /><br /> dispositivo?|Compatible<br /><br /> por un<br /><br /> ODBC 3. *x*<br /><br /> aplicación?|Asignado o compatible<br /><br /> por ODBC 3. *x*<br /><br /> Administrador de controladores para<br /><br /> ODBC 3. ¿controlador *x* ?|  
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
  
 [1] esta función está en desuso en ODBC 3. *x*. ODBC 3. las aplicaciones *x* no deben usar esta función. Sin embargo, un grupo abierto o una aplicación compatible con la CLI ISO puede llamar a esta función.  
  
 [2] ODBC 3. las aplicaciones *x* deben usar **SQLBindParameter** en lugar de **SQLBindParam**. Sin embargo, un grupo abierto o una aplicación compatible con la CLI ISO puede llamar a esta función.  
  
 [3] los escritores de controladores deben tener en cuenta que ODBC 2. los atributos de columna *x* SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE y SQL_COLUMN_LENGTH deben ser compatibles con **SQLColAttribute**.  
  
 [4]   **SQLCopyDesc** se implementa parcialmente por el administrador de controladores cuando se copia un descriptor entre conexiones que pertenecen a controladores diferentes. Los controladores son necesarios para admitir **SQLCopyDesc** en dos de sus propias conexiones. Las funciones como **SQLDrivers**, que se implementan únicamente por el administrador de controladores, no se muestran en esta lista.  
  
 [5] en determinadas circunstancias, es posible que los controladores necesiten admitir esta función. Para obtener más información, vea la página de referencia de esta función.  
  
 [6] el controlador puede optar por admitir **SQLGetFunctions** si el conjunto de funciones que admite el controlador varía de una conexión a una conexión.
