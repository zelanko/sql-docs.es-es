---
title: Ejecución asincrónica (método de notificación) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6aa634f154eb0594c76ae7e65b8d237175a3f92e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288517"
---
# <a name="asynchronous-execution-notification-method"></a>Ejecución asincrónica (método de notificación)
ODBC permite la ejecución asincrónica de conexión y las operaciones de la instrucción. Un subproceso de la aplicación puede llamar a una función ODBC en modo asincrónico y devolver la función antes de que la operación se completa, lo que permite al subproceso de la aplicación realizar otras tareas. En el SDK de Windows 7, para la instrucción asincrónica o las operaciones de conexión, una aplicación determinó que la operación asincrónica se completa mediante el método de sondeo. Para obtener más información, consulte [ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). A partir de Windows 8 SDK, puede determinar que una operación asincrónica está completa mediante el método de notificación.  
  
 En el método de sondeo, las aplicaciones deben llamar a la función asincrónica cada vez que desea que el estado de la operación. El método de notificación es similar a la devolución de llamada y espera en ADO.NET. Sin embargo, ODBC, usa eventos de Win32 como el objeto de notificación.  
  
 La biblioteca de cursores ODBC y la notificación asincrónica de ODBC no se puede usar al mismo tiempo. Configurar ambos atributos, se devolverá un error con SQLSTATE S1119 (biblioteca de cursores y la notificación asincrónica no se puede habilitar al mismo tiempo).  
  
 Consulte [notificación de finalización asincrónica de función](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) para obtener información para desarrolladores de controladores.  
  
> [!NOTE]  
>  El método de notificación no es compatible con la biblioteca de cursores. Una aplicación recibirá el mensaje de error si intenta habilitar la biblioteca de cursores a través de SQLSetConnectAttr, cuando el método de notificación está habilitado.  
  
## <a name="overview"></a>Información general  
 Cuando se llama a una función ODBC en modo asincrónico, el control se devuelve a la aplicación que realiza la llamada inmediatamente con el código de retorno SQL_STILL_EXECUTING. La aplicación debe sondear repetidamente la función hasta que devuelve un valor distinto de SQL_STILL_EXECUTING. El bucle de sondeo aumenta la utilización de CPU, lo que provoca un bajo rendimiento en muchos escenarios asincrónicos.  
  
 Cada vez que se usa el modelo de notificación, el modelo de sondeo está deshabilitado. Las aplicaciones no deben llamar nuevamente a la función original. Llame a [función SQLCompleteAsync](../../../odbc/reference/syntax/sqlcompleteasync-function.md) para completar la operación asincrónica. Si una aplicación llama a la función original antes de la operación asincrónica se complete, la llamada devolverá SQL_ERROR con SQLSTATE IM017 (sondeo está deshabilitado en el modo asincrónico de notificación).  
  
 Cuando se usa el modelo de notificación, la aplicación puede llamar a **SQLCancel** o **SQLCancelHandle** para cancelar una operación de conexión o instrucción. Si la solicitud de cancelación se realiza correctamente, devuelve SQL_SUCCESS ODBC. Este mensaje no indica que la función se ha cancelado realmente; indica que se procesó la solicitud de cancelación. Si realmente se cancela la función es dependiente del controlador y depende del origen de datos. Cuando se cancela una operación, el Administrador de controladores todavía señalará el evento. El Administrador de controladores devuelve SQL_ERROR en el búfer de código de retorno y el estado es HY008 SQLSTATE (operación cancelada) para indicar la cancelación es correcta. Si la función de completa su procesamiento normal, el Administrador de controladores devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
### <a name="downlevel-behavior"></a>Comportamiento de nivel inferior  
 La versión del Administrador de controladores ODBC que admiten esta notificación en completa es 3.81 de ODBC.  
  
|Versión de la aplicación ODBC|Versión del Administrador de controladores|Versión del controlador|Comportamiento|  
|------------------------------|----------------------------|--------------------|--------------|  
|Nueva aplicación de cualquier versión ODBC|ODBC 3.81|3,80 ODBC Driver|Aplicación puede utilizar esta característica si el controlador admite esta característica, en caso contrario, el Administrador de controladores generará un error.|  
|Nueva aplicación de cualquier versión ODBC|ODBC 3.81|Controlador ODBC de pre 3,80|El Administrador de controladores generará un error si el controlador no admite esta característica.|  
|Nueva aplicación de cualquier versión ODBC|3\.81 pre-ODBC|Cualquiera|Cuando la aplicación usa esta característica, un administrador de controladores antiguos considerará los nuevos atributos como atributos específicos del controlador y el controlador debe el error. Un nuevo administrador de controladores no pasará estos atributos para el controlador.|  
  
 Una aplicación debe comprobar la versión del Administrador de controladores antes de usar esta característica. En caso contrario, si un controlador mal escrito no producirá ningún error y la versión del Administrador de controladores es anterior a ODBC 3.81, comportamiento es indefinido.  
  
