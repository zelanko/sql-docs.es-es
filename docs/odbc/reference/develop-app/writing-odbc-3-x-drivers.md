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
manager: craigg
ms.openlocfilehash: 77a94c7505b5ab221fee4896e91f9b26850669df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795659"
---
# <a name="writing-odbc-3x-drivers"></a>Controladores ODBC 3.x de escritura
En la tabla siguiente se muestra la compatibilidad de la función en una aplicación ODBC 3. *x* controlador y una aplicación ODBC y la asignación que se realiza mediante el Administrador de controladores cuando se llaman las funciones en una aplicación ODBC 3. *x* controlador.  
  
|Función|Admitida<br /><br /> por un<br /><br /> ODBC 3. *x*<br /><br /> ¿controlador?|Admitida<br /><br /> por un<br /><br /> ODBC 3. *x*<br /><br /> ¿aplicación?|Compatible o asignado<br /><br /> por ODBC 3. *x*<br /><br /> Administrador de controladores para<br /><br /> una aplicación ODBC 3. ¿ *x* controlador?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|no|No hay [1]|Sí|  
|**SQLAllocEnv**|no|No hay [1]|Sí|  
|**SQLAllocHandle**|Sí|Sí|no|  
|**SQLAllocStmt**|no|No hay [1]|Sí|  
|**SQLBindCol**|Sí|Sí|no|  
|**SQLBindParam**|no|Sí [2]|Sí|  
|**SQLBindParameter**|Sí|Sí|no|  
|**SQLBrowseConnect**|Sí|Sí|no|  
|**SQLBulkOperations**|Sí|Sí|no|  
|**SQLCancel**|Sí|Sí|no|  
|**SQLCloseCursor**|Sí|Sí|no|  
|**SQLColAttribute**|Sí|Sí|no|  
|**SQLColAttributes**|No hay [3]|no|Sí|  
|**SQLColumnPrivileges**|Sí|Sí|no|  
|**SQLColumns**|Sí|Sí|no|  
|**SQLConnect**|Sí|Sí|no|  
|**SQLCopyDesc**|Sí|Sí|Sí [4]|  
|**SQLDataSources**|no|Sí|Sí|  
|**SQLDescribeCol**|Sí|Sí|no|  
|**SQLDescribeParam**|Sí|Sí|no|  
|**SQLDisconnect**|Sí|Sí|no|  
|**SQLDriverConnect**|Sí|Sí|no|  
|**SQLDrivers**|no|Sí|Sí|  
|**SQLEndTran**|Sí|Sí|no|  
|**SQLError**|no|No hay [1]|Sí|  
|**SQLExecDirect**|Sí|Sí|no|  
|**SQLExecute**|Sí|Sí|no|  
|**SQLExtendedFetch**|Sí|no|no|  
|**SQLFetch**|Sí|Sí|no|  
|**SQLFetchScroll**|Sí|Sí|no|  
|**SQLForeignKeys**|Sí|Sí|no|  
|**SQLFreeConnect**|no|Sí [1]|Sí|  
|**SQLFreeEnv**|no|Sí [1]|Sí|  
|**SQLFreeHandle**|Sí|Sí|no|  
|**SQLFreeStmt**|Sí|Sí|no|  
|**SQLGetConnectAttr**|Sí|Sí|no|  
|**SQLGetConnectOption**|No hay [5]|No hay [1]|Sí|  
|**SQLGetCursorName**|Sí|Sí|no|  
|**SQLGetData**|Sí|Sí|no|  
|**SQLGetDescField**|Sí|Sí|no|  
|**SQLGetDescRec**|Sí|Sí|no|  
|**SQLGetDiagField**|Sí|Sí|no|  
|**SQLGetDiagRec**|Sí|Sí|no|  
|**SQLGetEnvAttr**|Sí|Sí|no|  
|**SQLGetFunctions**|No hay [6]|Sí|Sí|  
|**SQLGetInfo**|Sí|Sí|no|  
|**SQLGetStmtAttr**|Sí|Sí|no|  
|**SQLGetStmtOption**|No hay [5]|No hay [1]|Sí|  
|**SQLGetTypeInfo**|Sí|Sí|no|  
|**SQLMoreResults**|Sí|Sí|no|  
|**SQLNativeSql**|Sí|Sí|no|  
|**SQLNumParams**|Sí|Sí|no|  
|**SQLNumResultCols**|Sí|Sí|no|  
|**SQLParamData**|Sí|Sí|no|  
|**SQLParamOptions**|no|no|Sí|  
|**SQLPrepare**|Sí|Sí|no|  
|**SQLPrimaryKeys**|Sí|Sí|no|  
|**SQLProcedureColumns**|Sí|Sí|no|  
|**SQLProcedures**|Sí|Sí|no|  
|**SQLPutData**|Sí|Sí|no|  
|**SQLRowCount**|Sí|Sí|no|  
|**SQLSetConnectAttr**|Sí|Sí|no|  
|**SQLSetConnectOption**|No hay [5]|No hay [1]|Sí|  
|**SQLSetCursorName**|Sí|Sí|no|  
|**SQLSetDescField**|Sí|Sí|no|  
|**SQLSetDescRec**|Sí|Sí|no|  
|**SQLSetEnvAttr**|Sí|Sí|no|  
|**SQLSetPos**|Sí|Sí|no|  
|**SQLSetParam**|no|no|Sí|  
|**SQLSetScrollOption**|Sí|Sí|no|  
|**SQLSetStmtAttr**|Sí|Sí|no|  
|**SQLSetStmtOption**|No hay [5]|No hay [1]|Sí|  
|**SQLSpecialColumns**|Sí|Sí|no|  
|**SQLStatistics**|Sí|Sí|no|  
|**SQLTablePrivileges**|Sí|Sí|no|  
|**SQLTables**|Sí|Sí|no|  
|**SQLTransact**|no|No hay [1]|Sí|  
  
 [1] esta función está en desuso en ODBC 3. *x*. ODBC 3. *x* aplicaciones no deben utilizar esta función. Sin embargo, una aplicación compatible con ISO CLI o Open Group puede llamar a esta función.  
  
 [2] ODBC 3. *x* las aplicaciones deben usar **SQLBindParameter** en lugar de **SQLBindParam**. Sin embargo, una aplicación compatible con ISO CLI o Open Group puede llamar a esta función.  
  
 [3] los escritores de controlador deben tener en cuenta que la API ODBC 2. *x* atributos de columna SQL_COLUMN_PRECISION SQL_COLUMN_SCALE y SQL_COLUMN_LENGTH deben ser compatibles con **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** parcialmente se implementa mediante el Administrador de controladores cuando se está copiando un descriptor de a través de conexiones que pertenecen a distintos controladores. Los controladores necesarios para admitir **SQLCopyDesc** entre dos de sus propias conexiones. Las funciones como **SQLDrivers**, que se implementan únicamente por el Administrador de controladores, no se muestran en esta lista.  
  
 [5] en determinadas circunstancias, los controladores que necesite admitir esta función. Para obtener más información, consulte la página de referencia de la función.  
  
 [6], el controlador puede optar por admitir **SQLGetFunctions** si el conjunto de funciones que admite el controlador varía en función de la conexión a la conexión.
