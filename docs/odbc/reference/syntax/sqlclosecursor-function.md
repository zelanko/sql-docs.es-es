---
title: "SQLCloseCursor, función | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0921de0c8bc117ca86f4aaabd273efff1f09a9e6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlclosecursor-function"></a>SQLCloseCursor, función
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLCloseCursor** cierra un cursor que se ha abierto en una instrucción y se descarta los resultados pendientes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLCloseCursor** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL _HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLCloseCursor** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|24000|Estado de cursor no válido|Ningún cursor estaba abierto en el *StatementHandle*. (Se devuelve solo por una aplicación ODBC 3. *x* controlador.)|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión asociado a la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el * StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 **SQLCloseCursor** devuelve SQLSTATE 24000 (estado de cursor no válido) si ningún cursor está abierto. Al llamar a **SQLCloseCursor** equivale a llamar a **SQLFreeStmt** con la opción de SQL_CLOSE, con la excepción que **SQLFreeStmt** con SQL_CLOSE no tiene ningún efecto el aplicación si ningún cursor está abierto en la instrucción, mientras que **SQLCloseCursor** devuelve SQLSTATE 24000 (estado de cursor no válido).  
  
> [!NOTE]  
>  Si está un ODBC 3. *x* aplicación trabajar con una API ODBC 2.* x* controlador llama **SQLCloseCursor** cuando ningún cursor está abierto, no se devuelve SQLSTATE 24000 (estado de cursor no válido), porque el Administrador de controladores se asignan **SQLCloseCursor** a **SQLFreeStmt** con SQL_CLOSE.  
  
 Para obtener más información, consulte [cerrar el Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) y [SQLConnect, función](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Liberar un identificador|[SQLFreeHandle, función](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Procesar varios conjuntos de resultados|[SQLMoreResults (función)](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