## <a name="use-cases"></a>Casos de uso  
 Esta sección muestra los casos de uso de la ejecución asincrónica y el mecanismo de sondeo.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>Integrar datos de varios orígenes ODBC  
 Una aplicación de integración de datos captura asincrónicamente los datos de varios orígenes de datos. Algunos de los datos proceden de orígenes de datos remotos y algunos datos proceden de archivos locales. La aplicación no puede continuar hasta que se completen las operaciones asincrónicas.  
  
 En lugar de sondear repetidamente una operación para determinar si se ha completado, la aplicación puede crear un objeto de evento y asociarlo con un identificador de conexión ODBC o un identificador de instrucción ODBC. A continuación, la aplicación llama a la API para esperar en el objeto de evento de uno o muchos objetos de eventos (eventos ODBC y otros eventos de Windows) de la sincronización del sistema operativo. ODBC señalará el objeto de evento cuando se completa la operación asincrónica de ODBC correspondiente.  
  
 En Windows, los objetos de evento de Win32 que se usará y que proporcionará al usuario un modelo de programación unificado. Los administradores de controlador en otras plataformas pueden usar la implementación de objeto de evento específica para estas plataformas.  
  
 Ejemplo de código siguiente muestra el uso de la conexión y la notificación asincrónica de instrucción:  
  
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
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>Determinar si un controlador es compatible con la notificación asincrónica  
 Una aplicación ODBC puede determinar si un controlador ODBC admite la notificación asincrónica mediante una llamada a [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md). El Administrador de controladores ODBC llamará en consecuencia el **SQLGetInfo** del controlador con SQL_ASYNC_NOTIFICATION.  
  
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
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Asociar un identificador de evento de Win32 con un controlador de ODBC  
 Las aplicaciones son responsables de crear objetos de evento de Win32 con las funciones de Win32 correspondientes. Una aplicación puede asociar un identificador de evento de Win32 con un identificador de conexión de ODBC o un identificador de instrucción ODBC.  
  
 Los atributos de conexión SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE y SQL_ATTR_ASYNC_DBC_EVENT determinan si ODBC se ejecuta en modo asincrónico y si ODBC habilita el modo de notificación para un identificador de conexión. Los atributos de instrucción SQL_ATTR_ASYNC_ENABLE y SQL_ATTR_ASYNC_STMT_EVENT determinan si ODBC se ejecuta en modo asincrónico y si ODBC habilita el modo de notificación para un identificador de instrucción.  
  
|SQL_ATTR_ASYNC_ENABLE o SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT o SQL_ATTR_ASYNC_DBC_EVENT|Modo|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|Habilitar|distinto de null|Notificación asincrónica|  
|Habilitar|null|Asincrónico de sondeo|  
|Deshabilitar|cualquiera|Sincrónica|  
  
 Una aplicación puede deshabilitar temporalmente el modo de operación asincrónica. ODBC omite los valores de SQL_ATTR_ASYNC_DBC_EVENT si la operación asincrónica de nivel de conexión está deshabilitada. ODBC omite los valores de SQL_ATTR_ASYNC_STMT_EVENT si la operación asincrónica de nivel de instrucción está deshabilitada.  
  
 Llamada sincrónica de **SQLSetStmtAttr** y **SQLSetConnectAttr**  
 -   **SQLSetConnectAttr** admite operaciones asincrónicas, pero la invocación de **SQLSetConnectAttr** establecer SQL_ATTR_ASYNC_DBC_EVENT siempre es sincrónica.  
  
