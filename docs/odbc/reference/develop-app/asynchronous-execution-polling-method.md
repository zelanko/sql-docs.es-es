---
title: Ejecución asincrónica (método de sondeo) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca7b3d5fa16be44bf4c2ef8f8df8953ae081235d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293405"
---
# <a name="asynchronous-execution-polling-method"></a>Ejecución asincrónica (método de sondeo)
Antes de ODBC 3.8 y el SDK de Windows 7, las operaciones asincrónicas solo se permitían en funciones de instrucción. Para obtener más información, vea **Ejecutar operaciones**de instrucción de forma asincrónica , más adelante en este tema.  
  
 ODBC 3.8 en el SDK de Windows 7 introdujo la ejecución asincrónica en las operaciones relacionadas con la conexión. Para obtener más información, vea la sección Ejecutar operaciones de conexión de **forma asincrónica,** más adelante en este tema.  
  
 En el SDK de Windows 7, para operaciones de conexión o instrucción asincrónica, una aplicación determinó que la operación asincrónica se completó mediante el método de sondeo. A partir del SDK de Windows 8, puede determinar que una operación asincrónica se completa mediante el método de notificación. Para obtener más información, vea Ejecución asincrónica (método de [notificación).](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)  
  
 De forma predeterminada, los controladores ejecutan funciones ODBC de forma sincrónica; es decir, la aplicación llama a una función y el controlador no devuelve el control a la aplicación hasta que haya terminado de ejecutar la función. Sin embargo, algunas funciones se pueden ejecutar de forma asincrónica; es decir, la aplicación llama a la función y el controlador, después de un procesamiento mínimo, devuelve el control a la aplicación. A continuación, la aplicación puede llamar a otras funciones mientras la primera función todavía se está ejecutando.  
  
 La ejecución asincrónica se admite para la mayoría de las funciones que se ejecutan en gran medida en el origen de datos, como las funciones para establecer conexiones, preparar y ejecutar instrucciones SQL, recuperar metadatos, capturar datos y confirmar transacciones. Es más útil cuando la tarea que se ejecuta en el origen de datos tarda mucho tiempo, como un proceso de inicio de sesión o una consulta compleja en una base de datos grande.  
  
 Cuando la aplicación ejecuta una función con una instrucción o conexión habilitada para el procesamiento asincrónico, el controlador realiza una cantidad mínima de procesamiento (como comprobar argumentos para errores), procesamiento de manos en el origen de datos y devuelve el control a la aplicación con el código de retorno SQL_STILL_EXECUTING. A continuación, la aplicación realiza otras tareas. Para determinar cuándo ha finalizado la función asincrónica, la aplicación sondea el controlador a intervalos regulares llamando a la función con los mismos argumentos que usó originalmente. Si la función sigue ejecutándose, devuelve SQL_STILL_EXECUTING; si ha terminado de ejecutarse, devuelve el código que habría devuelto si se ejecutara sincrónicamente, como SQL_SUCCESS, SQL_ERROR o SQL_NEED_DATA.  
  
 Si una función se ejecuta de forma sincrónica o asincrónica es específico del controlador. Por ejemplo, supongamos que los metadatos del conjunto de resultados se almacenan en caché en el controlador. En este caso, se tarda muy poco tiempo en ejecutar **SQLDescribeCol** y el controlador simplemente debe ejecutar la función en lugar de retrasar artificialmente la ejecución. Por otro lado, si el controlador necesita recuperar los metadatos del origen de datos, debe devolver el control a la aplicación mientras lo hace. Por lo tanto, la aplicación debe ser capaz de controlar un código de retorno distinto de SQL_STILL_EXECUTING cuando se ejecuta por primera vez una función de forma asincrónica.  
  
