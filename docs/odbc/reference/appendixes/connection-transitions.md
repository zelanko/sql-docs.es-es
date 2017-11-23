---
title: "Transiciones de conexión | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3fe5506d1bcaa644ba1a1b60ef06c5fe9b9ac4e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="connection-transitions"></a>Transiciones de conexión
Conexiones ODBC tienen los siguientes estados.  
  
|State|Description|  
|-----------|-----------------|  
|C0|Entorno sin asignar, sin asignar la conexión|  
|C1|Entorno asignada, sin asignar la conexión|  
|C2|Asigna el entorno, asignada la conexión|  
|C3|Función de conexión que necesita datos|  
|C4|Conexión conectado|  
|C5|Conectado conexión, asignada la instrucción|  
|C6|Transacción en curso, si la conexión es conectada. Es posible que una conexión esté en estado C6 con ninguna de las instrucciones asignada en la conexión. Por ejemplo, suponga que la conexión está en modo de confirmación manual y está en estado C4. Si una instrucción asigna, ejecuta (a partir de una transacción) y, a continuación, libera, la transacción permanece activa pero no hay ninguna instrucción en la conexión.|  
  
 Las tablas siguientes muestran cómo cada función ODBC afecta al estado de conexión.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> No hay Env.|C1 sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1 [1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH) [4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] llamada **SQLAllocHandle** con *OutputHandlePtr* que apunta a un identificador válido sobrescribe este identificador sin tener en cuenta el identificador de ofthat contenido anterior y podría causar problemas para los controladores ODBC. Es incorrecta programación de aplicaciones de ODBC para llamar a **SQLAllocHandle** dos veces con la misma variable de aplicación definida para  *\*OutputHandlePtr* sin llamar a  **SQLFreeHandle** para liberar el identificador antes de reasignación de él. Sobrescribir ODBC identificadores de esta manera pueden provocar un comportamiento incoherente o errores por parte de controladores ODBC.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 C3 [d] [s]|--C2 [d] [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--C5 [1] [2]|  
  
 [1] en la conexión estaba en modo de confirmación manual.  
  
 [2] la conexión estaba en modo de confirmación automática.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges y SQLTables  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--C6 [1] [2]|--|  
  
 [1] en la conexión estaba en modo de confirmación automática, o el origen de datos no comenzaron una transacción.  
  
 [2] la conexión estaba en modo de confirmación manual y el origen de datos comenzó una transacción.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField y SQLSetDescRec  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] en este estado, los descriptores solo disponibles para la aplicación se asignan explícitamente descriptores.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources y SQLDrivers  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|S C4: n [f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--[3]|--[3]|--[3]|--|--|: [4] "o" ([5], [6] y [8]) C4 [5] y [7] C5 [5], [6] y [9]|  
|(IH) [2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] porque la conexión no está en estado conectado, no resulta afectada por la transacción.  
  
 [4] la confirmación o reversión error en la conexión. La función devuelve SQL_ERROR en este caso.  
  
 [5] la confirmación o reversión correcta en la conexión. La función devuelve SQL_ERROR si no se pudo confirmar o revertir en otra conexión, o la función devuelve SQL_SUCCESS si la confirmación o reversión se realizó correctamente en todas las conexiones.  
  
 [6] se produjo al menos una instrucción asignada en la conexión.  
  
 [7] no había ninguna de las instrucciones asignada en la conexión.  
  
 [8] la conexión tenía al menos una instrucción para la que se estaba un cursor abierto, y el origen de datos conserva los cursores cuando las transacciones se confirma o revierte, lo que se aplica (dependiendo de si *Sql_commit* era SQL_ CONFIRMACIÓN o SQL_ROLLBACK). Para obtener más información, vea los atributos SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] si la conexión tenía las instrucciones para el que se produjeron cursores abiertos, los cursores no se conservan cuando se confirma o revierte la transacción.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect y SQLExecute  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--C6 C6 [1] [2] [3]|--|  
  
 [1] en la conexión estaba en modo de confirmación automática, y la instrucción ejecutada no era un *cursor* *especificación* (por ejemplo, una instrucción SELECT); o la conexión en modo de confirmación manual y la instrucción ejecuta no comenzaron una transacción.  
  
 [2] la conexión estaba en modo de confirmación automática, y la instrucción ejecutada fue un *cursor* *especificación* (por ejemplo, una instrucción SELECT).  
  
 [3] la conexión estaba en modo de confirmación manual y el origen de datos comenzó una transacción.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|C4 [5]: [6]|--C4 [7] [5] y [8] C5 [6] y [8]|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] se produjo una única instrucción asignada en la conexión.  
  
 [6] hay varias instrucciones asignadas en la conexión.  
  
 [7] la conexión estaba en modo de confirmación manual.  
  
 [8] la conexión estaba en modo de confirmación automática.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|(IH)|(IH)|(IH)|(IH)|--|C5 [3]: [4]|  
