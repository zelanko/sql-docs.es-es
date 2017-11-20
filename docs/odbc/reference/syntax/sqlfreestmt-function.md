---
title: "Función SQLFreeStmt | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 929fc50091c914936b5bedfb58bd42c1d07d99ab
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-function"></a>Función SQLFreeStmt
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLFreeStmt** detiene el procesamiento asociado con una instrucción concreta, cierra los cursores abiertos asociados con la instrucción, descarta los resultados pendientes o, de forma opcional, libera todos los recursos asociados con el identificador de instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción  
  
 *Opción*  
 [Entrada] Una de las siguientes opciones:  
  
 SQL_ cerrar: Cierra el cursor asociado con *StatementHandle* (si se ha definido uno) y descarta todos los resultados pendientes. La aplicación puede volver a abrir este cursor más adelante mediante la ejecución de un **seleccione** instrucción nuevo con los valores de parámetro iguales o distintos. Si ningún cursor está abierto, esta opción no tiene ningún efecto sobre la aplicación. **SQLCloseCursor** también se puede llamar para cerrar un cursor. Para obtener más información, consulte [cerrar el Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 SQL_DROP: Esta opción está en desuso. Una llamada a **SQLFreeStmt** con una *opción* de SQL_DROP se asigna en el Administrador de controladores a [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
 SQL_UNBIND: Establece el campo SQL_DESC_COUNT de la descartar en 0, liberar todos los búferes de columna enlazada por **SQLBindCol** para la dada *StatementHandle*. Esto no desenlaza la columna de marcador; Para ello, el campo SQL_DESC_DATA_PTR de la Descartar para la columna de marcador se establece en NULL. Tenga en cuenta que si esta operación se realiza en un descriptor asignado explícitamente que se comparte por más de una instrucción, la operación afectará a los enlaces de todas las instrucciones que comparten el descriptor. Para obtener más información, consulte [resúmenes de recuperación de los resultados (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 SQL_RESET_PARAMS: Establece el campo SQL_DESC_COUNT de la APD en 0, liberar todos los búferes de parámetros establecidos por **SQLBindParameter** para la dada *StatementHandle*. Si esta operación se realiza en un descriptor asignado explícitamente que se comparte por más de una instrucción, esta operación afectará a los enlaces de todas las instrucciones que comparten el descriptor. Para obtener más información, consulte [enlazar parámetros](../../../odbc/reference/develop-app/binding-parameters-odbc.md).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLFreeStmt** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLFreeStmt** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando **SQLFreeStmt** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca con *opción* establecido en SQL_RESET_PARAMS antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY092|Tipo de opción fuera del intervalo|(DM) el valor especificado para el argumento *opción* no era:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Al llamar a **SQLFreeStmt** con el SQL_CLOSE opción es equivalente a llamar a **SQLCloseCursor**, salvo que **SQLFreeStmt** con SQL_CLOSE no afecta a la aplicación Si ningún cursor está abierto en la instrucción. Si ningún cursor está abierto, una llamada a **SQLCloseCursor** devuelve SQLSTATE 24000 (estado de cursor no válido).  
  
 Una aplicación no debe utilizar un identificador de instrucción después de haberla liberado; el Administrador de controladores no comprueba la validez de un identificador en una llamada de función.  
  
## <a name="example"></a>Ejemplo  
 Es una buena práctica de programación para liberar los identificadores. Sin embargo, para simplificar, el ejemplo siguiente no incluye código que libera asignada identificadores. Para obtener un ejemplo de cómo liberar identificadores, vea [SQLFreeHandle, función](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
```  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador|[SQLAllocHandle, función](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Cerrar un cursor|[SQLCloseCursor, función](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Liberar un identificador|[SQLFreeHandle, función](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Establecer un nombre de cursor|[SQLSetCursorName, función](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