## <a name="executing-statement-operations-asynchronously"></a>Ejecución de operaciones de extracto de forma asincrónica  
 Las siguientes funciones de instrucción funcionan en un origen de datos y se pueden ejecutar de forma asincrónica:  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 La ejecución de instrucciones asincrónicas se controla por instrucción o por conexión, según el origen de datos. Es decir, la aplicación no especifica que una función determinada se va a ejecutar de forma asincrónica, sino que cualquier función ejecutada en una instrucción determinada se debe ejecutar de forma asincrónica. Para averiguar cuál se admite, una aplicación llama a [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) con una opción de SQL_ASYNC_MODE. SQL_AM_CONNECTION se devuelve si se admite la ejecución asincrónica de nivel de conexión (para un identificador de instrucción); SQL_AM_STATEMENT si se admite la ejecución asincrónica a nivel de instrucción.  
  
 Para especificar que las funciones ejecutadas con una instrucción determinada se deben ejecutar de forma asincrónica, la aplicación llama a **SQLSetStmtAttr** con el atributo SQL_ATTR_ASYNC_ENABLE y lo establece en SQL_ASYNC_ENABLE_ON. Si se admite el procesamiento asincrónico de nivel de conexión, el atributo de instrucción SQL_ATTR_ASYNC_ENABLE es de solo lectura y su valor es el mismo que el atributo de conexión de la conexión en la que se asignó la instrucción. Es específico del controlador si el valor del atributo de instrucción se establece en el momento de la asignación de instrucciones o posterior. Al intentar establecerlo, se devolverán SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada).  
  
 Para especificar que las funciones ejecutadas con una conexión determinada se deben ejecutar de forma asincrónica, la aplicación llama a **SQLSetConnectAttr** con el atributo SQL_ATTR_ASYNC_ENABLE y lo establece en SQL_ASYNC_ENABLE_ON. Todos los identificadores de instrucción futuras asignados en la conexión se habilitarán para la ejecución asincrónica; está definido por el controlador si esta acción habilitará los identificadores de instrucción existentes. Si SQL_ATTR_ASYNC_ENABLE se establece en SQL_ASYNC_ENABLE_OFF, todas las instrucciones de la conexión están en modo sincrónico. Se devuelve un error si la ejecución asincrónica está habilitada mientras hay una instrucción activa en la conexión.  
  
 Para determinar el número máximo de instrucciones simultáneas activas en modo asincrónico que el controlador puede admitir en una conexión determinada, la aplicación llama a **SQLGetInfo** con la opción SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
 El código siguiente muestra cómo funciona el modelo de sondeo:  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 Mientras una función se ejecuta de forma asincrónica, la aplicación puede llamar a funciones en cualquier otra instrucción. La aplicación también puede llamar a funciones en cualquier conexión, excepto la asociada a la instrucción asincrónica. Pero la aplicación solo puede llamar a la función original y a las siguientes funciones (con el identificador de instrucción o su conexión asociada, identificador de entorno), después de que una operación de instrucción devuelve SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (en el identificador de instrucción)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 Si la aplicación llama a cualquier otra función con la instrucción asincrónica o con la conexión asociada a esa instrucción, la función devuelve SQLSTATE HY010 (error de secuencia de funciones), por ejemplo.  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 Cuando una aplicación llama a una función para determinar si todavía se está ejecutando de forma asincrónica, debe usar el identificador de instrucción original. Esto se debe a que se realiza un seguimiento de la ejecución asincrónica por instrucción. La aplicación también debe proporcionar valores válidos para los demás argumentos - los argumentos originales harán - para obtener más allá de la comprobación de errores en el Administrador de controladores. Sin embargo, después de que el controlador comprueba el identificador de instrucción y determina que la instrucción se está ejecutando de forma asincrónica, omite todos los demás argumentos.  
  
 Mientras una función se ejecuta de forma asincrónica, es decir, después de que haya devuelto SQL_STILL_EXECUTING y antes de devolver un código diferente, la aplicación puede cancelarla llamando a **SQLCancel** o **SQLCancelHandle** con el mismo identificador de instrucción. Esto no se garantiza para cancelar la ejecución de la función. Por ejemplo, es posible que la función ya haya finalizado. Además, el código devuelto por **SQLCancel** o **SQLCancelHandle** solo indica si el intento de cancelar la función se realizó correctamente, no si realmente canceló la función. Para determinar si la función se canceló, la aplicación vuelve a llamar a la función. Si se canceló la función, devuelve SQL_ERROR y SQLSTATE HY008 (Operación cancelada). Si la función no se canceló, devuelve otro código, como SQL_SUCCESS, SQL_STILL_EXECUTING o SQL_ERROR con un SQLSTATE diferente.  
  
 Para deshabilitar la ejecución asincrónica de una instrucción determinada cuando el controlador admite el procesamiento asincrónico de nivel de instrucción, la aplicación llama a **SQLSetStmtAttr** con el atributo SQL_ATTR_ASYNC_ENABLE y lo establece en SQL_ASYNC_ENABLE_OFF. Si el controlador admite el procesamiento asincrónico de nivel de conexión, la aplicación llama a **SQLSetConnectAttr** para establecer SQL_ATTR_ASYNC_ENABLE en SQL_ASYNC_ENABLE_OFF, que deshabilita la ejecución asincrónica de todas las instrucciones de la conexión.  
  
 La aplicación debe procesar registros de diagnóstico en el bucle de repetición de la función original. Si **SQLGetDiagField** o **SQLGetDiagRec** se llama cuando se ejecuta una función asincrónica, devolverá la lista actual de registros de diagnóstico. Cada vez que se repite la llamada de función original, borra los registros de diagnóstico anteriores.  
  
