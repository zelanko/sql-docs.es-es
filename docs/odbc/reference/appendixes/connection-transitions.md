---
title: Transiciones de conexión | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f808460a1421a9ab4cb3a76c2810d810b9636b11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224504"
---
# <a name="connection-transitions"></a>Transiciones de conexión
Las conexiones de ODBC tienen los siguientes estados.  
  
|State|Descripción|  
|-----------|-----------------|  
|C0|Entorno sin asignar, sin asignar la conexión|  
|C1|Entorno asignado, sin asignar la conexión|  
|C2|Asigna el entorno, asignada la conexión|  
|C3|Función de conexión necesita datos|  
|C4|Conexión conectado|  
|C5|Conectado la conexión, asignada la instrucción|  
|C6|Conexión conectado, la transacción en curso. Es posible que una conexión a estar en estado C6 con ninguna de las instrucciones asignada en la conexión. Por ejemplo, suponga que la conexión está en modo de confirmación manual y está en estado C4. Si una instrucción asigna, ejecuta (a partir de una transacción) y, a continuación, se libera, la transacción permanece activa pero no hay ninguna instrucción en la conexión.|  
  
 Las tablas siguientes muestran cómo cada función ODBC afecta al estado de conexión.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> No hay Env.|C1 sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1[1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH)[4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] llamada **SQLAllocHandle** con *OutputHandlePtr* apuntando a un identificador válido sobrescribe dicho identificador sin tener en cuenta el identificador de ofthat contenido anterior y podría causar problemas para los controladores ODBC. Es incorrecta programación de aplicaciones de ODBC para llamar a **SQLAllocHandle** dos veces con la misma variable de aplicación definida para  *\*OutputHandlePtr* sin llamar a  **SQLFreeHandle** para liberar el identificador antes de reasignación de él. Sobrescribir ODBC controla de manera puede provocar un comportamiento incoherente o errores por parte de los controladores ODBC.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|-- [d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5[2]|  
  
 [1] en la conexión estaba en modo de confirmación manual.  
  
 [2] en la conexión estaba en modo de confirmación automática.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges, and SQLTables  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] en la conexión estaba en modo de confirmación automática, o el origen de datos no ha iniciado una transacción.  
  
 [2] en la conexión estaba en modo de confirmación manual, y el origen de datos comenzó una transacción.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField y SQLSetDescRec  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] en este estado, los descriptores solo disponibles para la aplicación se asignan explícitamente descriptores.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources y SQLDrivers  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s -- n[f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--[3]|--[3]|--[3]|--|--|: [4] o ([5], [6] y [8]) C4 [5] y [7] C5 [5], [6] y [9]|  
|(IH)[2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] porque la conexión no está en estado conectado, se ve afectado por la transacción.  
  
 [4] en la confirmación o reversión error en la conexión. La función devuelve SQL_ERROR en este caso.  
  
 [5] la confirmación o reversión correcta en la conexión. La función devuelve SQL_ERROR si no se pudo confirmar o revertir en otra conexión o la función devuelve SQL_SUCCESS si la confirmación o reversión se realizó correctamente en todas las conexiones.  
  
 [6] se produjo al menos una instrucción asignada en la conexión.  
  
 [7] se han producido ninguna de las instrucciones asignada en la conexión.  
  
 [8] la conexión tenía al menos una instrucción para el que existe era un cursor abierto, y el origen de datos conserva los cursores cuando las transacciones se confirman o se revierte, lo que corresponda (dependiendo de si *Sql_commit* fue SQL_ CONFIRMACIÓN o SQL_ROLLBACK). Para obtener más información, vea los atributos SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] si la conexión tenía las instrucciones para el que se produjeron los cursores abiertos, los cursores no se conservan cuando la transacción se ha confirmado o revertido.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect y SQLExecute  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2] C6[3]|--|  
  
 [1] en la conexión estaba en modo de confirmación automática y la instrucción ejecutada no era un *cursor* *especificación* (por ejemplo, una instrucción SELECT); o la conexión estaba en modo de confirmación manual y la instrucción ejecutar no se ha iniciado una transacción.  
  
 [2] en la conexión estaba en modo de confirmación automática y la instrucción ejecutada fue un *cursor* *especificación* (por ejemplo, una instrucción SELECT).  
  
 [3] en la conexión estaba en modo de confirmación manual, y el origen de datos comenzó una transacción.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|C4[5] --[6]|--C4 [7] [5] y [8] C5 [6] y [8]|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] se ha producido una única instrucción asignada en la conexión.  
  
 [6] había varias instrucciones asignadas en la conexión.  
  
 [7] la conexión estaba en modo de confirmación manual.  
  
 [8] la conexión estaba en modo de confirmación automática.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|(IH)|(IH)|(IH)|(IH)|--|C5[3] --[4]|  
