---
title: Función SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d48d9742f9b3fafe77f441226961218f47c6005
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719713"
---
# <a name="sqlfreestmt-function"></a>Función SQLFreeStmt
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: 92 ISO  
  
 **Resumen**  
 **SQLFreeStmt** detiene el procesamiento asociado con una instrucción concreta, cierra los cursores abiertos asociados con la instrucción, descarta los resultados pendientes o, de manera opcional, libera todos los recursos asociados con el identificador de instrucción.  
  
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
  
 SQL_ cerrar: Cierra el cursor asociado con *StatementHandle* (si se ha definido uno) y descarta todos los resultados pendientes. La aplicación puede volver a abrir este cursor más adelante mediante la ejecución de un **seleccione** instrucción nuevo con los valores de parámetro de la misma u otra. Si ningún cursor está abierto, esta opción no tiene efecto para la aplicación. **SQLCloseCursor** también se puede invocar para cerrar un cursor. Para obtener más información, consulte [cierre el Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 SQL_DROP: Esta opción es obsoleta. Una llamada a **SQLFreeStmt** con un *opción* de SQL_DROP se asigna en el Administrador de controladores a [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
 SQL_UNBIND: Establece el campo SQL_DESC_COUNT de la descartar en 0, liberando todos los búferes de columna enlazada por **SQLBindCol** para la dada *StatementHandle*. Esto desenlaza la columna de marcador; Para ello, el campo SQL_DESC_DATA_PTR de la Descartar para la columna de marcador se establece en NULL. Tenga en cuenta que si esta operación se realiza en un descriptor asignado explícitamente que se comparte por más de una instrucción, la operación afectará a los enlaces de todas las instrucciones que comparten el descriptor. Para obtener más información, consulte [información general de recuperar los resultados (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 SQL_RESET_PARAMS: Establece el campo SQL_DESC_COUNT del APD en 0, liberando todos los búferes de parámetros establecidos por **SQLBindParameter** para la dada *StatementHandle*. Si esta operación se realiza en un descriptor asignado explícitamente que se comparte por más de una instrucción, esta operación afectará a los enlaces de todas las instrucciones que comparten el descriptor. Para obtener más información, consulte [enlazar parámetros](../../../odbc/reference/develop-app/binding-parameters-odbc.md).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLFreeStmt** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLFreeStmt** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando **SQLFreeStmt** llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Se llamó a esta función con *opción* establecido en SQL_RESET_PARAMS antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY092|Tipo de opción fuera del intervalo|(DM) el valor especificado para el argumento *opción* no era:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una llamada a **SQLFreeStmt** con el SQL_CLOSE opción es equivalente a llamar a **SQLCloseCursor**, salvo que **SQLFreeStmt** con SQL_CLOSE no afecta a la aplicación Si el cursor no está abierto en la instrucción. Si ningún cursor está abierto, una llamada a **SQLCloseCursor** devuelve SQLSTATE 24000 (estado de cursor no válido).  
  
 Una aplicación no debe utilizar un identificador de instrucción después de que se haya liberado; el Administrador de controladores no comprueba la validez de un controlador en una llamada de función.  
  
## <a name="example"></a>Ejemplo  
 Es una buena práctica de programación para liberar los identificadores. Sin embargo, para simplificar, en el ejemplo siguiente no incluye código que libera asignada identificadores. Para obtener un ejemplo de cómo liberar identificadores, vea [función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
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
|Asignar un identificador|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Cerrar un cursor|[Función SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Liberar un identificador|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
