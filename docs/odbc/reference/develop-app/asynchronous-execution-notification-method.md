---
title: Ejecución asincrónica (método de notificación) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 250e71dcb47d44a6e437d12c269ea23fa6fb3c2c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306416"
---
# <a name="asynchronous-execution-notification-method"></a>Ejecución asincrónica (método de notificación)
ODBC permite la ejecución asincrónica de operaciones de conexión e instrucción. Un subproceso de aplicación puede llamar a una función ODBC en modo asincrónico y la función puede devolverse antes de que se complete la operación, lo que permite al subproceso de aplicación realizar otras tareas. En el SDK de Windows 7, para operaciones de conexión o instrucción asincrónica, una aplicación determinó que la operación asincrónica se completó mediante el método de sondeo. Para obtener más información, vea [Ejecución asincrónica (método de sondeo).](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md) A partir del SDK de Windows 8, puede determinar que una operación asincrónica se completa mediante el método de notificación.  
  
 En el método de sondeo, las aplicaciones deben llamar a la función asincrónica cada vez que desea el estado de la operación. El método de notificación es similar a la devolución de llamada y esperar en ADO.NET. ODBC, sin embargo, utiliza eventos Win32 como el objeto de notificación.  
  
 La biblioteca de cursores ODBC y la notificación asincrónica ODBC no se pueden usar al mismo tiempo. Establecer ambos atributos devolverá un error con SQLSTATE S1119 (la biblioteca de cursores y la notificación asincrónica no se pueden habilitar al mismo tiempo).  
  
 Consulte [Notificación de finalización de](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) funciones asincrónicas para obtener información para los desarrolladores de controladores.  
  
> [!NOTE]  
>  El método de notificación no es compatible con la biblioteca de cursores. Una aplicación recibirá un mensaje de error si intenta habilitar la biblioteca de cursores a través de SQLSetConnectAttr, cuando el método de notificación está habilitado.  
  
## <a name="overview"></a>Información general  
 Cuando se llama a una función ODBC en modo asincrónico, el control se devuelve a la aplicación que realiza la llamada inmediatamente con el código de retorno SQL_STILL_EXECUTING. La aplicación debe sondear repetidamente la función hasta que devuelve algo distinto de SQL_STILL_EXECUTING. El bucle de sondeo aumenta la utilización de la CPU, lo que provoca un rendimiento deficiente en muchos escenarios asincrónicos.  
  
 Siempre que se utiliza el modelo de notificación, el modelo de sondeo está deshabilitado. Las aplicaciones no deben llamar a la función original de nuevo. Llame a [SQLCompleteAsync Function](../../../odbc/reference/syntax/sqlcompleteasync-function.md) para completar la operación asincrónica. Si una aplicación vuelve a llamar a la función original antes de que se complete la operación asincrónica, la llamada devolverá SQL_ERROR con SQLSTATE IM017 (El sondeo está deshabilitado en el modo de notificación asincrónica).  
  
 Cuando se usa el modelo de notificación, la aplicación puede llamar a **SQLCancel** o **SQLCancelHandle** para cancelar una instrucción o operación de conexión. Si la solicitud de cancelación se realiza correctamente, ODBC devolverá SQL_SUCCESS. Este mensaje no indica que la función se haya cancelado realmente; indica que se ha procesado la solicitud de cancelación. Si la función se cancela realmente depende del controlador y del origen de datos. Cuando se cancela una operación, el Administrador de controladores seguirá señalando el evento. El Administrador de controladores devuelve SQL_ERROR en el búfer de código de retorno y el estado es SQLSTATE HY008 (Operación cancelada) para indicar que la cancelación se ha realizado correctamente. Si la función ha completado su procesamiento normal, el Administrador de controladores devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
### <a name="downlevel-behavior"></a>Comportamiento de nivel inferior  
 La versión del Administrador de controladores ODBC que admite esta notificación en completa es ODBC 3.81.  
  
|Versión ODBC de la aplicación|Versión del Administrador de controladores|Versión del controlador|Comportamiento|  
|------------------------------|----------------------------|--------------------|--------------|  
|Nueva aplicación de cualquier versión ODBC|ODBC 3.81|Controlador ODBC 3.80|La aplicación puede utilizar esta característica si el controlador admite esta característica, de lo contrario el Administrador de controladores se producirá un error.|  
|Nueva aplicación de cualquier versión ODBC|ODBC 3.81|Controlador Pre-ODBC 3.80|El Administrador de controladores se producirá un error si el controlador no admite esta característica.|  
|Nueva aplicación de cualquier versión ODBC|Pre-ODBC 3.81|Any|Cuando la aplicación utiliza esta característica, un administrador de controladores antiguo considerará los nuevos atributos como atributos específicos del controlador y el controlador debe error out. Un nuevo Administrador de controladores no pasará estos atributos al controlador.|  
  
 Una aplicación debe comprobar la versión del Administrador de controladores antes de usar esta característica. De lo contrario, si un controlador mal escrito no sale por error y la versión del Administrador de controladores es anterior a ODBC 3.81, el comportamiento es indefinido.  
  