-   **SQLSetStmtAttr** no admite la ejecución asincrónica.  
  
 Escenario de error de salida  
 Cuando **SQLSetConnectAttr** se llama antes de realizar una conexión, el Administrador de controladores no se puede determinar qué controlador usar. Por lo tanto, el Administrador de controladores devuelve un valor correcto para **SQLSetConnectAttr** pero el atributo no puede estar listo para establecer en el controlador. El Administrador de controladores establecerá estos atributos cuando la aplicación llama a una función de la conexión. El Administrador de controladores posible error de salida porque el controlador no admite operaciones asincrónicas.  
  
 Herencia de atributos de conexión  
 Por lo general, las instrucciones de una conexión heredará los atributos de conexión. Sin embargo, el atributo SQL_ATTR_ASYNC_DBC_EVENT no se puede heredar y solo afecta a las operaciones de conexión.  
  
 Para asociar un controlador de eventos con un identificador de conexión ODBC, una aplicación ODBC llama a la API de ODBC **SQLSetConnectAttr** y especifica SQL_ATTR_ASYNC_DBC_EVENT como controlan el atributo y el evento como el valor del atributo. El nuevo atributo ODBC SQL_ATTR_ASYNC_DBC_EVENT es de tipo SQL_IS_POINTER.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 Por lo general, las aplicaciones crean objetos de evento de restablecimiento automático. ODBC no restablece el objeto de evento. Las aplicaciones deben asegurarse de que el objeto no está en estado señalado antes de llamar a cualquier función ODBC asincrónica.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT es un atributo de sólo administrador de controladores que no se establecerán en el controlador.  
  
 El valor predeterminado de SQL_ATTR_ASYNC_DBC_EVENT es NULL. Si el controlador no admite la notificación asincrónica, obtener o establecer SQL_ATTR_ASYNC_DBC_EVENT devolverá SQL_ERROR con SQLSTATE HY092 (identificador de opción o atributo no válido).  
  
 Si el último valor SQL_ATTR_ASYNC_DBC_EVENT se establece en un identificador de conexión de ODBC no es NULL y la aplicación habilitado modo asincrónico, establezca el atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE con SQL_ASYNC_DBC_ENABLE_ON, llamar a cualquier conexión de ODBC función que admite el modo asincrónico recibirá una notificación de finalización. Si el último valor SQL_ATTR_ASYNC_DBC_EVENT establecido en un identificador de conexión de ODBC es NULL, ODBC no enviará la aplicación ninguna notificación, independientemente de si está habilitado el modo asincrónico.  
  
 Una aplicación puede establecer SQL_ATTR_ASYNC_DBC_EVENT antes o después de establecer el atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE.  
  
 Las aplicaciones pueden establecer el atributo SQL_ATTR_ASYNC_DBC_EVENT en un identificador de conexión de ODBC antes de llamar a una función de conexión (**SQLConnect**, **SQLBrowseConnect**, o  **SQLDriverConnect**). Dado que el Administrador de controladores ODBC no sabe qué controlador ODBC que se va a utilizar la aplicación, devolverá SQL_SUCCESS. Cuando la aplicación llama a una función de conexión, el Administrador de controladores ODBC comprobará si el controlador admite la notificación asincrónica. Si el controlador no admite la notificación asincrónica, el Administrador de controladores ODBC devuelve SQL_ERROR con SQLSTATE S1_118 (el controlador no admite la notificación asincrónica). Si el controlador admite la notificación asincrónica, el Administrador de controladores ODBC llamará a los controladores y establecer los atributos correspondientes SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK y SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT.  
  
 De forma similar, una aplicación llama a **SQLSetStmtAttr** en una instrucción ODBC controlar y especifica el atributo SQL_ATTR_ASYNC_STMT_EVENT para habilitar o deshabilitar la notificación asincrónica de nivel de instrucción. Dado que una función de instrucción siempre se llama una vez establecida la conexión, **SQLSetStmtAttr** devolverá SQL_ERROR con SQLSTATE S1_118 (el controlador no admite la notificación asincrónica) inmediatamente si correspondiente controlador no admite operaciones asincrónicas o el controlador admite la operación asincrónica, pero no admite la notificación asincrónica.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT, que se puede establecer en NULL, es un atributo de sólo administrador de controladores que no se establecerán en el controlador.  
  
 El valor predeterminado de SQL_ATTR_ASYNC_STMT_EVENT es NULL. Si el controlador no admite la notificación asincrónica, obtener o establecer el atributo SQL_ATTR_ASYNC_ STMT_EVENT devolverá SQL_ERROR con SQLSTATE HY092 (identificador de opción o atributo no válido).  
  
 Una aplicación no debe asociar el mismo identificador de evento con más de un controlador de ODBC. En caso contrario, una notificación se perderán si dos llamadas a funciones ODBC asincrónicas se completa en dos puntos de control que comparten el mismo identificador de evento. Para evitar un identificador de instrucción heredar el identificador de conexión en el mismo identificador de evento, ODBC devuelve SQL_ERROR con IM016 SQLSTATE (no se puede establecer el atributo de instrucción en el identificador de conexión) si una aplicación establece SQL_ATTR_ASYNC_STMT_EVENT en un identificador de conexión.  
  
### <a name="calling-asynchronous-odbc-functions"></a>Llamar a funciones ODBC asincrónica  
 Después de habilitar la notificación asincrónica e iniciar una operación asincrónica, la aplicación puede llamar a cualquier función ODBC. Si la función pertenece al conjunto de funciones que admiten la operación asincrónica, la aplicación obtendrá una notificación de finalización cuando se complete la operación, independientemente de si la función error o se ha realizado correctamente.  La única excepción es que la aplicación llama a una función ODBC con un identificador de conexión o instrucción no válido. En este caso, ODBC no obtener el identificador de evento y establézcala en el estado señalado.  
  
 La aplicación debe asegurarse de que el objeto de evento asociado está en un estado no señalado antes de iniciar una operación asincrónica en el controlador ODBC correspondiente. ODBC no restablece el objeto de evento.  
  
### <a name="getting-notification-from-odbc"></a>Obtener una notificación de ODBC  
 Puede llamar un subproceso de aplicación **WaitForSingleObject** para esperar en la llamada o identificador de un evento **WaitForMultipleObjects** para esperar en una matriz de identificadores de evento y se suspende hasta que uno o todos los objetos de evento se señala o transcurre el intervalo de tiempo de espera.  
  
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