## <a name="executing-connection-operations-asynchronously"></a>Ejecución asincrónica de operaciones de conexión  
 Antes de ODBC 3.8, se permitía la ejecución asincrónica para operaciones relacionadas con instrucciones como preparar, ejecutar y capturar, así como para operaciones de metadatos de catálogo. A partir de ODBC 3.8, la ejecución asincrónica también es posible para las operaciones relacionadas con la conexión, como la conexión, desconexión, confirmación y reversión.  
  
 Para obtener más información sobre ODBC 3.8, vea [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 La ejecución asincrónica de operaciones de conexión es útil en los siguientes escenarios:  
  
-   Cuando un pequeño número de subprocesos administra un gran número de dispositivos con velocidades de datos muy altas. Para maximizar la capacidad de respuesta y la escalabilidad, es deseable que todas las operaciones sean asincrónicas.  
  
-   Si desea superponer las operaciones de base de datos en varias conexiones para reducir los tiempos de transferencia transcurridos.  
  
-   Las llamadas ODBC asincrónicas eficaces y la capacidad de cancelar las operaciones de conexión permiten a una aplicación permitir al usuario cancelar cualquier operación lenta sin tener que esperar los tiempos de espera.  
  
 Las siguientes funciones, que funcionan en identificadores de conexión, ahora se pueden ejecutar de forma asincrónica:  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 Para determinar si un controlador admite operaciones asincrónicas en estas funciones, una aplicación llama a **SQLGetInfo** con SQL_ASYNC_DBC_FUNCTIONS. SQL_ASYNC_DBC_CAPABLE se devuelve si se admiten operaciones asincrónicas. SQL_ASYNC_DBC_NOT_CAPABLE se devuelve si no se admiten operaciones asincrónicas.  
  
 Para especificar que las funciones ejecutadas con una conexión determinada se deben ejecutar de forma asincrónica, la aplicación llama a **SQLSetConnectAttr** y establece el atributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE en SQL_ASYNC_DBC_ENABLE_ON. Establecer un atributo de conexión antes de establecer una conexión siempre se ejecuta sincrónicamente. Además, la operación que establece el atributo de conexión SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE con **SQLSetConnectAttr** siempre se ejecuta sincrónicamente.  
  
 Una aplicación puede habilitar la operación asincrónica antes de realizar una conexión. Dado que el Administrador de controladores no puede determinar qué controlador usar antes de realizar una conexión, el Administrador de controladores siempre devolverá el éxito en **SQLSetConnectAttr**. Sin embargo, es posible que no se pueda conectar si el controlador ODBC no admite operaciones asincrónicas.  
  
 En general, puede haber como máximo una función de ejecución asincrónica asociada a un identificador de conexión o identificador de instrucción determinado. Sin embargo, un identificador de conexión puede tener más de un identificador de instrucción asociado. Si no hay ninguna operación asincrónica ejecutándose en el identificador de conexión, un identificador de instrucción asociado puede ejecutar una operación asincrónica. De forma similar, puede tener una operación asincrónica en un identificador de conexión si no hay operaciones asincrónicas en curso en cualquier identificador de instrucción asociado. Un intento de ejecutar una operación asincrónica mediante un identificador que está ejecutando actualmente una operación asincrónica devolverá HY010, "Error de secuencia de funciones".  
  
 Si una operación de conexión devuelve SQL_STILL_EXECUTING, una aplicación solo puede llamar a la función original y a las siguientes funciones para ese identificador de conexión:  
  
-   **SQLCancelHandle** (en el identificador de conexión)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (asignación de ENV/DBC)  
  
-   **SQLAllocHandleStd** (asignación de ENV/DBC)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 La aplicación debe procesar registros de diagnóstico en el bucle de repetición de la función original. Si SQLGetDiagField o SQLGetDiagRec se llama cuando se ejecuta una función asincrónica, devolverá la lista actual de registros de diagnóstico. Cada vez que se repite la llamada de función original, borra los registros de diagnóstico anteriores.  
  
 Si se abre o cierra una conexión de forma asincrónica, la operación se completa cuando la aplicación recibe SQL_SUCCESS o SQL_SUCCESS_WITH_INFO en la llamada de función original.  
  
 Se ha agregado una nueva función a ODBC 3.8, **SQLCancelHandle**. Esta función cancela las seis funciones de conexión (**SQLBrowseConnect**, **SQLConnect**, **SQLDisconnect**, **SQLDriverConnect**, **SQLEndTran**y **SQLSetConnectAttr**). Una aplicación debe llamar a **SQLGetFunctions** para determinar si el controlador admite **SQLCancelHandle**. Al igual que con **SQLCancel**, si **SQLCancelHandle** devuelve el éxito, no significa que se canceló la operación. Una aplicación debe llamar a la función original de nuevo para determinar si se canceló la operación. **SQLCancelHandle** permite cancelar operaciones asincrónicas en identificadores de conexión o identificadores de instrucción. El uso de **SQLCancelHandle** para cancelar una operación en un identificador de instrucción es lo mismo que llamar a **SQLCancel**.  
  
 No es necesario admitir **SQLCancelHandle** y las operaciones de conexión asincrónicas al mismo tiempo. Un controlador puede admitir operaciones de conexión asincrónicas, pero no **SQLCancelHandle**, o viceversa.  
  
 Las operaciones de conexión asincrónicas y **SQLCancelHandle** también se pueden usar en odbc 3.x y ODBC 2.x con un controlador ODBC 3.8 y el Administrador de controladores ODBC 3.8. Para obtener información sobre cómo habilitar una aplicación anterior para usar nuevas características en la versión ODBC posterior, vea Matriz de [compatibilidad](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Agrupar conexiones  
 Siempre que se habilita la agrupación de conexiones, las operaciones asincrónicas solo se admiten mínimamente para establecer una conexión (con **SQLConnect** y **SQLDriverConnect)** y cerrar una conexión con **SQLDisconnect**. Pero una aplicación debe seguir siendo capaz de controlar el valor devuelto de SQL_STILL_EXECUTING de **SQLConnect**, **SQLDriverConnect**y **SQLDisconnect**.  
  
 Cuando se habilita la agrupación de conexiones, **SQLEndTran** y **SQLSetConnectAttr** se admiten para las operaciones asincrónicas.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="description"></a>Descripción  
 En el ejemplo siguiente se muestra cómo utilizar **SQLSetConnectAttr** para habilitar la ejecución asincrónica para funciones relacionadas con la conexión.  
  
### <a name="code"></a>Código  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>Ejemplo  
  
### <a name="description"></a>Descripción  
 En este ejemplo se muestran las operaciones de confirmación asincrónicas. Las operaciones de reversión también se pueden realizar de esta manera.  
  
### <a name="code"></a>Código  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución de instrucciones (ODBC)](../../../odbc/reference/develop-app/executing-statements-odbc.md)