|(IH) [2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] esta fila muestra las transacciones cuando la *opción* argumento es SQL_CLOSE.  
  
 [2] esta fila muestra las transacciones cuando la *opción* argumento es SQL_UNBIND o SQL_RESET_PARAMS.  
  
 [3] la conexión estaba en modo de confirmación automática, y que no estaba abiertas en las instrucciones excepto este ningún cursor.  
  
 [4] en la conexión estaba en modo de confirmación manual, o está en modo de confirmación automática y un cursor estaba abierto en al menos un otra instrucción.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--|--|--|  
  
 [1] el *atributo* argumento era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE o hubiera establecido un valor para el atributo de conexión.  
  
 [2] el *atributo* argumento no era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE y no hubiera establecido un valor para la conexión atributo.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField y SQLGetDiagRec  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--|--|--|--|--|--|  
|(IH) [2]|(IH)|--|--|--|--|--|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|08003|--|--|--|  
  
 [1] el *tipo de información* argumento era SQL_ODBC_VER.  
  
 [2] el *tipo de información* argumento no era SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--C6 [1] [2]|--C5 [3] [1]|  
  
 [1] en la conexión estaba en modo de confirmación automática y la llamada a **SQLMoreResults** no se ha inicializado el procesamiento de un conjunto de resultados de una especificación de cursor.  
  
 [2] la conexión estaba en modo de confirmación automática y la llamada a **SQLMoreResults** se ha inicializado el procesamiento de un conjunto de resultados de una especificación de cursor.  
  
 [3] la conexión estaba en modo de confirmación manual.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--C6 [1] [2]|--|  
  
 [1] en la conexión estaba en modo de confirmación automática, o el origen de datos no comenzaron una transacción.  
  
 [2] en la conexión no estaba en modo de confirmación: manual, y el origen de datos comenzó una transacción.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--08002 [3] [4] HY011 [5]|--08002 [3] [4] HY011 [5]|: [3] y [6] C5 [8] 08002 HY011 [4] [5] o [7]|  
  
 [1] el *atributo* argumento no era SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] el *atributo* argumento era SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] el *atributo* argumento no era SQL_ATTR_ODBC_CURSORS o SQL_ATTR_PACKET_SIZE.  
  
 [4] el *atributo* argumento era SQL_ATTR_ODBC_CURSORS.  
  
 [5] el *atributo* argumento era SQL_ATTR_PACKET_SIZE.  
  
 [6] el *atributo* argumento no era SQL_ATTR_AUTOCOMMIT, o la *atributo* argumento era SQL_ATTR_AUTOCOMMIT y establecer este atributo no se confirmaron la transacción.  
  
 [7] el *atributo* argumento era SQL_ATTR_TXN_ISOLATION.  
  
 [8] el *atributo* argumento era SQL_ATTR_AUTOCOMMIT y establecer este atributo confirmó la transacción.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Todas las demás funciones ODBC  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> Asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
