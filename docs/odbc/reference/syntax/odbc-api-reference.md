---
title: Referencia de la API de ODBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: abb5aebcd58c79c6351d7c47a7b98be5a040ef46
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-api-reference"></a>Referencia de la API de ODBC
Los temas de esta sección describen cada función ODBC en orden alfabético. Cada función se define como una función del lenguaje de programación de C. Las descripciones siguientes:  
  
-   Finalidad  
  
-   Versión de ODBC  
  
-   Nivel de conformidad de CLI estándar  
  
-   Sintaxis  
  
-   Argumentos  
  
-   Valores devueltos  
  
-   Diagnósticos  
  
-   Comentarios acerca del uso y la implementación  
  
-   Ejemplo de código  
  
-   Referencias a funciones relacionadas  
  
 El nivel de conformidad de CLI estándar puede ser uno de los siguientes: 92 ISO, Open Group, ODBC o en desuso. Una función de etiquetado como compatible con ISO 92 también aparece en Open Group versión 1, como Open Group es un superconjunto puro de ISO 92. Una función que se etiquetan como grupo conforme abra también aparece en ODBC 3. *x*, ya que ODBC 3.* x* es un superconjunto de Open Group versión 1. Una función que se etiquetan como compatible con ODBC aparece en ningún estándar. Una función de etiquetado como en desuso está en desuso en ODBC 3. *x*.  
  
 Control de información de diagnóstico se describe en el [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descripción de la función. El texto asociado a los valores de SQLSTATE se incluye para proporcionar una descripción de la condición, pero no está diseñado para prescribir un texto específico.  
  
> [!NOTE]  
>  Para obtener información acerca de las funciones ODBC específicos del controlador, vea la sección del controlador.  
  
 Esta sección contiene temas para las funciones siguientes:  
  
-   [SQLAllocConnect (función)](../../../odbc/reference/syntax/sqlallocconnect-function.md)  
  
-   [SQLAllocEnv (función)](../../../odbc/reference/syntax/sqlallocenv-function.md)  
  
-   [SQLAllocHandle, función](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLAllocStmt (función)](../../../odbc/reference/syntax/sqlallocstmt-function.md)  
  
-   [SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)  
  
-   [SQLBindParameter, función](../../../odbc/reference/syntax/sqlbindparameter-function.md)  
  
-   [SQLBrowseConnect, función](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
  
-   [Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
  
-   [SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle (función)](../../../odbc/reference/syntax/sqlcancelhandle-function.md)  
  
-   [SQLCloseCursor, función](../../../odbc/reference/syntax/sqlclosecursor-function.md)  
  
-   [Función SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
  
-   [SQLColAttributes (función)](../../../odbc/reference/syntax/sqlcolattributes-function.md)  
  
-   [Sqlcolumnprivileges, función](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
  
-   [SQLColumns, función](../../../odbc/reference/syntax/sqlcolumns-function.md)  
  
-   [SQLCompleteAsync (función)](../../../odbc/reference/syntax/sqlcompleteasync-function.md)  
  
-   [SQLConnect, función](../../../odbc/reference/syntax/sqlconnect-function.md)  
  
-   [SQLCopyDesc (función)](../../../odbc/reference/syntax/sqlcopydesc-function.md)  
  
-   [SQLDataSources (función)](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDescribeCol (función)](../../../odbc/reference/syntax/sqldescribecol-function.md)  
  
-   [SQLDescribeParam, función](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
  
-   [SQLDisconnect, función](../../../odbc/reference/syntax/sqldisconnect-function.md)  
  
-   [SQLDriverConnect, función](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
-   [Sqldrivers, función](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
-   [Función SQLError](../../../odbc/reference/syntax/sqlerror-function.md)  
  
-   [SQLExecDirect, función](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
  
-   [SQLExecute, función](../../../odbc/reference/syntax/sqlexecute-function.md)  
  
-   [Función SQLExtendedFetch](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
-   [SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
-   [SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
-   [SQLForeignKeys, función](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
  
-   [SQLFreeConnect (función)](../../../odbc/reference/syntax/sqlfreeconnect-function.md)  
  
-   [SQLFreeEnv (función)](../../../odbc/reference/syntax/sqlfreeenv-function.md)  
  
-   [SQLFreeHandle, función](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
-   [SQLFreeStmt, función](../../../odbc/reference/syntax/sqlfreestmt-function.md)  
  
-   [Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLGetConnectOption (función)](../../../odbc/reference/syntax/sqlgetconnectoption-function.md)  
  
-   [Función SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)  
  
-   [SQLGetData, función](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
-   [Sqlgetdescfield, función](../../../odbc/reference/syntax/sqlgetdescfield-function.md)  
  
-   [Sqlgetdescrec, función](../../../odbc/reference/syntax/sqlgetdescrec-function.md)  
  
-   [SQLGetDiagField, función](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec, función](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLGetEnvAttr (función)](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetFunctions, función](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetStmtAttr, función](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
-   [SQLGetStmtOption (función)](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)  
  
-   [SQLGetTypeInfo, función](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
-   [SQLMoreResults (función)](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
  
-   [SQLNativeSql, función](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
-   [Función SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)  
  
-   [SQLNumResultCols (función)](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
  
-   [SQLParamData, función](../../../odbc/reference/syntax/sqlparamdata-function.md)  
  
-   [Función SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)  
  
-   [Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)  
  
-   [SQLPrimaryKeys, función](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
  
-   [SQLProcedureColumns, función](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [SQLProcedures, función](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [SQLPutData, función](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [SQLRowCount, función](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
-   [SQLSetConnectAttr, función](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   [SQLSetConnectOption (función)](../../../odbc/reference/syntax/sqlsetconnectoption-function.md)  
  
-   [SQLSetCursorName, función](../../../odbc/reference/syntax/sqlsetcursorname-function.md)  
  
-   [Sqlsetdescfield, función](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
-   [Sqlsetdescrec, función](../../../odbc/reference/syntax/sqlsetdescrec-function.md)  
  
-   [SQLSetEnvAttr, función](../../../odbc/reference/syntax/sqlsetenvattr-function.md)  
  
-   [SQLSetParam (función)](../../../odbc/reference/syntax/sqlsetparam-function.md)  
  
-   [SQLSetPos, función](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
-   [SQLSetScrollOptions (función)](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)  
  
-   [SQLSetStmtAttr, función](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
-   [Función SQLSetStmtOption](../../../odbc/reference/syntax/sqlsetstmtoption-function.md)  
  
-   [SQLSpecialColumns, función](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
  
-   [Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)  
  
-   [SQLTablePrivileges, función](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
  
-   [SQLTables, función](../../../odbc/reference/syntax/sqltables-function.md)  
  
-   [SQLTransact (función)](../../../odbc/reference/syntax/sqltransact-function.md)
