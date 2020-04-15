---
title: Transiciones de la Declaración (Declaración) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55f82e275bfd5bff12544b35a1370cdb31495320
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302856"
---
# <a name="statement-transitions"></a>Transiciones de instrucción
Las instrucciones ODBC tienen los siguientes estados.  
  
|State|Descripción|  
|-----------|-----------------|  
|S0|Instrucción no asignada. (El estado de conexión debe ser C4, C5 o C6. Para obtener más información, consulte [Transiciones](../../../odbc/reference/appendixes/connection-transitions.md)de conexión .)|  
|S1|Instrucción asignada.|  
|S2|Declaración preparada. No se creará ningún conjunto de resultados.|  
|S3|Declaración preparada. Se creará un conjunto de resultados (posiblemente vacío).|  
|S4|Se ha ejecutado la instrucción y no se ha creado ningún conjunto de resultados.|  
|S5|Se ha creado una instrucción ejecutada y un conjunto de resultados (posiblemente vacío). El cursor se abre y se coloca antes de la primera fila del conjunto de resultados.|  
|S6|Cursor situado con **SQLFetch** o **SQLFetchScroll**.|  
|S7|Cursor posicionado con **SQLExtendedFetch**.|  
|S8|La función necesita datos. No se ha llamado a **SQLParamData.**|  
|S9|La función necesita datos. No se ha llamado a **SQLPutData.**|  
|S10|La función necesita datos. **SQLPutData** se ha llamado.|  
|S11|Sigue ejecutándose. Una instrucción se deja en este estado después de que una función que se ejecuta de forma asincrónica devuelve SQL_STILL_EXECUTING. Una instrucción está temporalmente en este estado mientras se ejecuta cualquier función que acepte un identificador de instrucción. La residencia temporal en el estado S11 no se muestra en ninguna tabla de estado excepto en la tabla de estado de **SQLCancel**. Mientras que una instrucción está temporalmente en el estado S11, la función se puede cancelar mediante una llamada a **SQLCancel** desde otro subproceso.|  
|S12|Ejecución asincrónica cancelada. En S12, una aplicación debe llamar a la función cancelada hasta que devuelve un valor distinto de SQL_STILL_EXECUTING. La función se canceló correctamente solo si la función devuelve SQL_ERROR y SQLSTATE HY008 (Operación cancelada). Si devuelve cualquier otro valor, como SQL_SUCCESS, se produce un error en la operación de cancelación y la función se ejecuta normalmente.|  
  
 Los Estados S2 y S3 se conocen como estados preparados, los estados S5 a S7 como estados del cursor, los estados S8 a S10 como los estados de datos de necesidad y los estados S11 y S12 como estados asincrónicos. En cada uno de estos grupos, las transiciones se muestran por separado solo cuando son diferentes para cada estado del grupo; en la mayoría de los casos, las transiciones para cada estado de cada grupo son las mismas.  
  
 En las tablas siguientes se muestra cómo afecta cada función ODBC al estado de la instrucción.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC.  
  
 [3] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_STMT.  
  
 [4] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DESC.  
  
 [5] Llamar a **SQLAllocHandle** con *OutputHandlePtr* apuntando a un identificador válido sobrescribe que controla sin tener en cuenta el contenido anterior a ese identificador y podría causar problemas para los controladores ODBC. Es incorrecto la programación de aplicaciones ODBC para llamar a **SQLAllocHandle** dos veces con la misma variable de aplicación definida para * \*OutputHandlePtr* sin llamar a **SQLFreeHandle** para liberar el identificador antes de reasignarlo. Sobrescribir identificadores ODBC de tal manera podría dar lugar a un comportamiento incoherente o errores por parte de los controladores ODBC.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect, SQLConnect y SQLDriverConnect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|Ver la siguiente tabla|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (Estados del cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-- [s] S8 [d] S11 [x]|-- [s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|S1[1] S2 [nr] y [2] S3 [r] y [2] S5[3] y [5] S6([3] o [4]) y [6] S7[4] y [7]|Ver la siguiente tabla|  
  
 [1] **SQLExecDirect** devolvió SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelto SQL_NEED_DATA.  
  
 [3] **SQLBulkOperations** devolvió SQL_NEED_DATA.  
  
 [4] **SQLSetPos** devolvió SQL_NEED_DATA.  
  
 [5] No se había llamado a **SQLFetch**, **SQLFetchScroll**o **SQLExtendedFetch.**  
  
 [6] **SQLFetch** o **SQLFetchScroll** se había llamado.  
  
 [7] **SQLExtendedFetch** había sido llamado.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (Estados asincrónicos)  
  
|S11<br /><br /> Sigue ejecutándose|S12<br /><br /> Asynch cancelado|  
|-----------------------------|-----------------------------|  
|NS[1] S12[2]|S12|  
  
 [1] La declaración estaba temporalmente en el estado S11 mientras se ejecutaba una función. **SQLCancel** se llamó desde un subproceso diferente.  
  
 [2] La instrucción estaba en el estado S11 porque una función llamada de forma asincrónica devolvió SQL_STILL_EXECUTING.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|Ver la siguiente tabla|24000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (Estados preparados)  
  
|S2<br /><br /> Sin resultados|S3<br /><br /> Results|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-- [s] S11 x|  
  
 [1] *FieldIdentifier* fue SQL_DESC_COUNT.  
  
 [2] *FieldIdentifier* no fue SQL_DESC_COUNT.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges y SQLTables  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] y [1] S5 [s] y [1] S11 [x] y [1] 24000[2]|Ver la siguiente tabla|HY010|NS [c] HY010 o|  
  
 [1] El resultado actual es el último o único resultado, o no hay resultados actuales. Para obtener más información acerca de varios resultados, vea [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] El resultado actual no es el último resultado.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges y SQLTables (Cursor States)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] Este error es devuelto por el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|NS [c] y [3] HY010 [o] o [4]|  
