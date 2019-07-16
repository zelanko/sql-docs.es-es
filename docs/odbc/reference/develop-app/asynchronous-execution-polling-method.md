---
title: Ejecución asincrónica (método de sondeo) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97fe8af6f02e9797bc14578edda09c420f8f94e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077047"
---
# <a name="asynchronous-execution-polling-method"></a>Ejecución asincrónica (método de sondeo)
Antes de ODBC 3.8 y el SDK de Windows 7, las operaciones asincrónicas se permiten solo en las funciones de la instrucción. Para obtener más información, consulte el **ejecutar operaciones de instrucción de forma asincrónica**, más adelante en este tema.  
  
 ODBC 3.8 en el SDK de Windows 7 presentó la ejecución asincrónica en operaciones relacionadas con la conexión. Para obtener más información, consulte el **ejecutar operaciones de conexión de forma asincrónica** sección más adelante en este tema.  
  
 En el SDK de Windows 7, para la instrucción asincrónica o las operaciones de conexión, una aplicación determinó que la operación asincrónica se completa mediante el método de sondeo. A partir de Windows 8 SDK, puede determinar que una operación asincrónica está completa mediante el método de notificación. Para obtener más información, consulte [ejecución asincrónica (método de notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
 De forma predeterminada, los controladores ejecutan funciones ODBC sincrónicamente; es decir, la aplicación llama a una función y el controlador no devuelve el control a la aplicación hasta que haya terminado de ejecutar la función. Sin embargo, algunas funciones se pueden ejecutar de forma asincrónica; es decir, la aplicación llama a la función, y el controlador, después del procesamiento mínimo, devuelve el control a la aplicación. La aplicación, a continuación, puede llamar a otras funciones mientras la primera función todavía se está ejecutando.  
  
 Se admite la ejecución asincrónica para la mayoría de las funciones que se ejecuta en gran medida en el origen de datos, como las funciones para establecer conexiones, preparar y ejecutar instrucciones SQL, recuperar los metadatos, capturar datos y confirmar las transacciones. Es muy útil cuando la tarea que se está ejecutada en el origen de datos tarda mucho tiempo, por ejemplo, un proceso de inicio de sesión o una consulta compleja en una base de datos grande.  
  
 Cuando la aplicación ejecuta una función con una instrucción o la conexión que está habilitada para el procesamiento asincrónico, el controlador realiza una cantidad mínima de procesamiento (como argumentos para los errores de comprobación), entrega el procesamiento para el origen de datos y devuelve el control a la aplicación con el código de retorno en SQL_STILL_EXECUTING. A continuación, la aplicación realiza otras tareas. Para determinar cuándo ha finalizado la función asincrónica, la aplicación sondea el controlador a intervalos regulares mediante una llamada a la función con los mismos argumentos que se usó originalmente. Si la función todavía se está ejecutando, devuelve SQL_STILL_EXECUTING; Si ha terminado de ejecutarse, devuelve el código que se habría devuelto tenía ejecutan sincrónicamente, como SQL_SUCCESS, SQL_ERROR o SQL_NEED_DATA.  
  
 Si se ejecuta una función de forma sincrónica o asincrónica es específico del controlador. Por ejemplo, supongamos que se almacena en caché los metadatos del conjunto de resultados en el controlador. En este caso, toma muy poco tiempo en ejecutarse **SQLDescribeCol** y el controlador debe simplemente ejecutar la función en lugar de artificialmente retrasar la ejecución. Por otro lado, si el controlador necesita para recuperar los metadatos del origen de datos, debe devolver el control a la aplicación mientras hace esto. Por lo tanto, la aplicación debe ser capaz de controlar un código de retorno distinto de SQL_STILL_EXECUTING primera vez que ejecuta una función de forma asincrónica.  
  
## <a name="executing-statement-operations-asynchronously"></a>Ejecutar operaciones de instrucción de forma asincrónica  
 Las siguientes funciones de instrucción operan en un origen de datos y se pueden ejecutar de forma asincrónica:  
  
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
  
 Ejecución de la instrucción asincrónicos se controla en una instrucción o una función de la conexión, según el origen de datos. Es decir, la aplicación no especifica que una determinada función es que se ejecutará de forma asincrónica, pero que es cualquier función que se ejecuta en una instrucción determinada que se ejecutará de forma asincrónica. Para buscar fuera cuál se admite, una aplicación llama a [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) con la opción de SQL_ASYNC_MODE. SQL_AM_CONNECTION se devuelve si se admite la ejecución asincrónica de nivel de conexión (para un identificador de instrucción); SQL_AM_STATEMENT si se admite la ejecución asincrónica de nivel de instrucción.  
  
 Para especificar que son funciones que se ejecuta con una instrucción determinada ejecuta de forma asincrónica, la aplicación llama a **SQLSetStmtAttr** con el SQL_ATTR_ASYNC_ENABLE de atributo y lo establece en SQL_ASYNC_ENABLE_ON. Si se admite el procesamiento asincrónico de nivel de conexión, el atributo de instrucción SQL_ATTR_ASYNC_ENABLE es de solo lectura y su valor es igual que el atributo de conexión de la conexión en el que se ha asignado la instrucción. Es específico del controlador si se establece el valor del atributo de instrucción de asignación cuando la instrucción o una versión posterior. Al intentar establecerla se devolverá SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada).  
  
 Para especificar que las funciones que se ejecuta con una conexión determinada se puede ejecuta de forma asincrónica, la aplicación llama a **SQLSetConnectAttr** con el SQL_ATTR_ASYNC_ENABLE de atributo y lo establece en SQL_ASYNC_ENABLE_ON. Todos los identificadores de instrucciones futuras asignados en la conexión se habilitarán para la ejecución asincrónica; es definido por el controlador si se habilitarán los identificadores de instrucciones existentes por esta acción. Si se establece SQL_ATTR_ASYNC_ENABLE en SQL_ASYNC_ENABLE_OFF, todas las instrucciones de la conexión están en modo sincrónico. Si está habilitada la ejecución asincrónica mientras hay una instrucción activa en la conexión, se devuelve un error.  
  
 Para determinar el número máximo de instrucciones simultáneas activas en modo asincrónico que puede admitir el controlador en una conexión determinada, la aplicación llama a **SQLGetInfo** con la opción SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
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
  
 Mientras se ejecuta de forma asincrónica una función, la aplicación puede llamar a funciones en cualquier otra instrucción. La aplicación también puede llamar a funciones en cualquier conexión, excepto el único asociado con la instrucción asincrónica. Pero la aplicación solo puede llamar a la función original y las funciones siguientes (con el identificador de instrucción o su conexión asociada, el identificador de entorno), después de una operación de la instrucción devuelve SQL_STILL_EXECUTING:  
  
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
  
 Si la aplicación llama a cualquier otra función con la instrucción asincrónica o con la conexión asociada a dicha instrucción, la función devuelve SQLSTATE HY010 (función error de secuencia), por ejemplo.  
  
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
  
 Cuando una aplicación llama a una función para determinar si todavía se está ejecutando asincrónicamente, debe usar el identificador de la instrucción original. Esto es porque se realiza un seguimiento de ejecución asincrónica en una base por instrucción. La aplicación también debe proporcionar los valores válidos para los demás argumentos, llevará a cabo los argumentos originales - para superar la comprobación en el Administrador de controladores de errores. Sin embargo, después de que el controlador comprueba el identificador de instrucción y determina que la instrucción se ejecuta de forma asincrónica, omite todos los demás argumentos.  
  
 Mientras se ejecuta una función de forma asincrónica: es decir, después de que ha devuelto SQL_STILL_EXECUTING y antes de devolver un código diferente: la aplicación puede cancelarlo mediante una llamada a **SQLCancel** o **SQLCancelHandle** con el mismo identificador de instrucción. Esto no se garantiza para cancelar la ejecución de la función. Por ejemplo, es posible que haya terminado ya la función. Además, el código devuelto por **SQLCancel** o **SQLCancelHandle** sólo indica si el intento de cancelar la función se realizó correctamente, no si realmente canceló la función. Para determinar si se ha cancelado la función, la aplicación llama a la función de nuevo. Si se ha cancelado la función, devuelve SQL_ERROR y SQLSTATE HY008 (operación cancelada). Si no se ha cancelado la función, devuelve otro código, como SQL_SUCCESS, SQL_STILL_EXECUTING o SQL_ERROR con un valor de SQLSTATE diferentes.  
  
 Para deshabilitar la ejecución asincrónica de una instrucción determinada cuando el controlador admite el procesamiento asincrónico de nivel de instrucción, la aplicación llama a **SQLSetStmtAttr** con el SQL_ATTR_ASYNC_ENABLE de atributo y lo establece en SQL_ ASYNC_ENABLE_OFF. Si el controlador admite el procesamiento asincrónico de nivel de conexión, la aplicación llama a **SQLSetConnectAttr** para establecer SQL_ATTR_ASYNC_ENABLE en SQL_ASYNC_ENABLE_OFF, lo que deshabilita la ejecución asincrónica de todas las instrucciones en el conexión.  
  
 La aplicación debe procesar los registros de diagnóstico en el bucle de repetición de la función original. Si **SQLGetDiagField** o **SQLGetDiagRec** se llama cuando se ejecuta una función asincrónica, devolverá la lista actual de registros de diagnóstico. Cada vez que se repite la llamada de función original, sino que borra los registros de diagnóstico anteriores.  
  
## <a name="executing-connection-operations-asynchronously"></a>Ejecuta de forma asincrónica las operaciones de conexión  
 Antes de ODBC 3.8, se permitió la ejecución asincrónica para operaciones relacionadas con la instrucción, como preparación, ejecutar y capturar, así como para las operaciones de metadatos de catálogo. A partir de ODBC 3.8, ejecución asincrónica también es posible para las operaciones relacionadas con la conexión, tal como conectar, desconectar, commit y rollback.  
  
 Para obtener más información sobre ODBC 3.8, consulte [What ' s New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 Ejecuta de forma asincrónica las operaciones de conexión es útil en los escenarios siguientes:  
  
-   Cuando un pequeño número de subprocesos administra un gran número de dispositivos con las tarifas de datos muy alta. Para maximizar la capacidad de respuesta y la escalabilidad es deseable para todas las operaciones asincrónicas.  
  
-   Si desea superponer las operaciones de base de datos a través de varias conexiones para reducir los tiempos de transferencia transcurrido.  
  
-   Eficaz las llamadas asincrónicas de ODBC y la capacidad para cancelar las operaciones de conexión permiten una aplicación para permitir al usuario cancelar cualquier operación lenta sin tener que esperar tiempos de espera.  
  
 Las siguientes funciones, que operan en identificadores de conexión, ahora se ejecutan de forma asincrónica:  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 Para determinar si un controlador admite las operaciones asincrónicas en estas funciones, una aplicación llama a **SQLGetInfo** con SQL_ASYNC_DBC_FUNCTIONS. SQL_ASYNC_DBC_CAPABLE se devuelve si se admiten las operaciones asincrónicas. SQL_ASYNC_DBC_NOT_CAPABLE se devuelve si no se admiten las operaciones asincrónicas.  
  
 Para especificar que las funciones que se ejecuta con una conexión determinada se puede ejecuta de forma asincrónica, la aplicación llama a **SQLSetConnectAttr** y establece el atributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE en SQL_ASYNC_DBC_ENABLE _ACTIVAR. Establecer un atributo de conexión antes de establecer una conexión siempre se ejecuta de forma sincrónica. Además, la operación de establecimiento de la conexión atributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE con **SQLSetConnectAttr** siempre se ejecuta de forma sincrónica.  
  
 Una aplicación puede permitir que una operación asincrónica antes de realizar una conexión. Dado que el Administrador de controladores no se puede determinar qué controlador usar antes de realizar una conexión, el Administrador de controladores siempre devolverá el éxito en **SQLSetConnectAttr**. Sin embargo, no puede conectarse si el controlador ODBC no admite operaciones asincrónicas.  
  
 En general, puede haber a lo sumo una ejecución asincrónica de función asociada con un identificador de conexión en particular o un identificador de instrucción. Sin embargo, un identificador de conexión puede tener más de un identificador de la instrucción asociada. Si no hay ninguna operación asincrónica que se ejecuta en el identificador de conexión, un identificador de instrucción asociado puede ejecutar una operación asincrónica. De forma similar, puede tener una operación asincrónica en un identificador de conexión si no hay ninguna operación asincrónica en curso en cualquier identificador de instrucción asociado. Un intento de ejecutar una operación asincrónica utilizando un identificador que se está ejecutando actualmente una operación asincrónica devolverá HY010, "Error de secuencia de función".  
  
 Si una operación de conexión devuelve SQL_STILL_EXECUTING, una aplicación solo puede llamar la función original y las siguientes funciones para ese identificador de conexión:  
  
-   **SQLCancelHandle** (en el identificador de conexión)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (asignar DBC/ENV)  
  
-   **SQLAllocHandleStd** (asignar DBC/ENV)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 La aplicación debe procesar los registros de diagnóstico en el bucle de repetición de la función original. Si se llama a SQLGetDiagField o SQLGetDiagRec cuando se está ejecutando una función asincrónica, devolverá la lista actual de los registros de diagnóstico. Cada vez que se repite la llamada de función original, sino que borra los registros de diagnóstico anteriores.  
  
 Si una conexión se está abierto o cerrado de forma asincrónica, la operación está completa cuando la aplicación recibe SQL_SUCCESS o SQL_SUCCESS_WITH_INFO en la llamada de función original.  
  
 Se ha agregado una nueva función para ODBC 3.8, **SQLCancelHandle**. Esta función cancela las funciones de seis conexiones (**SQLBrowseConnect**, **SQLConnect**, **SQLDisconnect**, **SQLDriverConnect**, **SQLEndTran**, y **SQLSetConnectAttr**). Una aplicación debe llamar a **SQLGetFunctions** para determinar si el controlador admite **SQLCancelHandle**. Igual que con **SQLCancel**si **SQLCancelHandle** devuelve un valor correcto, no significa que se ha cancelado la operación. Una aplicación debe llamar a la función original para determinar si se canceló la operación. **SQLCancelHandle** le permite cancelar las operaciones asincrónicas en identificadores de conexión o identificadores de instrucciones. Uso de **SQLCancelHandle** para cancelar una operación en una instrucción de identificador es igual que llamar a **SQLCancel**.  
  
 No es necesario admitir ambos **SQLCancelHandle** y las operaciones de conexión asincrónica al mismo tiempo. Un controlador es compatible con las operaciones de conexión asincrónica, pero no **SQLCancelHandle**, o viceversa.  
  
 Las operaciones de conexión asincrónica y **SQLCancelHandle** también puede usarse por ODBC 3.x aplicaciones y ODBC 2.x con un controlador de ODBC 3.8 y el Administrador de controladores de ODBC 3.8. Para obtener información acerca de cómo habilitar una aplicación anterior usar nuevas características de la versión más reciente ODBC, vea [matriz de compatibilidad](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Agrupar conexiones  
 Cada vez que la agrupación de conexiones está habilitada, mínimamente solo admiten operaciones asincrónicas para establecer una conexión (con **SQLConnect** y **SQLDriverConnect**) y cerrar una conexión con **SQLDisconnect**. Pero una aplicación todavía debe ser capaz de controlar el valor devuelto de SQL_STILL_EXECUTING de **SQLConnect**, **SQLDriverConnect**, y **SQLDisconnect**.  
  
 Cuando se habilita la agrupación de conexiones, **SQLEndTran** y **SQLSetConnectAttr** se admiten para las operaciones asincrónicas.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="description"></a>Descripción  
 El ejemplo siguiente muestra cómo usar **SQLSetConnectAttr** para habilitar la ejecución asincrónica de funciones relacionadas con la conexión.  
  
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
 Este ejemplo muestra las operaciones de confirmación asincrónica. Operaciones de reversión también pueden realizarse de este modo.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Ejecución de instrucciones ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
