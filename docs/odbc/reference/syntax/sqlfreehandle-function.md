---
title: Función SQLFreeHandle (SQLFreeHandle) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b136dec98a19676aa67c78615d8fe931f62aafa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285776"
---
# <a name="sqlfreehandle-function"></a>Función SQLFreeHandle
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLFreeHandle** libera los recursos asociados a un entorno específico, conexión, instrucción o identificador de descriptor.  
  
> [!NOTE]
>  Esta función es una función genérica para liberar identificadores. Reemplaza las funciones ODBC 2.0 **SQLFreeConnect** (para liberar un identificador de conexión) y **SQLFreeEnv** (para liberar un identificador de entorno). **SQLFreeConnect** y **SQLFreeEnv** están en desuso en ODBC 3 *.x*. **SQLFreeHandle** también reemplaza la función ODBC 2.0 **SQLFreeStmt** (con la *opción*SQL_DROP ) para liberar un identificador de instrucción. Para obtener más información, consulte "Comentarios." Para obtener más información acerca de a qué asigna el Administrador de controladores esta función cuando una aplicación ODBC 3 *.x* está trabajando con un controlador ODBC 2 *.x,* vea Asignación de funciones de [reemplazo para la compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] El tipo de identificador que va a liberar **SQLFreeHandle**. Debe ser uno de los siguientes valores:   
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN identificador solo lo utilizan el Administrador de controladores y el controlador. Las aplicaciones no deben usar este tipo de identificador. Para obtener más información acerca de SQL_HANDLE_DBC_INFO_TOKEN, vea Desarrollar el reconocimiento de grupos [de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 Si *HandleType* no es uno de estos valores, **SQLFreeHandle** devuelve SQL_INVALID_HANDLE.  
  
 *Handle*  
 [Entrada] El mango que se va a liberar.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_ERROR o SQL_INVALID_HANDLE.  
  
 Si **SQLFreeHandle** devuelve SQL_ERROR, el identificador sigue siendo válido.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLFreeHandle** devuelve SQL_ERROR, se puede obtener un valor SQLSTATE asociado de la estructura de datos de diagnóstico para el identificador que **SQLFreeHandle** intentó liberar pero no pudo. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLFreeHandle** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) el *HandleType* argumento era SQL_HANDLE_ENV y al menos una conexión estaba en un estado asignado o conectado. **SQLDisconnect** y **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC debe llamarse para cada conexión antes de llamar a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV.<br /><br /> (DM) el *HandleType* argumento se SQL_HANDLE_DBC y se llamó a la función antes de llamar a **SQLDisconnect** para la conexión.<br /><br /> (DM) el *HandleType* argumento fue SQL_HANDLE_DBC. Se llamó a una función de ejecución asincrónica con *Handle* y la función todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) El *HandleType* argumento fue SQL_HANDLE_STMT. **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó con el identificador de instrucción y SQL_NEED_DATA devuelto. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) El *HandleType* argumento fue SQL_HANDLE_STMT. Se llamó a una función de ejecución asincrónica en el identificador de instrucción o en el identificador de conexión asociado y la función todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) El *HandleType* argumento se SQL_HANDLE_DESC. Se llamó a una función de ejecución asincrónica en el identificador de conexión asociado; y la función todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) Todos los identificadores de subsidiaria y otros recursos no se liberaron antes de **sqlFreeHandle** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *Handle* y *HandleType* se estableció en SQL_HANDLE_STMT o SQL_HANDLE_DESC devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|El *HandleType* argumento era SQL_HANDLE_STMT o SQL_HANDLE_DESC y la llamada de función no se pudo procesar porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de memoria baja.|  
|HY017|Uso no válido de un identificador de descriptor asignado automáticamente.|(DM) El *Handle* argumento se estableció en el identificador de un descriptor asignado automáticamente.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) el *HandleType* argumento era SQL_HANDLE_DESC y el controlador era un controlador ODBC 2 *.x.*<br /><br /> (DM) el *HandleType* argumento era SQL_HANDLE_STMT y el controlador no era un controlador ODBC válido.|  
  
## <a name="comments"></a>Comentarios  
 **SQLFreeHandle** se utiliza para liberar identificadores para entornos, conexiones, instrucciones y descriptores, como se describe en las secciones siguientes. Para obtener información general acerca de los identificadores, vea [Handles](../../../odbc/reference/develop-app/handles.md).  
  
 Una aplicación no debe utilizar un identificador después de que se haya liberado; el Administrador de controladores no comprueba la validez de un identificador en una llamada de función.  
  