|IH[2]|HY010|Ver la siguiente tabla|24000|-- [s] S11 x|HY010|NS [c] y [3] HY010 [o] o [4]|  
  
 [1] Esta fila muestra transiciones cuando el *SourceDescHandle* argumento era un ARD, APD, o IPD.  
  
 [2] Esta fila muestra transiciones cuando el *SourceDescHandle* argumento era un IRD.  
  
 [3] Los *argumentos SourceDescHandle* y *TargetDescHandle* eran los mismos que en la función **SQLCopyDesc** que se ejecuta de forma asincrónica.  
  
 [4] El *argumento SourceDescHandle* o el argumento *TargetDescHandle* (o ambos) eran diferentes que en la función **SQLCopyDesc** que se ejecuta de forma asincrónica.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (Estados preparados)  
  
|S2<br /><br /> Sin resultados|S3<br /><br /> Results|  
|-----------------------|--------------------|  
|24000[1]|-- [s] S11 [x]|  
  
 [1] Esta fila muestra transiciones cuando el *SourceDescHandle* argumento era un IRD.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources y SQLDrivers  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|Ver la siguiente tabla|24000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (Estados preparados)  
  
|S2<br /><br /> Sin resultados|S3<br /><br /> Results|  
|-----------------------|--------------------|  
|07005|-- [s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0[1]|S0[1]|S0[1]|S0[1]|(HY010)|(HY010)|  
  
 [1] Llamar a **SQLDisconnect** libera todas las instrucciones asociadas a la conexión. Además, esto devuelve el estado de conexión a C2; el estado de conexión debe ser C4 antes de que el estado de la instrucción sea S0.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] o [3] S1[1]|--[[3] S1 [np] y ([1] o [2]) S1 [p] y [1] S2 [p] y [2]|--[[3] S1 [np] y ([1] o [2]) S1 [p] y [1] S3 [p] y [2]|(HY010)|(HY010)|  
  
 [1] El *CompletionType* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_DELETE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o el *CompletionType* argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_DELETE para el SQL_CURSOR_ROLLBACK_BEHAVIOR tipo de información.  
  
 [2] El *CompletionType* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_CLOSE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o el *CompletionType* argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_CLOSE para el tipo de información SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [3] El *CompletionType* argumento es SQL_COMMIT y **SQLGetInfo** devuelve SQL_CB_PRESERVE para el tipo de información SQL_CURSOR_COMMIT_BEHAVIOR, o el *CompletionType* argumento es SQL_ROLLBACK y **SQLGetInfo** devuelve SQL_CB_PRESERVE para el tipo de información SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] y [nr] S5 [s] y [r] S8 [d] S11 [x]|-- [e] y [1] S1 [e] y [2] S4 [s] y [nr] S5 [s] y [r] S8 [d] S11 [x]|-- [e], [1] y [3] S1 [e], [2] y [3] S4 [s], [nr] y [3] S5 [s], [r] y [3] S8 [d] y [3] S11 [x] y [3] 24000 [4]|Ver la siguiente tabla|HY010|NS [c] HY010 [o]|  
  
 [1] El error fue devuelto por el Administrador de controladores.  
  
 [2] El error no fue devuelto por el Administrador de controladores.  
  
 [3] El resultado actual es el último o único resultado, o no hay resultados actuales. Para obtener más información acerca de varios resultados, vea [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] El resultado actual no es el último resultado.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (Estados del cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] Este error es devuelto por el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|Ver la siguiente tabla|S2 [e], p y [1] S4 [s], [p], [nr] y [1] S5 [s], [p], [r] y [1] S8 [d], [p] y [1] S11 [x], [p] y [1] 24000 [p] y [2] HY010 [np]|Ver tabla de estados de cursor|HY010|NS [c] HY010 [o]|  
  
 [1] El resultado actual es el último o único resultado, o no hay resultados actuales. Para obtener más información acerca de varios resultados, vea [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] El resultado actual no es el último resultado.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (Estados preparados)  
  
|S2<br /><br /> Sin resultados|S3<br /><br /> Results|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (Estados del cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p], [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] Este error es devuelto por el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S1010|S1010|24000|Ver la siguiente tabla|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (Estados del cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] o [nf] S11 [x]|S1010|-- [s] o [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch y SQLFetchScroll  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|Ver la siguiente tabla|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch y SQLFetchScroll (estados de cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] o [nf] S11 [x]|-- [s] o [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV o SQL_HANDLE_DBC.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_STMT.  
  
 [3] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DESC y el descriptor se asignó explícitamente.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] Esta fila muestra transiciones cuando *Option* fue SQL_CLOSE.  
  
 [2] Esta fila muestra transiciones cuando *Option* fue SQL_UNBIND o SQL_RESET_PARAMS. Si el *Option* argumento era SQL_DROP y el controlador subyacente es un controlador ODBC 3 *.x,* el Administrador de controladores asigna esto a una llamada a **SQLFreeHandle** con *HandleType* establecido en SQL_HANDLE_STMT. Para obtener más información, vea la tabla de transición para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|Ver la siguiente tabla|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (Estados del cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] o [nf] S11 [x] 24000 [b] HY109 [i]|-- [s] o [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField y SQLGetDescRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|-- [1] o [2] HY010 [3]|Ver la siguiente tabla|-- [1] o [2] 24000 [3]|-- [1], [2] o [3] S11 [3] y [x]|HY010|NS [c] o [4] HY010 [o] y [5]|  
  
 [1] El argumento *DescriptorHandle* era un APD o ARD.  
  
 [2] El argumento *DescriptorHandle* era una IPD.  
  
 [3] El argumento *DescriptorHandle* era un IRD.  
  
 [4] El *DescriptorHandle* argumento era el mismo que el *DescriptorHandle* argumento en el **SQLGetDescField** o **SQLGetDescRec** función que se ejecuta de forma asincrónica.  
  
 [5] El *DescriptorHandle* argumento era diferente de la *DescriptorHandle* argumento en el **SQLGetDescField** o **SQLGetDescRec** función que se ejecuta de forma asincrónica.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField y SQLGetDescRec (Estados preparados)  
  
|S2<br /><br /> Sin resultados|S3<br /><br /> Results|  
|-----------------------|--------------------|  
|--[1], [2] o [3] S11[2] y [x]|--[1], [2] o [3] S11 [x]|  
  
 [1] El argumento *DescriptorHandle* era un APD o ARD.  
  
 [2] El argumento *DescriptorHandle* era una IPD.  
  
 [3] El argumento *DescriptorHandle* era un IRD. Tenga en cuenta que estas funciones siempre devuelven SQL_NO_DATA en el estado S2 cuando *DescriptorHandle* era un IRD.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField y SQLGetDiagRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH[2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_DESC.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_STMT.  
  
 [3] **SQLGetDiagField** siempre devuelve un error en este estado cuando *DiagIdentifier* se SQL_DIAG_ROW_COUNT.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|Ver la siguiente tabla|HY010|HY010|  
  
 [1] El atributo statement no fue SQL_ATTR_ROW_NUMBER.  
  
 [2] El atributo statement se SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (Estados del cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--[1] o ([v] y [2]) 24000 [b] y [2] HY109 [i] y [2]|-- [i] o ([v] y [2]) 24000 [b] y [2] HY109[1] y [2]|  
  
 [1] El argumento *Attribute* no fue SQL_ATTR_ROW_NUMBER.  
  
 [2] El argumento *Atributo* fue SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|-- [s] y [2] S1 [nf], [np] y [4] S2 [nf], [p] y [4] S5 [s] y [3] S11 [x]|S1 [nf], [np] y [4] S3 [nf], [p] y [4] S4 [s] y [2] S5 [s] y [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] La función siempre devuelve SQL_NO_DATA en este estado.  
  
 [2] El siguiente resultado es un recuento de filas.  
  
 [3] El siguiente resultado es un conjunto de resultados.  
  
 [4] El resultado actual es el último resultado.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|Ver la siguiente tabla|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (necesita estados de datos)  
  
|S8<br /><br /> Datos de necesidad|S9<br /><br /> Must Put|S10<br /><br /> Can Put|  
|----------------------|---------------------|---------------------|  
|S1 [e] y [1] S2 [e], [nr] y [2] S3 [e], [r] y [2] S5 [e] y [4] S6 [e] y [5] S7 [e] y [3] S9 [d] S11 [x]|HY010|S1 [e] y [1] S2 [e], [nr] y [2] S3 [e], [r], y [2] S4 [s], [nr], y ([1] o [2]) S5 [s], [r], y ([1] o [2]) S5 ([s] o [e]) y [4] S6 ([s] o [e]) y [5] S7 ([s] o [e]) y [3] S9 [d] S1 [x]|  
  
 [1] **SQLExecDirect** devolvió SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelto SQL_NEED_DATA.  
  
 [3] **SQLSetPos** había sido llamado desde el estado S7 y devuelto SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** había sido llamado desde el estado S5 y devuelto SQL_NEED_DATA.  
  
 [5] **SQLSetPos** o **SQLBulkOperations** se había llamado desde el estado S6 y devuelto SQL_NEED_DATA.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] y [nr] S3 [s] y [r] S11 [x]|-- [s] o ([e] y [1]) S1 [e] y [2] S11 [x]|S1 [e] y [3] S2 [s], [nr] y [3] S3 [s], [r] y [3] S11 [x] y [3] 24000[4]|Ver la siguiente tabla|HY010|NS [c] HY010 [o]|  
  
 [1] La preparación falla por una razón que no sea validar la instrucción (sqlSTATE era HY009 [valor de argumento no válido] o HY090 [Cadena no válida o longitud de búfer]).  
  
 [2] La preparación falla al validar la instrucción (SQLSTATE no era HY009 [Valor de argumento no válido] o HY090 [Cadena no válida o longitud de búfer]).  
  
 [3] El resultado actual es el último o único resultado, o no hay resultados actuales. Para obtener más información acerca de varios resultados, vea [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] El resultado actual no es el último resultado.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (Estados del cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|Ver la siguiente tabla|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (necesita estados de datos)  
  
|S8<br /><br /> Datos de necesidad|S9<br /><br /> Must Put|S10<br /><br /> Can Put|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] y [1] S2 [e], [nr] y [2] S3 [e], [r] y [2] S5 [e] y [4] S6 [e] y [5] S7 [e] y [3] S10 [s] S11 [x]|-- [s] S1 [e] y [1] S2 [e], [nr], y [2] S3 [e], [r] y [2] S5 [e] y [4] S6 [e] y [5] S7 [e] y [3] S11 [x] HY011[6]|  
  
 [1] **SQLExecDirect** devolvió SQL_NEED_DATA.  
  
 [2] **SQLExecute** devuelto SQL_NEED_DATA.  
  
 [3] **SQLSetPos** había sido llamado desde el estado S7 y devuelto SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** había sido llamado desde el estado S5 y devuelto SQL_NEED_DATA.  
  
 [5] **SQLSetPos** o **SQLBulkOperations** se había llamado desde el estado S6 y devuelto SQL_NEED_DATA.  
  
 [6] Una o más llamadas a **SQLPutData** para un único parámetro devuelto SQL_SUCCESS y, a continuación, se realizó una llamada a **SQLPutData** para el mismo parámetro con *StrLen_or_Ind* establecido en SQL_NULL_DATA.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] Esta fila muestra transiciones cuando *Attribute* era un atributo de conexión. Para obtener transiciones cuando *Attribute* era un atributo de instrucción, vea la tabla de transición de instrucción para **SQLSetStmtAttr**.  
  
 [2] El argumento *Atributo* no fue SQL_ATTR_CURRENT_CATALOG.  
  
 [3] El argumento *Atributo* fue SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField y SQLSetDescRec  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|HY010|  
  
 [1] Esta fila muestra transiciones donde el *DescriptorHandle* argumento es un ARD, APD, IPD, o (para **SQLSetDescField**) un IRD cuando el *FieldIdentifier* argumento es SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR. Es un error llamar a **SQLSetDescField** para un IRD cuando *FieldIdentifier* es cualquier otro valor.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|Ver la siguiente tabla|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (Estados del cursor)  
  
|S5<br /><br /> Abierto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> Sin asignar|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> Ejecutado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Datos de necesidad|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--[1] HY011[2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] o [1] HY011 [p] y [2]|HY010 [np] o [1] HY011 [p] y [2]|  
  
 [1] El argumento *Attribute* no era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE ni SQL_ATTR_CURSOR_SENSITIVITY.  
  
 [2] El argumento *Attribute* era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE o SQL_ATTR_CURSOR_SENSITIVITY.