## <a name="use-cases"></a>Casos de uso  
 En esta sección se muestran los casos de uso para la ejecución asincrónica y el mecanismo de sondeo.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>Integrar datos de múltiples orígenes ODBC  
 Una aplicación de integración de datos captura de forma asincrónica datos de varios orígenes de datos. Algunos de los datos proceden de orígenes de datos remotos y algunos datos proceden de archivos locales. La aplicación no puede continuar hasta que se completen las operaciones asincrónicas.  
  
 En lugar de sondear repetidamente una operación para determinar si se ha completado, la aplicación puede crear un objeto de evento y asociarlo a un identificador de conexión ODBC o un identificador de instrucción ODBC. A continuación, la aplicación llama a las API de sincronización del sistema operativo para esperar en un objeto de evento o en muchos objetos de evento (eventos ODBC y otros eventos de Windows). ODBC señalará el objeto de evento cuando se complete la operación asincrónica ODBC correspondiente.  
  
 En Windows, se usarán objetos de evento Win32 que proporcionarán al usuario un modelo de programación unificado. Los administradores de controladores en otras plataformas pueden usar la implementación de objetos de evento específica para esas plataformas.  
  
 En el ejemplo de código siguiente se muestra el uso de la notificación asincrónica de conexión e instrucción:  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>Determinar si un controlador admite la notificación asincrónica  
 Una aplicación ODBC puede determinar si un controlador ODBC admite la notificación asincrónica llamando a [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md). Por consiguiente, el Administrador de controladores ODBC llamará a **SQLGetInfo** del controlador con SQL_ASYNC_NOTIFICATION.  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Asociar un identificador de evento Win32 con un identificador ODBC  
 Las aplicaciones son responsables de crear objetos de evento Win32 utilizando las funciones Win32 correspondientes. Una aplicación puede asociar un identificador de evento Win32 con un identificador de conexión ODBC o un identificador de instrucción ODBC.  
  
 Los atributos de conexión SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE y SQL_ATTR_ASYNC_DBC_EVENT determinar si ODBC se ejecuta en modo asincrónico y si ODBC habilita el modo de notificación para un identificador de conexión. Los atributos de instrucción SQL_ATTR_ASYNC_ENABLE y SQL_ATTR_ASYNC_STMT_EVENT determinar si ODBC se ejecuta en modo asincrónico y si ODBC habilita el modo de notificación para un identificador de instrucción.  
  
|SQL_ATTR_ASYNC_ENABLE o SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT o SQL_ATTR_ASYNC_DBC_EVENT|Mode|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|Habilitar|no nulo|Notificación asincrónica|  
|Habilitar|null|Sondeo asincrónico|  
|Disable|cualquiera|Sincrónica|  
  
 Una aplicación puede deshabilitar temporalmente el modo de operación asincrónica. ODBC omite los valores de SQL_ATTR_ASYNC_DBC_EVENT si la operación asincrónica de nivel de conexión está deshabilitada. ODBC omite los valores de SQL_ATTR_ASYNC_STMT_EVENT si la operación asincrónica de nivel de instrucción está deshabilitada.  
  
 Llamada sincrónica de **SQLSetStmtAttr** y **SQLSetConnectAttr**  
 -   **SQLSetConnectAttr** admite operaciones asincrónicas, pero la invocación de **SQLSetConnectAttr** para establecer SQL_ATTR_ASYNC_DBC_EVENT siempre es sincrónica.  
  
