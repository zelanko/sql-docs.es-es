---
title: Función SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d853d843e7b2cf168516fa4007883f280029e53b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006229"
---
# <a name="sqlfreehandle-function"></a>Función SQLFreeHandle
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: ISO 92  
  
 **Resumen**  
 **SQLFreeHandle** libera los recursos asociados con un identificador específico del entorno, conexión, instrucción o descriptor.  
  
> [!NOTE]
>  Esta función es una función genérica de liberación de identificadores. Reemplaza las funciones ODBC 2.0 **SQLFreeConnect** (para liberar un identificador de conexión) y **SQLFreeEnv** (para liberar un identificador de entorno). **SQLFreeConnect** y **SQLFreeEnv** están desusadas en ODBC 3 *.x*. **SQLFreeHandle** también reemplaza la función ODBC 2.0 **SQLFreeStmt** (con el SQL_DROP *opción*) para liberar un identificador de instrucción. Para obtener más información, vea "Comentarios". Para obtener más información sobre lo que el Administrador de controladores se asigna esta función cuando una aplicación ODBC 3 *.x* aplicación funciona con un ODBC 2 *.x* controladores, consulte [asignación de funciones de reemplazo para hacia atrás Compatibilidad de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] El tipo de identificador que se liberen por **SQLFreeHandle**. Debe ser uno de los siguientes valores:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN se utiliza únicamente por el Administrador de controladores y el controlador. Las aplicaciones no deben usar este tipo de identificador. Para obtener más información sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desarrollar el conocimiento de grupo de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 Si *HandleType* no es uno de estos valores, **SQLFreeHandle** devuelva SQL_INVALID_HANDLE.  
  
 *Handle*  
 [Entrada] El identificador se va a liberar.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_ERROR o SQL_INVALID_HANDLE.  
  
 Si **SQLFreeHandle** devuelve SQL_ERROR, el identificador es válido aún.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLFreeHandle** devuelve SQL_ERROR, un valor SQLSTATE asociado puede obtenerse a partir de la estructura de datos de diagnóstico para el identificador que **SQLFreeHandle** intentó libre pero no se pudo. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLFreeHandle** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) el *HandleType* argumento era SQL_HANDLE_ENV y al menos una conexión se encontraba en un estado conectado o asignado. **SQLDisconnect** y **SQLFreeHandle** con un *HandleType* debe llamarse de SQL_HANDLE_DBC para cada conexión antes de llamar a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV.<br /><br /> (DM) el *HandleType* argumento era SQL_HANDLE_DBC y se llamó a la función antes de llamar a **SQLDisconnect** para la conexión.<br /><br /> (DM) el *HandleType* argumento era SQL_HANDLE_DBC. Se llamó a una función que se ejecuta de forma asincrónica con *controlar* y la función todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) el *HandleType* argumento era SQL_HANDLE_STMT. **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó con el identificador de instrucción y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) el *HandleType* argumento era SQL_HANDLE_STMT. Se llamó a una función ejecuta de forma asincrónica en el identificador de instrucción o en el identificador de conexión asociado y la función todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) el *HandleType* argumento era SQL_HANDLE_DESC. Se llamó a una función que se ejecuta de forma asincrónica en el identificador de conexión asociada; y la función todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) controla todos los distribuidores y otros recursos no se liberan antes **SQLFreeHandle** llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *controlar* y *HandleType* se ha establecido en SQL_HANDLE_STMT o SQL_HANDLE_DESC devuelve SQL_PARAM_DATA_AVAILABLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|El *HandleType* argumento era SQL_HANDLE_STMT o SQL_HANDLE_DESC y no se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY017|Uso no válido de un identificador de descriptor asignado automáticamente.|(DM) el *controlar* argumento se estableció en el identificador de un descriptor asignado automáticamente.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el *HandleType* argumento era SQL_HANDLE_DESC y el controlador era un ODBC 2 *.x* controlador.<br /><br /> (DM) el *HandleType* argumento era SQL_HANDLE_STMT y el controlador no era un controlador ODBC válido.|  
  
