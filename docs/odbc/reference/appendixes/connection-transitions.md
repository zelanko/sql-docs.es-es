---
title: Transiciones de conexión (Connection Transitions) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 225f8517a78f8e9d4d765163649da174d72e490c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284775"
---
# <a name="connection-transitions"></a>Transiciones de conexión
Las conexiones ODBC tienen los siguientes estados.  
  
|State|Descripción|  
|-----------|-----------------|  
|C0|Entorno no asignado, conexión no asignada|  
|C1|Entorno asignado, conexión no asignada|  
|C2|Entorno asignado, conexión asignada|  
|C3|La función de conexión necesita datos|  
|C4|Conexión conectada|  
|C5|Conexión conectada, instrucción asignada|  
|C6|Conexión conectada, transacción en curso. Es posible que una conexión esté en el estado C6 sin instrucciones asignadas en la conexión. Por ejemplo, supongamos que la conexión está en modo de confirmación manual y está en el estado C4. Si se asigna una instrucción, se ejecuta (iniciando una transacción) y, a continuación, se libera, la transacción permanece activa, pero no hay instrucciones en la conexión.|  
  
 En las tablas siguientes se muestra cómo afecta cada función ODBC al estado de conexión.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> No Env.|C1 Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1[1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH) [4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC.  
  
 [3] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_STMT.  
  
 [4] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DESC.  
  
 [5] Llamar a **SQLAllocHandle** con *OutputHandlePtr* apuntando a un identificador válido sobrescribe que controla sin tener en cuenta el contenido anterior de ese identificador, y podría causar problemas para los controladores ODBC. Es incorrecto la programación de aplicaciones ODBC para llamar a **SQLAllocHandle** dos veces con la misma variable de aplicación definida para * \*OutputHandlePtr* sin llamar a **SQLFreeHandle** para liberar el identificador antes de reasignarlo. Sobrescribir identificadores ODBC de tal manera puede dar lugar a un comportamiento incoherente o errores por parte de los controladores ODBC.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|-- [d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5[2]|  
  
 [1] La conexión estaba en modo de confirmación manual.  
  
 [2] La conexión estaba en modo de confirmación automática.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges y SQLTables  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] La conexión estaba en modo de confirmación automática, o el origen de datos no comenzó una transacción.  
  
 [2] La conexión estaba en modo de confirmación manual, y la fuente de datos comenzó una transacción.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField y SQLSetDescRec  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] En este estado, los únicos descriptores disponibles para la aplicación son descriptores asignados explícitamente.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources y SQLDrivers  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s -- n[f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--[3]|--[3]|--[3]|--|--|--[4] o ([5], [6] y [8]) C4[5] y [7] C5[5], [6] y [9]|  
|(IH) [2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC.  
  
 [3] Debido a que la conexión no está en un estado conectado, la transacción no se ve afectada.  
  
 [4] Error en la confirmación o reversión en la conexión. La función devuelve SQL_ERROR en este caso.  
  
 [5] La confirmación o reversión se realizó correctamente en la conexión. La función devuelve SQL_ERROR si la confirmación o reversión ha fallado en otra conexión o la función devuelve SQL_SUCCESS si la confirmación o reversión se realizó correctamente en todas las conexiones.  
  
 [6] Había al menos una declaración asignada en la conexión.  
  
 [7] No se asignaron declaraciones sobre la conexión.  
  
 [8] La conexión tenía al menos una instrucción para la que había un cursor abierto, y el origen de datos conserva los cursores cuando se confirman o revierten las transacciones, lo que corresponda (dependiendo de si *CompletionType* se SQL_COMMIT o SQL_ROLLBACK). Para obtener más información, vea los atributos SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] Si la conexión tenía instrucciones para las que había cursores abiertos, los cursores no se conservaban cuando la transacción se confirmó o revirtió.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect y SQLExecute  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2] C6[3]|--|  
  
 [1] La conexión estaba en modo de confirmación automática, y la instrucción ejecutada no era una *especificación* de *cursor* (como una instrucción SELECT); o la conexión estaba en modo de confirmación manual y la instrucción ejecutada no comenzó una transacción.  
  
 [2] La conexión estaba en modo de confirmación automática, y la instrucción ejecutada era una *especificación* de *cursor* (como una instrucción SELECT).  
  
 [3] La conexión estaba en modo de confirmación manual, y la fuente de datos comenzó una transacción.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|C4[5] --[6]|--[7] C4[5] y [8] C5[6] y [8]|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC.  
  
 [3] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_STMT.  
  
 [4] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DESC.  
  
 [5] Sólo había una declaración asignada en la conexión.  
  
 [6] Hubo varias declaraciones asignadas en la conexión.  
  
 [7] La conexión estaba en modo de confirmación manual.  
  
 [8] La conexión estaba en modo de confirmación automática.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|(IH)|(IH)|(IH)|(IH)|--|C5[3] --[4]|  