-   **SQLSetStmtAttr** no admite la ejecución asincrónica.  
  
 Escenario de error-out  
 Cuando **SQLSetConnectAttr** se llama antes de realizar una conexión, el Administrador de controladores no puede determinar qué controlador usar. Por lo tanto, el Administrador de controladores devuelve el éxito de **SQLSetConnectAttr,** pero es posible que el atributo no esté listo para establecerse en el controlador. El Administrador de controladores establecerá estos atributos cuando la aplicación llama a una función de conexión. El Administrador de controladores puede realizar un error porque el controlador no admite operaciones asincrónicas.  
  
 Herencia de atributos de conexión  
 Normalmente, las instrucciones de una conexión heredarán los atributos de conexión. Sin embargo, el atributo SQL_ATTR_ASYNC_DBC_EVENT no es heredable y solo afecta a las operaciones de conexión.  
  
 Para asociar un identificador de evento con un identificador de conexión ODBC, una aplicación ODBC llama a la API ODBC **SQLSetConnectAttr** y especifica SQL_ATTR_ASYNC_DBC_EVENT como el atributo y el identificador de evento como el valor del atributo. El nuevo atributo ODBC SQL_ATTR_ASYNC_DBC_EVENT es de tipo SQL_IS_POINTER.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 Normalmente, las aplicaciones crean objetos de evento de restablecimiento automático. ODBC no restablecerá el objeto de evento. Las aplicaciones deben asegurarse de que el objeto no está en estado de señalización antes de llamar a cualquier función ODBC asincrónica.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT es un atributo solo del Administrador de controladores que no se establecerá en el controlador.  
  
 El valor predeterminado de SQL_ATTR_ASYNC_DBC_EVENT es NULL. Si el controlador no admite la notificación asincrónica, obtener o establecer SQL_ATTR_ASYNC_DBC_EVENT devolverá SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido).  
  
 Si el último valor de SQL_ATTR_ASYNC_DBC_EVENT establecido en un identificador de conexión ODBC no es NULL y la aplicación habilita el modo asincrónico estableciendo el atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE con SQL_ASYNC_DBC_ENABLE_ON, al llamar a cualquier función de conexión ODBC que admita el modo asincrónico se obtendrá una notificación de finalización. Si el último valor de SQL_ATTR_ASYNC_DBC_EVENT establecido en un identificador de conexión ODBC es NULL, ODBC no enviará a la aplicación ninguna notificación, independientemente de si el modo asincrónico está habilitado.  
  
 Una aplicación puede establecer SQL_ATTR_ASYNC_DBC_EVENT antes o después de establecer el atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE.  
  
 Las aplicaciones pueden establecer el atributo SQL_ATTR_ASYNC_DBC_EVENT en un identificador de conexión ODBC antes de llamar a una función de conexión (**SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect**). Dado que el Administrador de controladores ODBC no sabe qué controlador ODBC usará la aplicación, devolverá SQL_SUCCESS. Cuando la aplicación llama a una función de conexión, el Administrador de controladores ODBC comprobará si el controlador admite la notificación asincrónica. Si el controlador no admite la notificación asincrónica, el Administrador de controladores ODBC devolverá SQL_ERROR con SQLSTATE S1_118 (el controlador no admite la notificación asincrónica). Si el controlador admite la notificación asincrónica, el Administrador de controladores ODBC llamará al controlador y establecerá los atributos correspondientes SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK y SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT.  
  
 De forma similar, una aplicación llama a **SQLSetStmtAttr** en un identificador de instrucción ODBC y especifica el atributo SQL_ATTR_ASYNC_STMT_EVENT para habilitar o deshabilitar la notificación asincrónica de nivel de instrucción. Dado que siempre se llama a una función de instrucción después de establecer la conexión, **SQLSetStmtAttr** devolverá SQL_ERROR con SQLSTATE S1_118 (Driver no admite la notificación asincrónica) inmediatamente si el controlador correspondiente no admite operaciones asincrónicas o el controlador admite la operación asincrónica, pero no admite la notificación asincrónica.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT, que se puede establecer en NULL, es un atributo solo del Administrador de controladores que no se establecerá en el controlador.  
  
 El valor predeterminado de SQL_ATTR_ASYNC_STMT_EVENT es NULL. Si el controlador no admite la notificación asincrónica, obtener o establecer el SQL_ATTR_ASYNC_ STMT_EVENT atributo devolverá SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido).  
  
 Una aplicación no debe asociar el mismo identificador de evento con más de un identificador ODBC. De lo contrario, se perderá una notificación si se completan dos invocaciones de función ODBC asincrónicas en dos identificadores que comparten el mismo identificador de evento. Para evitar que un identificador de instrucción herede el mismo identificador de evento del identificador de conexión, ODBC devuelve SQL_ERROR con SQLSTATE IM016 (No se puede establecer el atributo de instrucción en el identificador de conexión) si una aplicación establece SQL_ATTR_ASYNC_STMT_EVENT en un identificador de conexión.  
  
### <a name="calling-asynchronous-odbc-functions"></a>Llamar a funciones ODBC asincrónicas  
 Después de habilitar la notificación asincrónica e iniciar una operación asincrónica, la aplicación puede llamar a cualquier función ODBC. Si la función pertenece al conjunto de funciones que admiten la operación asincrónica, la aplicación recibirá una notificación de finalización cuando se complete la operación, independientemente de si la función ha fallado o se ha realizado correctamente.  La única excepción es que la aplicación llama a una función ODBC con una conexión no válida o identificador de instrucción. En este caso, ODBC no obtendrá el identificador de evento y lo establecerá en el estado señalado.  
  
 La aplicación debe asegurarse de que el objeto de evento asociado está en un estado no señalizado antes de iniciar una operación asincrónica en el identificador ODBC correspondiente. ODBC no restablecerá el objeto de evento.  
  
### <a name="getting-notification-from-odbc"></a>Recibir notificaciones desde ODBC  
 Un subproceso de aplicación puede llamar a **WaitForSingleObject** para esperar en un identificador de evento o llamar a **WaitForMultipleObjects** para esperar en una matriz de identificadores de eventos y suspenderse hasta que uno o todos los objetos de evento se señalen o transcurra el intervalo de tiempo de espera.  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```
