---
title: Función SQLFreeStmt (SQLFreeStmt) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e252769c26a5491100094b1243b9c2c6bb67d94d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285705"
---
# <a name="sqlfreestmt-function"></a>Función SQLFreeStmt
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLFreeStmt** detiene el procesamiento asociado a una instrucción específica, cierra los cursores abiertos asociados a la instrucción, descarta los resultados pendientes o, opcionalmente, libera todos los recursos asociados con el identificador de instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Manejo de la declaración  
  
 *Opción*  
 [Entrada] Una de las siguientes opciones:  
  
 SQL_ CLOSE: cierra el cursor asociado a *StatementHandle* (si se ha definido) y descarta todos los resultados pendientes. La aplicación puede volver a abrir este cursor más adelante ejecutando una instrucción **SELECT** de nuevo con los mismos o diferentes valores de parámetro. Si no hay ningún cursor abierto, esta opción no tiene ningún efecto para la aplicación. **SQLCloseCursor** también se puede llamar para cerrar un cursor. Para obtener más información, consulte [Cierre del cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 SQL_DROP: Esta opción está en desuso. Una llamada a **SQLFreeStmt** con una *opción* de SQL_DROP se asigna en el Administrador de controladores a [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
 SQL_UNBIND: establece el campo SQL_DESC_COUNT de LA ARD en 0, liberando todos los búferes de columna enlazados por **SQLBindCol** para el *StatementHandle*determinado . Esto no desvincula la columna de marcador; para ello, el campo SQL_DESC_DATA_PTR de la ARD para la columna de marcador se establece en NULL. Tenga en cuenta que si esta operación se realiza en un descriptor asignado explícitamente que es compartido por más de una instrucción, la operación afectará a los enlaces de todas las instrucciones que comparten el descriptor. Para obtener más información, consulte [Información general sobre la recuperación de resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 SQL_RESET_PARAMS: Establece el campo SQL_DESC_COUNT del APD en 0, liberando todos los búferes de parámetros establecidos por **SQLBindParameter** para el *StatementHandle*especificado . Si esta operación se realiza en un descriptor asignado explícitamente que es compartido por más de una instrucción, esta operación afectará a los enlaces de todas las instrucciones que comparten el descriptor. Para obtener más información, vea [Parámetros de enlace](../../../odbc/reference/develop-app/binding-parameters-odbc.md).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLFreeStmt** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLFreeStmt** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando **sqlFreeStmt** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Esta función se llamó con *Option* establecido en SQL_RESET_PARAMS antes de que se recuperaran los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY092|Tipo de opción fuera del rango|(DM) El valor especificado para el argumento *Opción* no era:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Llamar a **SQLFreeStmt** con la opción SQL_CLOSE equivale a llamar a **SQLCloseCursor**, excepto que **SQLFreeStmt** con SQL_CLOSE no afecta a la aplicación si no hay ningún cursor abierto en la instrucción. Si no hay ningún cursor abierto, una llamada a **SQLCloseCursor** devuelve SQLSTATE 24000 (estado de cursor no válido).  
  
 Una aplicación no debe usar un identificador de instrucción después de que se haya liberado; el Administrador de controladores no comprueba la validez de un identificador en una llamada de función.  
  
## <a name="example"></a>Ejemplo  
 Es una buena práctica de programación para liberar asas. Sin embargo, para simplificar, el ejemplo siguiente no incluye código que libera los identificadores asignados. Para obtener un ejemplo de cómo liberar identificadores, vea [SQLFreeHandle (función).](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
```cpp  
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
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un asa|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Cierre de un cursor|[Función SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Liberar un mango|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