|(IH)[2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] esta fila muestra las transacciones cuando la *opción* argumento es SQL_CLOSE.  
  
 [2] esta fila muestra las transacciones cuando la *opción* argumento es SQL_UNBIND o SQL_RESET_PARAMS.  
  
 [3] en la conexión estaba en modo de confirmación automática y no hay cursores estaban abiertos en las instrucciones excepto este.  
  
 [4] en la conexión estaba en modo de confirmación manual, o estaba en modo de confirmación automática y un cursor estaba abierto en al menos un otra instrucción.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--|--|--|  
  
 [1] el *atributo* argumento era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE o se haya establecido un valor para el atributo de conexión.  
  
 [2] el *atributo* argumento no era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE y no se haya establecido un valor para la conexión atributo.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField y SQLGetDiagRec  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--|--|--|--|--|--|  
|(IH)[2]|(IH)|--|--|--|--|--|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|08003|--|--|--|  
  
 [1] el *InfoType* argumento era SQL_ODBC_VER.  
  
 [2] el *InfoType* argumento no era SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--[3] C5[1]|  
  
 [1] en la conexión estaba en modo de confirmación automática y la llamada a **SQLMoreResults** no se ha inicializado el procesamiento de un conjunto de resultados de una especificación de cursor.  
  
 [2] en la conexión estaba en modo de confirmación automática y la llamada a **SQLMoreResults** se ha inicializado el procesamiento de un conjunto de resultados de una especificación de cursor.  
  
 [3] en la conexión estaba en modo de confirmación manual.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] en la conexión estaba en modo de confirmación automática, o el origen de datos no ha iniciado una transacción.  
  
 [2] en la conexión estaba en modo de confirmación manual, y el origen de datos comenzó una transacción.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--[3] 08002[4] HY011[5]|--[3] 08002[4] HY011[5]|: [3] y [6] C5 [8] 08002 HY011 [4] [5] o [7]|  
  
 [1] el *atributo* argumento no era SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] el *atributo* argumento era SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] el *atributo* argumento no era SQL_ATTR_ODBC_CURSORS o SQL_ATTR_PACKET_SIZE.  
  
 [4] el *atributo* argumento era SQL_ATTR_ODBC_CURSORS.  
  
 [5] el *atributo* argumento era SQL_ATTR_PACKET_SIZE.  
  
 [6] el *atributo* argumento no era SQL_ATTR_AUTOCOMMIT, o la *atributo* argumento era SQL_ATTR_AUTOCOMMIT y establecer este atributo no se confirmaron la transacción.  
  
 [7] el *atributo* argumento era SQL_ATTR_TXN_ISOLATION.  
  
 [8] el *atributo* argumento era SQL_ATTR_AUTOCOMMIT y establecer este atributo confirma la transacción.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Todas las demás funciones ODBC  
  
|C0<br /><br /> No hay Env.|C1<br /><br /> Sin asignar|C2<br /><br /> asignado|C3<br /><br /> Necesita los datos|C4<br /><br /> Conectado|C5<br /><br /> .|C6<br /><br /> Transacción|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
