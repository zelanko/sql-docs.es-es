---
title: Referencia de la API de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d56d6068b842256bd450844c7b163727e5d35f3d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653402"
---
# <a name="odbc-api-reference"></a>Referencia de API ODBC
Los temas de esta sección describen cada función ODBC en orden alfabético. Cada función se define como una función de lenguaje de programación de C. Las descripciones siguientes:  
  
-   Finalidad  
  
-   Versión de ODBC  
  
-   Nivel de conformidad con CLI estándar  
  
-   Sintaxis  
  
-   Argumentos  
  
-   Valores devueltos  
  
-   Diagnósticos  
  
-   Comentarios sobre la implementación y uso  
  
-   Ejemplo de código  
  
-   Referencias a otras funciones relacionadas  
  
 El nivel de conformidad con CLI estándar puede ser uno de los siguientes: 92 de ISO, abra el grupo, ODBC, o en desuso. Una función etiquetada como conforme a ISO 92 también aparece en Open Group versión 1, porque Open Group es un superconjunto de ISO 92. Una función etiquetada como grupo conforme abra también aparece en ODBC 3. *x*, ya que ODBC 3. *x* es un superconjunto de la versión 1 de Open Group. Una función que se etiquetan como compatible con ODBC aparece en ninguno estándar. Una función que se etiquetan como en desuso en desuso en ODBC 3. *x*.  
  
 Control de información de diagnóstico se describe en el [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descripción de la función. El texto asociado con los valores de SQLSTATE se incluye para proporcionar una descripción de la condición, pero no está pensado para prescribir un texto específico.  
  
> [!NOTE]  
>  Para obtener información acerca de las funciones ODBC específico del controlador, consulte la sección del controlador.  
  
 Esta sección contiene temas para las funciones siguientes:  
  
-   [Función SQLAllocConnect](../../../odbc/reference/syntax/sqlallocconnect-function.md)  
  
-   [Función SQLAllocEnv](../../../odbc/reference/syntax/sqlallocenv-function.md)  
  
-   [Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [Función SQLAllocStmt](../../../odbc/reference/syntax/sqlallocstmt-function.md)  
  
-   [Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)  
  
-   [Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)  
  
-   [Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
  
-   [Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
  
-   [Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [Función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)  
  
-   [Función SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)  
  
-   [Función SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
  
-   [Función SQLColAttributes](../../../odbc/reference/syntax/sqlcolattributes-function.md)  
  
-   [Función SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
  
-   [Función SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)  
  
-   [Función SQLCompleteAsync](../../../odbc/reference/syntax/sqlcompleteasync-function.md)  
  
-   [Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)  
  
-   [Función SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)  
  
-   [Función SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [Función SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)  
  
-   [Función SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
  
-   [Función SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)  
  
-   [Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
-   [Función SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
-   [Función SQLError](../../../odbc/reference/syntax/sqlerror-function.md)  
  
-   [Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
  
-   [Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)  
  
-   [Función SQLExtendedFetch](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
-   [Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
-   [Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
-   [Función SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
  
-   [Función SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)  
  
-   [Función SQLFreeEnv](../../../odbc/reference/syntax/sqlfreeenv-function.md)  
  
-   [Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
-   [Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)  
  
-   [Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [Función SQLGetConnectOption](../../../odbc/reference/syntax/sqlgetconnectoption-function.md)  
  
-   [Función SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)  
  
-   [Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
-   [Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)  
  
-   [Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)  
  
-   [Función SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [Función SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [Función SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [Función SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
-   [Función SQLGetStmtOption](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)  
  
-   [Función SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
-   [Función SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
  
-   [Función SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
-   [Función SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)  
  
-   [Función SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
  
-   [Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)  
  
-   [Función SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)  
  
-   [Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)  
  
-   [Función SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
  
-   [Función SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [Función SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [Función SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
-   [Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   [Función SQLSetConnectOption](../../../odbc/reference/syntax/sqlsetconnectoption-function.md)  
  
-   [Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)  
  
-   [Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
-   [Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)  
  
-   [Función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)  
  
-   [Función SQLSetParam](../../../odbc/reference/syntax/sqlsetparam-function.md)  
  
-   [Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
-   [Función SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)  
  
-   [Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
-   [Función SQLSetStmtOption](../../../odbc/reference/syntax/sqlsetstmtoption-function.md)  
  
-   [Función SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
  
-   [Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)  
  
-   [Función SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
  
-   [Función SQLTables](../../../odbc/reference/syntax/sqltables-function.md)  
  
-   [Función SQLTransact](../../../odbc/reference/syntax/sqltransact-function.md)
