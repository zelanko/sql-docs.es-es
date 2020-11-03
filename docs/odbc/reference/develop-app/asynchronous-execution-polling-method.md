---
description: Ejecución asincrónica (método de sondeo)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2767a89347329ee084c8b055bcb444dc4e78117
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243534"
---
# <a name="asynchronous-execution-polling-method"></a>Ejecución asincrónica (método de sondeo)
Antes de ODBC 3,8 y el SDK de Windows 7, solo se permitían las operaciones asincrónicas en las funciones de instrucción. Para obtener más información, vea **operaciones de ejecución de instrucciones de forma asincrónica** , más adelante en este tema.  
  
 ODBC 3,8 en el SDK de Windows 7 presentó la ejecución asincrónica en operaciones relacionadas con la conexión. Para obtener más información, vea la sección **ejecución de operaciones de conexión de forma asincrónica** , más adelante en este tema.  
  
 En el SDK de Windows 7, para las operaciones de conexión o instrucción asincrónicas, una aplicación determinó que la operación asincrónica se completó con el método de sondeo. A partir del SDK de Windows 8, puede determinar que una operación asincrónica se ha completado con el método de notificación. Para obtener más información, vea [ejecución asincrónica (método de notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
 De forma predeterminada, los controladores ejecutan las funciones ODBC sincrónicamente. es decir, la aplicación llama a una función y el controlador no devuelve el control a la aplicación hasta que haya finalizado la ejecución de la función. Sin embargo, algunas funciones se pueden ejecutar de forma asincrónica. es decir, la aplicación llama a la función, y el controlador, después del procesamiento mínimo, devuelve el control a la aplicación. A continuación, la aplicación puede llamar a otras funciones mientras la primera función todavía se está ejecutando.  
  
 La ejecución asincrónica es compatible con la mayoría de las funciones que se ejecutan en gran medida en el origen de datos, como las funciones para establecer conexiones, preparar y ejecutar instrucciones SQL, recuperar metadatos, capturar datos y confirmar transacciones. Resulta muy útil cuando la tarea que se ejecuta en el origen de datos tarda mucho tiempo, como un proceso de inicio de sesión o una consulta compleja en una base de datos grande.  
  
 Cuando la aplicación ejecuta una función con una instrucción o una conexión que está habilitada para el procesamiento asincrónico, el controlador realiza una cantidad mínima de procesamiento (por ejemplo, la comprobación de los argumentos de los errores), realiza el procesamiento en el origen de datos y devuelve el control a la aplicación con el código de retorno SQL_STILL_EXECUTING. A continuación, la aplicación realiza otras tareas. Para determinar cuándo ha finalizado la función asincrónica, la aplicación sondea el controlador a intervalos regulares mediante una llamada a la función con los mismos argumentos que usó originalmente. Si la función todavía se está ejecutando, devuelve SQL_STILL_EXECUTING; Si ha terminado de ejecutarse, devuelve el código que habría devuelto cuando se ejecutó sincrónicamente, como SQL_SUCCESS, SQL_ERROR o SQL_NEED_DATA.  
  
 Si una función se ejecuta de forma sincrónica o asincrónica es específica del controlador. Por ejemplo, supongamos que los metadatos del conjunto de resultados se almacenan en caché en el controlador. En este caso, tarda muy poco tiempo en ejecutar **SQLDescribeCol** y el controlador solo debe ejecutar la función en lugar de retrasar la ejecución de forma artificial. Por otro lado, si el controlador necesita recuperar los metadatos del origen de datos, debe devolver el control a la aplicación mientras lo está haciendo. Por lo tanto, la aplicación debe ser capaz de controlar un código de retorno que no sea SQL_STILL_EXECUTING cuando ejecute por primera vez una función de forma asincrónica.  
  
## <a name="executing-statement-operations-asynchronously"></a>Ejecutar operaciones de instrucción de forma asincrónica  
 Las siguientes funciones de instrucción operan en un origen de datos y se pueden ejecutar de forma asincrónica:  

:::row:::
    :::column:::
        [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
        [SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
        [SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
        [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)  
        [SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)  
        [SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
        [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
        [SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)  
        [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)  
    :::column-end:::
    :::column:::
        [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
        [SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
        [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
        [SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
        [SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
        [SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)  
        [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
        [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)  
        [SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)  
    :::column-end:::
    :::column:::
        [SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
        [SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
        [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)  
        [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)  
        [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)  
        [SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
        [SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)  
        [SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
        [SQLTables](../../../odbc/reference/syntax/sqltables-function.md)  
    :::column-end:::
:::row-end:::

 La ejecución de instrucciones asincrónicas se controla por cada instrucción o por conexión, dependiendo del origen de datos. Es decir, la aplicación especifica que una función determinada se ejecutará de forma asincrónica, pero que cualquier función ejecutada en una instrucción determinada se ejecutará de forma asincrónica. Para averiguar cuál es compatible, una aplicación llama a [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) con una opción de SQL_ASYNC_MODE. Se devuelve SQL_AM_CONNECTION si se admite la ejecución asincrónica en el nivel de conexión (para un identificador de instrucción); SQL_AM_STATEMENT si se admite la ejecución asincrónica de nivel de instrucción.  
  
 Para especificar que las funciones ejecutadas con una instrucción determinada se ejecuten de forma asincrónica, la aplicación llama a **SQLSetStmtAttr** con el atributo SQL_ATTR_ASYNC_ENABLE y lo establece en SQL_ASYNC_ENABLE_ON. Si se admite el procesamiento asincrónico de nivel de conexión, el atributo de instrucción SQL_ATTR_ASYNC_ENABLE es de solo lectura y su valor es el mismo que el atributo de conexión de la conexión en la que se asignó la instrucción. Es específico del controlador si el valor del atributo de instrucción se establece en el tiempo de asignación de la instrucción o en una versión posterior. Si intenta establecerlo, se devolverá SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada).  
  
 Para especificar que las funciones ejecutadas con una conexión determinada se ejecuten de forma asincrónica, la aplicación llama a **SQLSetConnectAttr** con el atributo SQL_ATTR_ASYNC_ENABLE y lo establece en SQL_ASYNC_ENABLE_ON. Todos los identificadores de instrucción futuros asignados en la conexión se habilitarán para la ejecución asincrónica; está definido por el controlador si esta acción va a habilitar los identificadores de instrucción existentes. Si SQL_ATTR_ASYNC_ENABLE se establece en SQL_ASYNC_ENABLE_OFF, todas las instrucciones de la conexión se encuentran en modo sincrónico. Se devuelve un error si la ejecución asincrónica está habilitada mientras haya una instrucción activa en la conexión.  
  
 Para determinar el número máximo de instrucciones simultáneas activas en modo asincrónico que el controlador puede admitir en una conexión determinada, la aplicación llama a **SQLGetInfo** con la opción SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
 En el código siguiente se muestra cómo funciona el modelo de sondeo:  
  
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
  
 Mientras una función se ejecuta de forma asincrónica, la aplicación puede llamar a funciones en cualquier otra instrucción. La aplicación también puede llamar a funciones en cualquier conexión, excepto la asociada a la instrucción asincrónica. Pero la aplicación solo puede llamar a la función original y a las funciones siguientes (con el identificador de instrucción o su conexión asociada, el identificador de entorno), después de que una operación de instrucción devuelva SQL_STILL_EXECUTING:  
  
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
  
 Si la aplicación llama a cualquier otra función con la instrucción asincrónica o con la conexión asociada a esa instrucción, la función devuelve SQLSTATE HY010 (error de secuencia de función), por ejemplo.  
  
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
  
 Cuando una aplicación llama a una función para determinar si aún se está ejecutando de forma asincrónica, debe utilizar el identificador de instrucción original. Esto se debe a que se realiza un seguimiento de la ejecución asincrónica en cada instrucción. La aplicación también debe proporcionar valores válidos para los demás argumentos: los argumentos originales sí: para obtener la comprobación de errores anterior en el administrador de controladores. Sin embargo, una vez que el controlador comprueba el identificador de la instrucción y determina que la instrucción se ejecuta de forma asincrónica, omite todos los demás argumentos.  
  
 Mientras una función se ejecuta de forma asincrónica, es decir, después de que haya devuelto SQL_STILL_EXECUTING y antes de que devuelva un código diferente, la aplicación puede cancelarla llamando a **SQLCancel** o **SQLCancelHandle** con el mismo identificador de instrucción. No se garantiza que se cancele la ejecución de la función. Por ejemplo, puede que la función ya haya finalizado. Además, el código devuelto por **SQLCancel** o **SQLCancelHandle** solo indica si el intento de cancelar la función se realizó correctamente, no si realmente se canceló la función. Para determinar si se canceló la función, la aplicación llama de nuevo a la función. Si se canceló la función, devuelve SQL_ERROR y SQLSTATE HY008 (operación cancelada). Si la función no se canceló, devuelve otro código, como SQL_SUCCESS, SQL_STILL_EXECUTING o SQL_ERROR con un SQLSTATE diferente.  
  
 Para deshabilitar la ejecución asincrónica de una instrucción determinada cuando el controlador admite el procesamiento asincrónico de nivel de instrucción, la aplicación llama a **SQLSetStmtAttr** con el atributo SQL_ATTR_ASYNC_ENABLE y lo establece en SQL_ASYNC_ENABLE_OFF. Si el controlador admite el procesamiento asincrónico de nivel de conexión, la aplicación llama a **SQLSetConnectAttr** para establecer SQL_ATTR_ASYNC_ENABLE en SQL_ASYNC_ENABLE_OFF, lo que deshabilita la ejecución asincrónica de todas las instrucciones en la conexión.  
  
 La aplicación debe procesar los registros de diagnóstico en el bucle de repetición de la función original. Si se llama a **SQLGetDiagField** o **SQLGetDiagRec** cuando se está ejecutando una función asincrónica, devolverá la lista actual de registros de diagnóstico. Cada vez que se repite la llamada de función original, se borran los registros de diagnóstico anteriores.  
  
## <a name="executing-connection-operations-asynchronously"></a>Ejecutar operaciones de conexión de forma asincrónica  
 Antes de ODBC 3,8, se permitía la ejecución asincrónica para las operaciones relacionadas con instrucciones como preparar, ejecutar y recuperar, así como para las operaciones de metadatos del catálogo. A partir de ODBC 3,8, la ejecución asincrónica también es posible para las operaciones relacionadas con la conexión, como la conexión, la desconexión, la confirmación y la reversión.  
  
 Para obtener más información acerca de ODBC 3,8, vea [novedades de odbc 3,8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 Ejecutar operaciones de conexión de forma asincrónica es útil en los escenarios siguientes:  
  
-   Cuando un número pequeño de subprocesos administra un gran número de dispositivos con una velocidad de datos muy alta. Para maximizar la capacidad de respuesta y la escalabilidad, es deseable que todas las operaciones sean asincrónicas.  
  
-   Si desea superponer las operaciones de base de datos en varias conexiones para reducir los tiempos de transferencia transcurridos.  
  
-   Las llamadas ODBC eficaces asincrónicas y la capacidad de cancelar las operaciones de conexión permiten que una aplicación permita al usuario cancelar cualquier operación lenta sin tener que esperar los tiempos de espera.  
  
 Las siguientes funciones, que operan en identificadores de conexión, ahora se pueden ejecutar de forma asincrónica:  

:::row:::
    :::column:::
        [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
        [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)  
        [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)  
        [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
    :::column-end:::
:::row-end:::

 Para determinar si un controlador admite operaciones asincrónicas en estas funciones, una aplicación llama a **SQLGetInfo** con SQL_ASYNC_DBC_FUNCTIONS. Se devuelve SQL_ASYNC_DBC_CAPABLE si se admiten operaciones asincrónicas. Se devuelve SQL_ASYNC_DBC_NOT_CAPABLE si no se admiten las operaciones asincrónicas.  
  
 Para especificar que las funciones ejecutadas con una conexión determinada se ejecuten de forma asincrónica, la aplicación llama a **SQLSetConnectAttr** y establece el atributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE en SQL_ASYNC_DBC_ENABLE_ON. La configuración de un atributo de conexión antes de establecer una conexión siempre se ejecuta de forma sincrónica. Además, la operación que establece el atributo de conexión SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE con **SQLSetConnectAttr** siempre se ejecuta de forma sincrónica.  
  
 Una aplicación puede habilitar la operación asincrónica antes de establecer una conexión. Dado que el administrador de controladores no puede determinar qué controlador usar antes de establecer una conexión, el administrador de controladores siempre devolverá un valor correcto en **SQLSetConnectAttr** . Sin embargo, es posible que no se pueda conectar si el controlador ODBC no admite operaciones asincrónicas.  
  
 En general, puede haber como máximo una función que se ejecuta de forma asincrónica asociada a un identificador de conexión o un identificador de instrucción determinado. Sin embargo, un identificador de conexión puede tener más de un identificador de instrucción asociado. Si no hay ninguna operación asincrónica en ejecución en el identificador de conexión, un identificador de instrucción asociado puede ejecutar una operación asincrónica. Del mismo modo, puede tener una operación asincrónica en un identificador de conexión si no hay ninguna operación asincrónica en curso en ningún identificador de instrucción asociado. Un intento de ejecutar una operación asincrónica mediante un identificador que está ejecutando actualmente una operación asincrónica devolverá HY010, "error de secuencia de función".  
  
 Si una operación de conexión devuelve SQL_STILL_EXECUTING, una aplicación solo puede llamar a la función original y a las funciones siguientes para ese identificador de conexión:  
  
-   **SQLCancelHandle** (en el identificador de conexión)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (asignar env/DBC)  
  
-   **SQLAllocHandleStd** (asignar env/DBC)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 La aplicación debe procesar los registros de diagnóstico en el bucle de repetición de la función original. Si se llama a SQLGetDiagField o SQLGetDiagRec cuando se está ejecutando una función asincrónica, devolverá la lista actual de registros de diagnóstico. Cada vez que se repite la llamada de función original, se borran los registros de diagnóstico anteriores.  
  
 Si una conexión se abre o se cierra de forma asincrónica, la operación se completa cuando la aplicación recibe SQL_SUCCESS o SQL_SUCCESS_WITH_INFO en la llamada de función original.  
  
 Se ha agregado una nueva función a ODBC 3,8, **SQLCancelHandle** . Esta función cancela las seis funciones de conexión ( **SQLBrowseConnect** , **SQLConnect** , **SQLDisconnect** , **SQLDriverConnect** , **SQLEndTran** y **SQLSetConnectAttr** ). Una aplicación debe llamar a **SQLGetFunctions** para determinar si el controlador admite **SQLCancelHandle** . Al igual que con **SQLCancel** , si **SQLCancelHandle** devuelve Success, no significa que se haya cancelado la operación. Una aplicación debe llamar de nuevo a la función original para determinar si se canceló la operación. **SQLCancelHandle** permite cancelar operaciones asincrónicas en identificadores de conexión o de instrucciones. El uso de **SQLCancelHandle** para cancelar una operación en un identificador de instrucción es igual que llamar a **SQLCancel** .  
  
 No es necesario admitir las operaciones de conexión asincrónica y **SQLCancelHandle** al mismo tiempo. Un controlador puede admitir operaciones de conexión asincrónicas pero no **SQLCancelHandle** , o viceversa.  
  
 Las operaciones de conexión asincrónica y **SQLCancelHandle** también se pueden usar en las aplicaciones ODBC 3. x y ODBC 2. x con un controlador ODBC 3,8 y el administrador de controladores ODBC 3,8. Para obtener información sobre cómo habilitar una aplicación más antigua para usar nuevas características en una versión posterior de ODBC, consulte [matriz de compatibilidad](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Agrupar conexiones  
 Cada vez que la agrupación de conexiones está habilitada, las operaciones asincrónicas solo se admiten mínimas para establecer una conexión (con **SQLConnect** y **SQLDriverConnect** ) y cerrar una conexión con **SQLDisconnect** . Pero una aplicación todavía debe ser capaz de controlar los SQL_STILL_EXECUTING valor devuelto de **SQLConnect** , **SQLDriverConnect** y **SQLDisconnect** .  
  
 Cuando la agrupación de conexiones está habilitada, se admiten **SQLEndTran** y **SQLSetConnectAttr** para las operaciones asincrónicas.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enable-asynchronous-execution-of-connection-functions"></a>A. Habilitar la ejecución asincrónica de funciones de conexión

 En el ejemplo siguiente se muestra cómo usar **SQLSetConnectAttr** para habilitar la ejecución asincrónica de las funciones relacionadas con la conexión.  
  
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
  
### <a name="b-asynchronous-commit-operations"></a>B. Operaciones de confirmación asincrónicas 

 En este ejemplo se muestran las operaciones de confirmación asincrónica. Las operaciones de reversión también se pueden realizar de esta manera.  
  
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