|(IH) [2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] Esta fila muestra transacciones cuando *el* Option argumento es SQL_CLOSE.  
  
 [2] Esta fila muestra transacciones cuando *el* Option argumento es SQL_UNBIND o SQL_RESET_PARAMS.  
  
 [3] La conexión estaba en modo de confirmación automática, y no había cursores abiertos en ninguna declaración excepto esta.  
  
 [4] La conexión estaba en modo de confirmación manual, o estaba en modo de confirmación automática y un cursor estaba abierto en al menos otra instrucción.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|HY010|--|--|--|  
  
 [1] El argumento *Attribute* era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE, o se había establecido un valor para el atributo connection.  
  
 [2] El argumento *Attribute* no se SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE, y no se había establecido un valor para el atributo connection.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField y SQLGetDiagRec  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--|--|--|--|--|--|  
|(IH) [2]|(IH)|--|--|--|--|--|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC.  
  
 [3] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_STMT.  
  
 [4] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|08003|--|--|--|  
  
 [1] El argumento *InfoType* fue SQL_ODBC_VER.  
  
 [2] El *infoType* argumento no era SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--[3] C5[1]|  
  
 [1] La conexión estaba en modo de confirmación automática, y la llamada a **SQLMoreResults** no ha inicializado el procesamiento de un conjunto de resultados de una especificación de cursor.  
  
 [2] La conexión estaba en modo de confirmación automática, y la llamada a **SQLMoreResults** ha inicializado el procesamiento de un conjunto de resultados de una especificación de cursor.  
  
 [3] La conexión estaba en modo de confirmación manual.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] La conexión estaba en modo de confirmación automática, o el origen de datos no comenzó una transacción.  
  
 [2] La conexión estaba en modo de confirmación manual, y la fuente de datos comenzó una transacción.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|HY010|--[3] 08002[4] HY011[5]|--[3] 08002[4] HY011[5]|--[3] y [6] C5[8] 08002[4] HY011[5] o [7]|  
  
 [1] El argumento *Atributo* no era SQL_ATTR_TRANSLATE_LIB ni SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] El argumento *Atributo* era SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] El argumento *Atributo* no era SQL_ATTR_ODBC_CURSORS ni SQL_ATTR_PACKET_SIZE.  
  
 [4] El argumento *Atributo* fue SQL_ATTR_ODBC_CURSORS.  
  
 [5] El argumento *Atributo* fue SQL_ATTR_PACKET_SIZE.  
  
 [6] El *atributo* argumento no era SQL_ATTR_AUTOCOMMIT, o el *attribute* argumento fue SQL_ATTR_AUTOCOMMIT y establecer este atributo no confirmó la transacción.  
  
 [7] El argumento *Atributo* fue SQL_ATTR_TXN_ISOLATION.  
  
 [8] El *atributo* argumento era SQL_ATTR_AUTOCOMMIT, y al establecer este atributo se confirmó la transacción.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Todas las demás funciones ODBC  
  
|C0<br /><br /> No Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Allocated|C3<br /><br /> Datos de necesidad|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
