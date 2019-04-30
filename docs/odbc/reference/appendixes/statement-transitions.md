---
title: Transiciones de instrucción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db8ec0edfa1a5ae1b6b94ed07f63c930bc896f5c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297410"
---
# <a name="statement-transitions"></a>Transiciones de instrucción
Instrucciones de ODBC tienen los siguientes estados.  
  
|State|Descripción|  
|-----------|-----------------|  
|S0|Instrucción sin asignar. (El estado de conexión debe ser C4, C5 o C6. Para obtener más información, consulte [transiciones de conexión](../../../odbc/reference/appendixes/connection-transitions.md).)|  
|S1|Instrucción asignada.|  
|S2|Instrucción preparada. No se creará ningún conjunto de resultados.|  
|S3|Instrucción preparada. Se creará un conjunto de resultados (posiblemente vacía).|  
|S4|Se creó ningún conjunto de resultados y de instrucción ejecutada.|  
|S5|Se creó un conjunto de resultados (posiblemente vacía) y de instrucción ejecutada. El cursor está abierta y colocada delante de la primera fila del conjunto de resultados.|  
|S6|Cursor colocado con **SQLFetch** o **SQLFetchScroll**.|  
|S7|Cursor colocado con **SQLExtendedFetch**.|  
|S8|Función necesita que los datos. **SQLParamData** no se ha llamado.|  
|S9|Función necesita que los datos. **SQLPutData** no se ha llamado.|  
|S10|Función necesita que los datos. **SQLPutData** se ha llamado.|  
|S11|Todavía está ejecutando. Una instrucción se deja en este estado después de una función que se ejecuta de forma asincrónica devuelve SQL_STILL_EXECUTING. Una instrucción está temporalmente en este estado mientras cualquier función que acepta que un identificador de instrucción se está ejecutando. Residencia temporal en estado no se muestra en las tablas de estado, excepto la tabla de estado para S11 **SQLCancel**. Mientras una instrucción está en estado S11 temporalmente, la función puede cancelarse mediante una llamada a **SQLCancel** desde otro subproceso.|  
|S12|Se canceló la ejecución asincrónica. En S12, una aplicación debe llamar a la función cancelada hasta que devuelve un valor distinto de SQL_STILL_EXECUTING. La función se canceló correctamente sólo si la función devuelve SQL_ERROR y SQLSTATE HY008 (operación cancelada). Si devuelve cualquier otro valor, como SQL_SUCCESS, la operación de cancelación no se pudo y la función que se ejecuta con normalidad.|  
  
 Estados S2 y S3 se conocen como los Estados preparados, Estados S5 mediante S7 mientras el cursor Estados, Estados S8 mediante S10 como los Estados de datos necesario y Estados S11 y S12 como los Estados asincrónicos. En cada uno de estos grupos, las transiciones sólo se muestran por separado cuando son diferentes para cada estado en el grupo; en la mayoría de los casos, las transiciones para cada estado en cada uno un grupo son los mismos.  
  
 Las tablas siguientes muestran cómo afecta cada función ODBC al estado de la instrucción.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] llamada **SQLAllocHandle** con *OutputHandlePtr* que apunta a un identificador válido sobrescribe dicho identificador sin tener en cuenta para el contenido anterior para que controle y podría causar problemas para los controladores ODBC. Es incorrecta programación de aplicaciones de ODBC para llamar a **SQLAllocHandle** dos veces con la misma variable de aplicación definida para  *\*OutputHandlePtr* sin llamar a  **SQLFreeHandle** para liberar el identificador antes de reasignación de él. Sobrescribir ODBC controla de manera podría provocar un comportamiento incoherente o errores por parte de los controladores ODBC.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect, SQLConnect y SQLDriverConnect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Consulte la tabla siguiente|HY010|E/s de HY010 NS [c]|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-- [s] S8 [d] S11 [x]|-- [s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|S1 S2 [1] [n] y [2] S3 [r] y S5 [2] [3] y [5] S6 ([3] o [4]) y S7 [6] [4] y [7]|Consulte la tabla siguiente|  
  
 [1] **SQLExecDirect** devuelve SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelve SQL_NEED_DATA.  
  
 [3] **SQLBulkOperations** devuelve SQL_NEED_DATA.  
  
 [4] **SQLSetPos** devuelve SQL_NEED_DATA.  
  
 [5] **SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch** no se había llamado.  
  
 [6] **SQLFetch** o **SQLFetchScroll** hubiera llamado.  
  
 [7] **SQLExtendedFetch** hubiera llamado.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (Estados asincrónicos)  
  
|S11<br /><br /> Todavía está ejecutando|S12<br /><br /> Asincrónico se canceló|  
|-----------------------------|-----------------------------|  
|NS[1] S12[2]|S12|  
  
 [1] en la instrucción se estaba temporalmente en estado S11 mientras se estaba ejecutando una función. **SQLCancel** se ha llamado desde un subproceso diferente.  
  
 [2] en la instrucción se estaba en estado S11 porque una función que llama de forma asincrónica devuelve SQL_STILL_EXECUTING.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|Consulte la tabla siguiente|24000|-- [s] S11 [x]|HY010|E/s de HY010 NS [c]|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-- [s] S11 x|  
  
 [1] *FieldIdentifier* era SQL_DESC_COUNT.  
  
 [2] *FieldIdentifier* no era SQL_DESC_COUNT.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges, and SQLTables  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s]  S11 [x]|S1 [e] S5 [s]  S11 [x]|S1 [e] y [1] S5 [s] y [1] S11 [x] y [1] 24000 [2]|Consulte la tabla siguiente|HY010|E/s de HY010 NS [c]|  
  
 [1], el resultado actual es el último o el resultado solo o no hay ningún resultado actual. Para obtener más información acerca de varios resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2], el resultado actual no es el último resultado.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges y SQLTables (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|NS [c] y [3] HY010 [o] o [4]|  
|IH[2]|HY010|Consulte la tabla siguiente|24000|-- [s]  S11 x|HY010|NS [c] y [3] HY010 [o] o [4]|  
  
 [1] esta fila muestra las transiciones cuando el *SourceDescHandle* argumento era un descartar, APD o IPD.  
  
 [2] esta fila muestra las transiciones cuando el *SourceDescHandle* argumento era un IRD.  
  
 [3] el *SourceDescHandle* y *TargetDescHandle* argumentos eran el mismo que en el **SQLCopyDesc** función que se está ejecutando de forma asincrónica.  
  
 [4], ya sea el *SourceDescHandle* argumento o la *TargetDescHandle* argumento (o ambos) eran diferentes que en el **SQLCopyDesc** función que se está ejecutando de forma asincrónica.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|24000[1]|-- [s]  S11 [x]|  
  
 [1] Esta fila muestra las transiciones cuando el *SourceDescHandle* argumento era un IRD.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources y SQLDrivers  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|Consulte la tabla siguiente|24000|-- [s]  S11 [x]|HY010|E/s de HY010 NS [c]|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|07005|-- [s]  S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-- [s]  S11 [x]|HY010|HY010|HY010|HY010 NS [c] [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0[1]|S0[1]|S0[1]|S0[1]|(HY010)|(HY010)|  
  
 [1] llamada **SQLDisconnect** libera todas las instrucciones asociadas con la conexión. Además, esto devuelve el estado de conexión a C2; el estado de conexión debe ser C4 antes de que el estado de la instrucción es S0.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|: [2] o [3] S1 [1]|--S1 [3] [np] y ([1] o [2]) S1 [p] y S2 [1] [p] y [2]|--S1 [3] [np] y ([1] o [2]) S1 [p] y S3 [1] [p] y [2]|(HY010)|(HY010)|  
  
 [1] el *Sql_commit* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_DELETE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o el *Sql_commit*argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_DELETE para el tipo de información SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [2] el *Sql_commit* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_CLOSE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o el *Sql_commit*argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_CLOSE para el tipo de información SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [3] el *Sql_commit* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_PRESERVE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o el *Sql_commit*argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_PRESERVE para el tipo de información SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] y [nr] S5 [s] y [r] [d] S8 S11 [x]|--S1 [1] [e] y [2] S4 [s] y [nr] S5 [e] y [s] y [r] [d] S8 S11 [x]|--[e], [1] y [3] S1 [e], [2] y [3] S4 [s], [nr,] y [3] S5 [s], [r], S8 [3] [d] y [3] S11 [x] y [3] 24000 [4]|Consulte la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
 [1], el error fue devuelto por el Administrador de controladores.  
  
 [2], el error no ha devuelto por el Administrador de controladores.  
  
 [3], el resultado actual es el último o el resultado solo o no hay ningún resultado actual. Para obtener más información acerca de varios resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4], el resultado actual no es el último resultado.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o  **SQLFetchScroll** devuelva SQL_NO_DATA.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|Consulte la tabla siguiente|S2 [e], p y S4 [1] [s], [p], [nr,] y [1] S5 [s], [p], [r] y S8 [d] [p], [1] y [1] S11 [x], [p] y [1] 24000 [p] y [2] HY010 [SP]|Consulte la tabla de Estados de cursor|HY010|HY010 NS [c] [o]|  
  
 [1], el resultado actual es el último o el resultado solo o no hay ningún resultado actual. Para obtener más información acerca de varios resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2], el resultado actual no es el último resultado.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|S4 [s]  S8 [d]  S11 [x]|S5 [s]  S8 [d]  S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p]  HY010 [np]|24000 [p], [1] HY010 [SP]|24000 [p]  HY010 [np]|  
  
 [1] este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o  **SQLFetchScroll** devuelva SQL_NO_DATA.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|S1010|S1010|24000|Consulte la tabla siguiente|S1010|S1010 NS [c] [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] o [nf] S11 [x]|S1010|--[s] o [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch y SQLFetchScroll  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Consulte la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch y SQLFetchScroll (Estados Cursor)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] o [nf] S11 [x]|--[s] o [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV o SQL_HANDLE_DBC.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC y el descriptor se ha asignado explícitamente.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np]  S2 [p]|S1 [np]  S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] esta fila muestra las transiciones cuando *opción* era SQL_CLOSE.  
  
 [2] esta fila muestra las transiciones cuando *opción* era SQL_UNBIND o SQL_RESET_PARAMS. Si el *opción* argumento era SQL_DROP y el controlador subyacente es una aplicación ODBC 3 *.x* controlador, el Administrador de controladores se asigna a una llamada a **SQLFreeHandle** con  *HandleType* establecido en SQL_HANDLE_STMT. Para obtener más información, consulte la tabla de transición para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Consulte la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] o [nf] S11 [24000 [b] HY109 x] [i]|--[s] o [nf] S11 [24000 [b] HY109 x] [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField y SQLGetDescRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] o HY010 [2] [3]|Consulte la tabla siguiente|--[1] o 24000 [2] [3]|--[1], [2], o S11 [3] [3] y [x]|HY010|NS [c] o [4] HY010 [o] y [5]|  
  
 [1] el *DescriptorHandle* argumento era un APD o descartar.  
  
 [2] el *DescriptorHandle* argumento era un IPD.  
  
 [3] el *DescriptorHandle* argumento era un IRD.  
  
 [4] el *DescriptorHandle* argumento era el mismo que el *DescriptorHandle* argumento en el **SQLGetDescField** o **SQLGetDescRec** función que se está ejecutando de forma asincrónica.  
  
 [5] el *DescriptorHandle* argumento era diferente a la *DescriptorHandle* argumento en el **SQLGetDescField** o **SQLGetDescRec**función que se está ejecutando de forma asincrónica.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField y SQLGetDescRec (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|--[1], [2] o [3] S11 [2] y [x]|--[1], [2] o [3] S11 [x]|  
  
 [1] el *DescriptorHandle* argumento era un APD o descartar.  
  
 [2] el *DescriptorHandle* argumento era un IPD.  
  
 [3] el *DescriptorHandle* argumento era un IRD. Tenga en cuenta que estas funciones siempre devuelven SQL_NO_DATA en estado S2 cuando *DescriptorHandle* era un IRD.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField y SQLGetDiagRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH[2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_DESC.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [3] **SQLGetDiagField** siempre devuelve un error en este estado cuando *DiagIdentifier* es SQL_DIAG_ROW_COUNT.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|Consulte la tabla siguiente|HY010|HY010|  
  
 [1], el atributo de instrucción no era SQL_ATTR_ROW_NUMBER.  
  
 [2], el atributo de instrucción era SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--[1] "o" ([v] y [2]) 24000 [b] y [2] HY109 [i] y [2]|--[i] o ([v] y [2]) 24000 [b] y [2] HY109 [1] y [2]|  
  
 [1] el *atributo* argumento no era SQL_ATTR_ROW_NUMBER.  
  
 [2] el *atributo* argumento era SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|--[s] y [2] S1 [nf], [SP] y S2 [4] [nf], [p] y S5 [4] [s] y [3] S11 [x]|S1 [nf], [SP] y S3 [4] [nf], [p] y [4] S4 [s] y [2] S5 [s] y [3] S11 [x]|HY010|HY010 NS [c] [o]|  
  
 [1] la función siempre devuelve SQL_NO_DATA en este estado.  
  
 [2], el resultado siguiente es un recuento de filas.  
  
 [3], el resultado siguiente es un conjunto de resultados.  
  
 [4], el resultado actual es el último resultado.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-- [s]  S11 [x]|-- [s]  S11 [x]|-- [s]  S11 [x]|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-- [s]  S11 [x]|-- [s]  S11 [x]|-- [s]  S11 [x]|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|Consulte la tabla siguiente|HY010 NS [c] [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (necesidad de Estados de datos)  
  
|S8<br /><br /> Necesita los datos|S9<br /><br /> Debe colocar|S10<br /><br /> Puede colocar|  
|----------------------|---------------------|---------------------|  
|S1 [e] y S2 [1] [e], [nr] y S3 [2] [e], [r] y S5 [2] [e] y [4] S6 [e] y [5] S7 [e] y [3] S9 [d] S11 [x]|HY010|S1 [e] y S2 [1] [e], [n] y S3 de [2] [e] [r] y [2] S4 [s], [n], y ([1] o [2]) S5 [s], [r] y ([1] o [2]) S5 ([s] o [e]) y S6 [4]\([s] o [e]) y [5] S7 ([s] o [e]) y S9 [3] [d] S11 [x]|  
  
 [1] **SQLExecDirect** devuelve SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelve SQL_NEED_DATA.  
  
 [3] **SQLSetPos** se ha llamado desde estado S7 y devuelve SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** se ha llamado desde estado S5 y devuelve SQL_NEED_DATA.  
  
 [5] **SQLSetPos** o **SQLBulkOperations** se ha llamado desde estado S6 y devuelve SQL_NEED_DATA.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] y [nr] S3 [s] y [r] S11 [x]|--[s] o ([e] y [1]) S1 [e] y [2] S11 [x]|S1 [e] y [3] S2 [s], [nr,] y [3] S3 [s], [r] y [3] S11 [x] y [3] 24000 [4]|Consulte la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
 [1] en la preparación falla por alguna razón distinta de la validación de la instrucción (el valor de SQLSTATE era HY009 [valor de argumento no válido] o HY090 [longitud de búfer o cadena no válida]).  
  
 [2] en la preparación produce un error al validar la instrucción (el valor de SQLSTATE no era HY009 [valor de argumento no válido] o HY090 [longitud de búfer o cadena no válida]).  
  
 [3], el resultado actual es el último o el resultado solo o no hay ningún resultado actual. Para obtener más información acerca de varios resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4], el resultado actual no es el último resultado.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|Consulte la tabla siguiente|HY010 NS [c] [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (necesidad de Estados de datos)  
  
|S8<br /><br /> Necesita los datos|S9<br /><br /> Debe colocar|S10<br /><br /> Puede colocar|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] y S2 [1] [e], [n] y S3 [2] [e], [r] y S5 [2] [e] y [4] S6 [e] y [5] S7 [e] y [3] S10 S11 [s] [x]|--S1 [s] [e] y S2 [1] [e], [n] y S3 [2] [e], [r] y S5 [2] [e] y [4] S6 [e] y [5] S7 [e] y [3] S11 [x] HY011 [6]|  
  
 [1] **SQLExecDirect** devuelve SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelve SQL_NEED_DATA.  
  
 [3] **SQLSetPos** se ha llamado desde estado S7 y devuelve SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** se ha llamado desde estado S5 y devuelve SQL_NEED_DATA.  
  
 [5] **SQLSetPos** o **SQLBulkOperations** se ha llamado desde estado S6 y devuelve SQL_NEED_DATA.  
  
 [6] uno o más llamadas a **SQLPutData** para un único parámetro devuelve SQL_SUCCESS y, a continuación, una llamada a **SQLPutData** se realizó para el mismo parámetro con *StrLen_or_Ind* establecido en SQL_NULL_DATA.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] esta fila muestra las transiciones cuando *atributo* era un atributo de conexión. Para transiciones cuando *atributo* era una instrucción de atributo, vea la tabla de transiciones de instrucción para **SQLSetStmtAttr**.  
  
 [2] el *atributo* argumento no era SQL_ATTR_CURRENT_CATALOG.  
  
 [3] el *atributo* argumento era SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField y SQLSetDescRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|HY010|  
  
 [1] esta fila muestra las transiciones donde el *DescriptorHandle* argumento es un descartar, APD, IPD, o (para **SQLSetDescField**) un IRD cuando la *FieldIdentifier* argumento es SQL_ DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR. Es un error llamar a **SQLSetDescField** para un IRD cuando *FieldIdentifier* es cualquier otro valor.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Consulte la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (Cursor estados)  
  
|S5<br /><br /> Puede abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s]  S8 [d]  S11 [x]  24000 [b]  HY109 [i]|-- [s]  S8 [d]  S11 [x]  24000 [b]  HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> asignado|S2-S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Necesita los datos|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--[1] HY011[2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] o [1] HY011 [p] y [2]|HY010 [np] o [1] HY011 [p] y [2]|  
  
 [1] el *atributo* argumento no era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE y SQL_ATTR_CURSOR_SENSITIVITY.  
  
 [2] el *atributo* argumento era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE y SQL_ATTR_CURSOR_SENSITIVITY.
