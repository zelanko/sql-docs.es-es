---
title: Transiciones de instrucción | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94696a2975436669567db926b3d66020dd29ab5b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="statement-transitions"></a>Transiciones de instrucción
Instrucciones de ODBC tienen los siguientes estados.  
  
|State|Description|  
|-----------|-----------------|  
|S0|Instrucción sin asignar. (El estado de conexión debe ser C4, C5 o C6. Para obtener más información, consulte [conexión transiciones](../../../odbc/reference/appendixes/connection-transitions.md).)|  
|S1|Instrucción asignado.|  
|S2|Instrucción preparada. No se creará ningún conjunto de resultados.|  
|S3|Instrucción preparada. Se creará un conjunto de resultados (posiblemente vacía).|  
|S4|Instrucción que ejecuta y ningún conjunto de resultados que se creó.|  
|S5|Se creó un conjunto de resultados (posiblemente vacía) y de instrucción ejecutada. El cursor está abierta y colocada antes de la primera fila del conjunto de resultados.|  
|S6|Cursor situado con **SQLFetch** o **SQLFetchScroll**.|  
|S7|Cursor situado con **SQLExtendedFetch**.|  
|S8|Función necesita que los datos. **SQLParamData** no se ha llamado.|  
|S9|Función necesita que los datos. **SQLPutData** no se ha llamado.|  
|S10|Función necesita que los datos. **SQLPutData** se ha llamado.|  
|S11|Todavía está ejecutando. Una instrucción se deja en este estado después de una función que se ejecuta de forma asincrónica devuelve SQL_STILL_EXECUTING. Una instrucción está temporalmente en este estado mientras cualquier función que acepta que un identificador de instrucción se está ejecutando. Residencia temporal en estado S11 no se muestra en las tablas de estado, excepto la tabla de estado para **SQLCancel**. Mientras una instrucción está temporalmente en estado S11, la función puede cancelarse mediante una llamada a **SQLCancel** desde otro subproceso.|  
|S12|Se canceló la ejecución asincrónica. En S12, una aplicación debe llamar a la función cancelada hasta que devuelve un valor distinto de SQL_STILL_EXECUTING. La función se canceló correctamente sólo si la función devuelve SQL_ERROR y SQLSTATE HY008 (operación cancelada). Si devuelve cualquier otro valor, como SQL_SUCCESS, error en la operación de cancelación y la función que se ejecuta normalmente.|  
  
 Estados S2 y S3 se conocen como los Estados preparados, Estados S5 mediante S7 como el cursor Estados, Estados S8 mediante S10 como los Estados de datos necesario y Estados S11 y S12 como los Estados asincrónicos. En cada uno de estos grupos, las transiciones sólo se muestran por separado cuando son diferentes para cada estado en el grupo; en la mayoría de los casos, las transiciones para cada estado en cada uno un grupo son los mismos.  
  
 Las tablas siguientes muestran cómo cada función ODBC afecta al estado de la instrucción.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] llamada **SQLAllocHandle** con *OutputHandlePtr* que apunta a un identificador válido sobrescribe este identificador sin tener en cuenta para el contenido anterior para que controle y podría causar problemas para los controladores ODBC. Es incorrecta programación de aplicaciones de ODBC para llamar a **SQLAllocHandle** dos veces con la misma variable de aplicación definida para  *\*OutputHandlePtr* sin llamar a  **SQLFreeHandle** para liberar el identificador antes de reasignación de él. Sobrescribir ODBC controla de manera podría provocar un comportamiento incoherente o errores por parte de controladores ODBC.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect, SQLConnect y SQLDriverConnect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Vea la tabla siguiente|HY010|O de HY010 NS [c]|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--S8 [s] [d] S11 [x]|--S8 [s] [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|S1 S2 [1] [n] y [2] S3 [r] y S5 [2] [3] y [5] S6 ([3] o [4]) y S7 [6] [4] y [7]|Vea la tabla siguiente|  
  
 [1] **SQLExecDirect** devuelve SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelve SQL_NEED_DATA.  
  
 [3] **SQLBulkOperations** devuelve SQL_NEED_DATA.  
  
 [4] **SQLSetPos** devuelve SQL_NEED_DATA.  
  
 [5] **SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch** si no se hubiese llamado.  
  
 [6] **SQLFetch** o **SQLFetchScroll** si se hubiese llamado.  
  
 [7] **SQLExtendedFetch** si se hubiese llamado.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (asincrónicos estados)  
  
|S11<br /><br /> Todavía está ejecutando|S12<br /><br /> Asincrónico cancelado|  
|-----------------------------|-----------------------------|  
|S12 NS [1] [2]|S12|  
  
 [1] la instrucción estaba temporalmente en estado S11 mientras se estaba ejecutando una función. **SQLCancel** se ha llamado desde un subproceso diferente.  
  
 [2] la instrucción estaba en estado S11 porque una función que llama de forma asincrónica devuelve SQL_STILL_EXECUTING.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|24000|24000|24000|S1 S3 [np] [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|Vea la tabla siguiente|24000|--S11 [s] [x]|HY010|O de HY010 NS [c]|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|--[1] 07005[2]|--[s] S11 x|  
  
 [1] *FieldIdentifier* era SQL_DESC_COUNT.  
  
 [2] *FieldIdentifier* no era SQL_DESC_COUNT.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges y SQLTables  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 S5 [e] [s] S11 [x]|S1 [e] y [1] S5 [s] y [1] S11 [x] y [1] 24000 [2]|Vea la tabla siguiente|HY010|O de HY010 NS [c]|  
  
 [1], el resultado actual es la última o un solo resultado o sin resultados actual. Para obtener más información acerca de varios resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2], el resultado actual no es el último resultado.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges y SQLTables (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|NS [c] y [3] HY010 [o] o [4]|  
|IH [2]|HY010|Vea la tabla siguiente|24000|--[s] S11 x|HY010|NS [c] y [3] HY010 [o] o [4]|  
  
 [1] esta fila muestra las transiciones cuando la *SourceDescHandle* argumento era un descartar, APD o IPD.  
  
 [2] esta fila muestra las transiciones cuando la *SourceDescHandle* argumento era un IRD.  
  
 [3] el *SourceDescHandle* y *TargetDescHandle* argumentos fueran los mismos que en el **SQLCopyDesc** función que se ejecuta de forma asincrónica.  
  
 [4] o el *SourceDescHandle* argumento o el *TargetDescHandle* argumento (o ambos) son diferentes que en el **SQLCopyDesc** función que se está ejecutando de forma asincrónica.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|24000[1]|--S11 [s] [x]|  
  
 [1] Esta fila muestra las transiciones cuando la *SourceDescHandle* argumento era un IRD.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources y SQLDrivers  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|Vea la tabla siguiente|24000|--S11 [s] [x]|HY010|O de HY010 NS [c]|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|07005|--S11 [s] [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--S11 [s] [x]|HY010|HY010|HY010|HY010 NS [c] [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|(HY010)|(HY010)|  
  
 [1] llamada **SQLDisconnect** libera todas las instrucciones asociadas con la conexión. Además, se devuelve el estado de conexión a C2; el estado de conexión debe ser C4 antes de que el estado de la instrucción es S0.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|: [2] o [3] S1 [1]|--S1 [3] [np] y ([1] o [2]) S1 [p] y [1] S2 [p] y [2]|--S1 [3] [np] y ([1] o [2]) S1 [p] y [1] S3 [p] y [2]|(HY010)|(HY010)|  
  
 [1] el *Sql_commit* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_DELETE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o la *Sql_commit*argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_DELETE para el tipo de información de SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [2] el *Sql_commit* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_CLOSE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o la *Sql_commit*argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_CLOSE para el tipo de información de SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [3] el *Sql_commit* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_PRESERVE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o la *Sql_commit*argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_PRESERVE para el tipo de información de SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] y [n] S5 [s] y [r] [d] S8 S11 [x]|--[e] y [1] S1 [e] y [2] S4 [s] y [n] S5 [s] y [r] [d] S8 S11 [x]|--[e], [1] y [3] S1 [e], [2] y S4 [3] [s], [n] y [3] S5 [s] [r] y S8 [3] [d] y [3] S11 [x] y [3] 24000 [4]|Vea la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
 [1], el error fue devuelto por el Administrador de controladores.  
  
 [2], el error no ha devuelto por el Administrador de controladores.  
  
 [3], el resultado actual es la última o un solo resultado o sin resultados actual. Para obtener más información acerca de varios resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4], el resultado actual no es el último resultado.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y se devuelve el controlador si **SQLFetch** o  **SQLFetchScroll** devuelva SQL_NO_DATA.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|Vea la tabla siguiente|S2 [e], p y S4 [1] [s] [p], [n] y [1] S5 [s], [p] [r] y S8 [d] [p] [1] y [1] S11 [x], [p] y [1] 24000 [p] y [2] HY010 [np]|Vea la tabla de Estados de cursor|HY010|HY010 NS [c] [o]|  
  
 [1], el resultado actual es la última o un solo resultado o sin resultados actual. Para obtener más información acerca de varios resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2], el resultado actual no es el último resultado.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|S4 [s] [d] S8 S11 [x]|S5 [s] [d] S8 S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 HY010 [p] [np]|24000 [p], [1] HY010 [np]|24000 HY010 [p] [np]|  
  
 [1] este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y se devuelve el controlador si **SQLFetch** o  **SQLFetchScroll** devuelva SQL_NO_DATA.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|S1010|S1010|24000|Vea la tabla siguiente|S1010|S1010 NS [c] [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] o [nf] S11 [x]|S1010|--[s] o [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch y SQLFetchScroll  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Vea la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch y SQLFetchScroll (Estados de Cursor)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] o [nf] S11 [x]|--[s] o [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV o SQL_HANDLE_DBC.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* se SQL_HANDLE_DESC y se asigna explícitamente el descriptor.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 S2 [np] [p]|S1 S3 [np] [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] esta fila muestra las transiciones cuando *opción* era SQL_CLOSE.  
  
 [2] esta fila muestra las transiciones cuando *opción* era SQL_UNBIND o SQL_RESET_PARAMS. Si el *opción* argumento era SQL_DROP y el controlador subyacente es una aplicación ODBC 3 *.x* controlador, el Administrador de controladores se asigna a una llamada a **SQLFreeHandle** con  *HandleType* establecido en SQL_HANDLE_STMT. Para obtener más información, consulte la tabla de transición para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Vea la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] o [nf] S11 [24000 [b] HY109 x] [i]|--[s] o [nf] S11 [24000 [b] HY109 x] [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField y SQLGetDescRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] o HY010 [2] [3]|Vea la tabla siguiente|--[1] o 24000 [2] [3]|--[1], [2], o S11 [3] [3] y [x]|HY010|NS [c] o [4] HY010 [o] y [5]|  
  
 [1] el *DescriptorHandle* argumento era un APD o descartar.  
  
 [2] el *DescriptorHandle* argumento era un IPD.  
  
 [3] el *DescriptorHandle* argumento era un IRD.  
  
 [4] el *DescriptorHandle* argumento era el mismo que el *DescriptorHandle* argumento en el **SQLGetDescField** o **SQLGetDescRec** función que se ejecuta de forma asincrónica.  
  
 [5] el *DescriptorHandle* argumento es diferente de la *DescriptorHandle* argumento en el **SQLGetDescField** o **SQLGetDescRec**función que se ejecuta de forma asincrónica.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField y SQLGetDescRec (preparados estados)  
  
|S2<br /><br /> No hay resultados|S3<br /><br /> Resultado|  
|-----------------------|--------------------|  
|--[1], [2] o [3] S11 [2] y [x]|--[1], [2] o [3] S11 [x]|  
  
 [1] el *DescriptorHandle* argumento era un APD o descartar.  
  
 [2] el *DescriptorHandle* argumento era un IPD.  
  
 [3] el *DescriptorHandle* argumento era un IRD. Tenga en cuenta que estas funciones siempre devuelven SQL_NO_DATA en estado S2 cuando *DescriptorHandle* era un IRD.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField y SQLGetDiagRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_DESC.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [3] **SQLGetDiagField** siempre devuelve un error en este estado cuando *DiagIdentifier* es SQL_DIAG_ROW_COUNT.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|Vea la tabla siguiente|HY010|HY010|  
  
 [1], el atributo de instrucción no era SQL_ATTR_ROW_NUMBER.  
  
 [2], el atributo de instrucción era SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--[1] "o" ([v] y [2]) 24000 [b] y [2] HY109 [i] y [2]|--[i] "o" ([v] y [2]) 24000 [b] y [2] HY109 [1] y [2]|  
  
 [1] el *atributo* argumento no era SQL_ATTR_ROW_NUMBER.  
  
 [2] el *atributo* argumento era SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|--[s] y [2] S1 [nf], [np] y [4] S2 [nf] [p] y [4] S5 [s] y [3] S11 [x]|S1 [nf], [np] y [4] S3 [nf] [p] y [4] S4 [s] y [2] S5 [s] y [3] S11 [x]|HY010|HY010 NS [c] [o]|  
  
 [1] la función siempre devuelve SQL_NO_DATA en este estado.  
  
 [2], el resultado siguiente es un recuento de filas.  
  
 [3], el resultado siguiente es un conjunto de resultados.  
  
 [4], el resultado actual es el último resultado.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--S11 [s] [x]|--S11 [s] [x]|--S11 [s] [x]|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--S11 [s] [x]|--S11 [s] [x]|--S11 [s] [x]|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|Vea la tabla siguiente|HY010 NS [c] [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (necesidad de Estados de datos)  
  
|S8<br /><br /> Necesita los datos|S9<br /><br /> Debe colocar|S10<br /><br /> Puede colocar|  
|----------------------|---------------------|---------------------|  
|S1 [e] y [1] S2 [e], [n] y S3 de [2] [e], [r] y [2] S5 [e] y [4] S6 [e] y [5] S7 [e] y S9 [3] [d] S11 [x]|HY010|S1 [e] y S2 [1] [e], [n] y S3 de [2] [e] [r] y [2] S4 [s], [n], y ([1] o [2]) S5 [s], [r] y ([1] o [2]) S5 ([s] o [e]) y S6 [4]\([s] o [e]) y [5] S7 ([s] o [e]) y S9 [3] [d] S11 [x]|  
  
 [1] **SQLExecDirect** devuelve SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelve SQL_NEED_DATA.  
  
 [3] **SQLSetPos** se ha llamado desde estado S7 y devuelve SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** se ha llamado desde estado S5 y devuelve SQL_NEED_DATA.  
  
 [5] **SQLSetPos** o **SQLBulkOperations** se ha llamado desde estado S6 y devuelve SQL_NEED_DATA.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] y [n] S3 [s] y [r] S11 [x]|--[s] "o" ([e] y [1]) S1 [e] y [2] S11 [x]|S1 [e] y [3] S2 [s], [n] y [3] S3 [s] [r] y [3] S11 [x] y [3] 24000 [4]|Vea la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
 [1] la preparación produce un error por alguna razón distinta de la validación de la instrucción (el valor de SQLSTATE era HY009 [valor de argumento no válido] o HY090 [longitud de búfer o cadena no válida]).  
  
 [2] la preparación produce un error al validar la instrucción (el valor de SQLSTATE no era HY009 [valor de argumento no válido] o HY090 [longitud de búfer o cadena no válida]).  
  
 [3], el resultado actual es la última o un solo resultado o sin resultados actual. Para obtener más información acerca de varios resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4], el resultado actual no es el último resultado.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|Vea la tabla siguiente|HY010 NS [c] [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (necesidad de Estados de datos)  
  
|S8<br /><br /> Necesita los datos|S9<br /><br /> Debe colocar|S10<br /><br /> Puede colocar|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] y S2 [1] [e], [n] y S3 de [2] [e], [r] y [2] S5 [e] y [4] S6 [e] y [5] S7 [e] y [3] S10 [s] S11 [x]|--S1 [s] [e] y [1] S2 [e], [n] y S3 de [2] [e] [r] y [2] S5 [e] y [4] S6 [e] y [5] S7 [e] y HY011 S11 [3] [x] [6]|  
  
 [1] **SQLExecDirect** devuelve SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelve SQL_NEED_DATA.  
  
 [3] **SQLSetPos** se ha llamado desde estado S7 y devuelve SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** se ha llamado desde estado S5 y devuelve SQL_NEED_DATA.  
  
 [5] **SQLSetPos** o **SQLBulkOperations** se ha llamado desde estado S6 y devuelve SQL_NEED_DATA.  
  
 [6] uno o más llamadas a **SQLPutData** para un único parámetro devuelve SQL_SUCCESS y, a continuación, una llamada a **SQLPutData** se creó para el mismo parámetro con *StrLen_or_Ind* establecer en SQL_NULL_DATA.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] esta fila muestra las transiciones cuando *atributo* era un atributo de conexión. Para realiza la transición cuando *atributo* fue un atributo, vea la tabla de transiciones de instrucción para **SQLSetStmtAttr**.  
  
 [2] el *atributo* argumento no era SQL_ATTR_CURRENT_CATALOG.  
  
 [3] el *atributo* argumento era SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField y SQLSetDescRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|HY010|  
  
 [1] esta fila muestra las transiciones donde la *DescriptorHandle* argumento es un descartar, APD, IPD, o (para **SQLSetDescField**) un IRD cuando la *FieldIdentifier* argumento es SQL_ DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR. Es un error al llamar a **SQLSetDescField** para un IRD cuando *FieldIdentifier* es cualquier otro valor.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Vea la tabla siguiente|HY010|HY010 NS [c] [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (Cursor estados)  
  
|S5<br /><br /> Abrir|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] [d] S8 S11 [24000 [b] HY109 x] [i]|--[s] [d] S8 S11 [24000 [b] HY109 x] [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Asignado|S2, S3<br /><br /> Prepared|S4<br /><br /> ejecuta|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Necesita los datos|S11: S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--HY011 [1] [2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] o HY011 [1] [p] y [2]|HY010 [np] o HY011 [1] [p] y [2]|  
  
 [1] el *atributo* argumento no era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE y SQL_ATTR_CURSOR_SENSITIVITY.  
  
 [2] el *atributo* argumento era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE y SQL_ATTR_CURSOR_SENSITIVITY.