## <a name="comments"></a>Comentarios  
 **SQLFreeHandle** se usa para liberar los identificadores para los entornos, las conexiones, instrucciones y los descriptores de, como se describe en las secciones siguientes. Para obtener información general acerca de los identificadores, vea [identificadores](../../../odbc/reference/develop-app/handles.md).  
  
 Una aplicación no debe utilizar un identificador después de que se haya liberado; el Administrador de controladores no comprueba la validez de un controlador en una llamada de función.  
  
## <a name="freeing-an-environment-handle"></a>Liberar un identificador de entorno  
 Antes de llamar a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV, una aplicación debe llamar a **SQLFreeHandle** con un *HandleType*de SQL_HANDLE_DBC para todas las conexiones que se asignan en el entorno. En caso contrario, la llamada a **SQLFreeHandle** devuelve SQL_ERROR y el entorno y ninguna conexión activa sigue siendo válida. Para obtener más información, consulte [controla el entorno](../../../odbc/reference/develop-app/environment-handles.md) y [asignar el entorno de controlar](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Si el entorno es un entorno compartido, la aplicación que llama **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV ya no tiene acceso para el entorno después de la llamada, pero el entorno recursos no se liberan necesariamente. La llamada a **SQLFreeHandle** disminuye el recuento de referencias del entorno. El recuento de referencias se mantiene mediante el Administrador de controladores. Si no llegue a cero, no se libera el entorno compartido, porque aún se está usando otro componente. Si el recuento de referencias llega a cero, se liberan los recursos del entorno compartido.  
  
## <a name="freeing-a-connection-handle"></a>Liberar un identificador de conexión  
 Antes de llamar a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC, una aplicación debe llamar a **SQLDisconnect** para la conexión si hay una conexión en este controlar *.* En caso contrario, la llamada a **SQLFreeHandle** devuelve SQL_ERROR y la conexión sigue siendo válida.  
  
 Para obtener más información, consulte [conexión controla](../../../odbc/reference/develop-app/connection-handles.md) y [desconectarse de un origen de datos o un controlador](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="freeing-a-statement-handle"></a>Liberar un identificador de instrucción  
 Una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT libera todos los recursos asignados por una llamada a **SQLAllocHandle** con un  *HandleType* de SQL_HANDLE_STMT. Cuando una aplicación llama **SQLFreeHandle** para liberar una instrucción que tiene resultados pendientes, se eliminan los resultados pendientes. Cuando una aplicación libera un identificador de instrucción, el controlador libera los descriptores asignados automáticamente cuatro asociados con ese identificador. Para obtener más información, consulte [instrucción controla](../../../odbc/reference/develop-app/statement-handles.md) y [liberar un identificador de instrucciones](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 Tenga en cuenta que **SQLDisconnect** quita automáticamente las declaraciones y los descriptores de abierto en la conexión.  
  
## <a name="freeing-a-descriptor-handle"></a>Liberar un identificador de Descriptor  
 Una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC libera el identificador de descriptor en *controlar*. La llamada a **SQLFreeHandle** no libera memoria asignada por la aplicación que puede hacer referencia a un campo de puntero (incluido SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR) de cualquiera registro del descriptor de *controlar*. Cuando se libere el identificador, se libera la memoria asignada por el controlador para los campos que no son campos de puntero. Cuando se libera un identificador de descriptor asignado por el usuario, todas las instrucciones que había se ha asociado el identificador liberado se vuelven a sus identificadores respectivos descriptor asignado automáticamente.  
  
> [!NOTE]
>  ODBC 2 *.x* controladores no admiten identificadores de descriptor de liberación, igual que no admiten la asignación de identificadores de descriptor.  
  
 Tenga en cuenta que **SQLDisconnect** quita automáticamente las declaraciones y los descriptores de abierto en la conexión. Cuando una aplicación libera un identificador de instrucción, el controlador libera todos los descriptores de generado automáticamente asociados con ese identificador.  
  
 Para obtener más información acerca de los descriptores, consulte [descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Para obtener ejemplos de código adicional, vea [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) y [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
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
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Procesamiento de una instrucción de cancelación|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa de ejemplo de ODBC](../../../odbc/reference/sample-odbc-program.md)