## <a name="freeing-an-environment-handle"></a>Liberar una manija ambiental  
 Antes de llamar a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV, una aplicación debe llamar a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC para todas las conexiones asignadas en el entorno. De lo contrario, la llamada a **SQLFreeHandle** devuelve SQL_ERROR y el entorno y cualquier conexión activa sigue siendo válida. Para obtener más información, consulte [Controldeación](../../../odbc/reference/develop-app/environment-handles.md) del entorno y [Asignación del controlador](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)de entorno .  
  
 Si el entorno es un entorno compartido, la aplicación que llama a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV ya no tiene acceso al entorno después de la llamada, pero los recursos del entorno no se liberan necesariamente. La llamada a **SQLFreeHandle** reduce el recuento de referencias del entorno. El Administrador de controladores mantiene el recuento de referencias. Si no llega a cero, el entorno compartido no se libera, porque todavía está siendo utilizado por otro componente. Si el recuento de referencias llega a cero, se liberan los recursos del entorno compartido.  
  
## <a name="freeing-a-connection-handle"></a>Liberación de una manija de conexión  
 Antes de llamar a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC, una aplicación debe llamar a **SQLDisconnect** para la conexión si hay una conexión en este identificador *.* De lo contrario, la llamada a **SQLFreeHandle** devuelve SQL_ERROR y la conexión sigue siendo válida.  
  
 Para obtener más información, vea [Controladores](../../../odbc/reference/develop-app/connection-handles.md) de conexión y [desconexión de un origen](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)de datos o controlador .  
  
## <a name="freeing-a-statement-handle"></a>Liberar un identificador de instrucción  
 Una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT libera todos los recursos asignados por una llamada a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_STMT. Cuando una aplicación llama a **SQLFreeHandle** para liberar una instrucción que tiene resultados pendientes, se eliminan los resultados pendientes. Cuando una aplicación libera un identificador de instrucción, el controlador libera los cuatro descriptores asignados automáticamente asociados a ese identificador. Para obtener más información, vea [Controldeación](../../../odbc/reference/develop-app/statement-handles.md) de instrucciones y [Liberación de un identificador](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)de instrucción .  
  
 Tenga en cuenta que **SQLDisconnect** quita automáticamente las instrucciones y descriptores abiertos en la conexión.  
  
## <a name="freeing-a-descriptor-handle"></a>Liberar una manija descriptora  
 Una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC libera el identificador de descriptor en *Handle*. La llamada a **SQLFreeHandle** no libera ninguna memoria asignada por la aplicación a la que pueda hacer referencia un campo de puntero (incluidos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR) de cualquier registro descriptor de *Handle*. La memoria asignada por el controlador para los campos que no son campos de puntero se libera cuando se libera el identificador. Cuando se libera un identificador de descriptor asignado por el usuario, todas las instrucciones que el identificador liberado se había asociado con la reversión a sus respectivos identificadores de descriptor asignados automáticamente.  
  
> [!NOTE]
>  Los controladores *.x* de ODBC 2 no admiten controladores de descriptor de liberación, del igual que no admiten la asignación de identificadores de descriptor.  
  
 Tenga en cuenta que **SQLDisconnect** quita automáticamente las instrucciones y descriptores abiertos en la conexión. Cuando una aplicación libera un identificador de instrucción, el controlador libera todos los descriptores generados automáticamente asociados a ese identificador.  
  
 Para obtener más información acerca de los descriptores, consulte [Descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Para obtener ejemplos de código adicionales, vea [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) y [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
### <a name="code"></a>Código  
  
```cpp  
// SQLFreeHandle.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <stdio.h>  
  
int main() {  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   // Initialize the environment, connection, statement handles.  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   // Allocate the environment.  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set environment attributes.  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
  
   // Allocate the connection.  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Set the login timeout.  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
  
   // Let the user select the data source and connect to the database.  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Free handles, and disconnect.     
   if (hstmt) {   
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
      hstmt = NULL;   
   }  
   if (hdbc) {   
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      hdbc = NULL;   
   }  
   if (henv) {   
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
      henv = NULL;   
   }  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un asa|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Cancelación del procesamiento de extractos|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa de ejemplo de ODBC](../../../odbc/reference/sample-odbc-program.md)
