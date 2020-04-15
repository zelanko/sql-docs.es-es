---
title: Función SQLRowCount ? Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cbca03e7c3e381b803196a1bf7bb227ebeea03b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293375"
---
# <a name="sqlrowcount-function"></a>Función SQLRowCount
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLRowCount** devuelve el número de filas afectadas por una instrucción **UPDATE**, **INSERT**o **DELETE;** una operación SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK en **SQLBulkOperations**; o una operación de SQL_UPDATE o SQL_DELETE en **SQLSetPos**.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *RowCountPtr*  
 [Salida] Apunta a un búfer en el que se devuelve un recuento de filas. Para las instrucciones **UPDATE**, **INSERT**y **DELETE,** para las operaciones SQL_ADD, SQL_UPDATE_BY_BOOKMARK y SQL_DELETE_BY_BOOKMARK en **SQLBulkOperations**y para las operaciones SQL_UPDATE o SQL_DELETE en **SQLSetPos**, el valor devuelto en **RowCountPtr* es el número de filas afectadas por la solicitud o -1 si el número de filas afectadas no está disponible.  
  
 Cuando **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos, o SQLMoreResults** se llama, el campo SQL_DIAG_ROW_COUNT de la estructura de datos de diagnóstico se establece en el recuento de filas y el recuento de filas se almacena en caché de forma dependiente de la implementación. **SQLRowCount** devuelve el valor de recuento de filas almacenado en caché. El valor de recuento de filas almacenado en caché es válido hasta que el identificador de instrucción se establece de nuevo en el estado preparado o asignado, se vuelve a ejecutar la instrucción o **SQLCloseCursor** se llama. Tenga en cuenta que si se ha llamado a una función desde que se estableció el campo SQL_DIAG_ROW_COUNT, el valor devuelto por **SQLRowCount** podría ser diferente del valor del campo SQL_DIAG_ROW_COUNT porque el campo SQL_DIAG_ROW_COUNT se restablece a 0 mediante cualquier llamada de función.  
  
 Para otras instrucciones y funciones, el controlador \*puede definir el valor devuelto en *RowCountPtr*. Por ejemplo, algunos orígenes de datos pueden devolver el número de filas devueltas por una instrucción **SELECT** o una función de catálogo antes de capturar las filas.  
  
> [!NOTE]  
>  Muchos orígenes de datos no pueden devolver el número de filas de un conjunto de resultados antes de capturarlos; para lograr la máxima interoperabilidad, las aplicaciones no deben confiar en este comportamiento.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLRowCount** devuelve SQL_ERROR u SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLRowCount** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLRowCount.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) Se llamó a la función antes de llamar a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** para *StatementHandle*.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Si la última instrucción SQL ejecutada en el identificador de instrucción no era una instrucción **UPDATE**, **INSERT**o **DELETE,** o si el argumento *Operation* de la llamada anterior a **SQLBulkOperations** no era SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK, o si el argumento *Operation* de la llamada anterior a **SQLSetPos** no era SQL_UPDATE ni SQL_DELETE, el valor de **RowCountPtr* está definido por el controlador. Para obtener más información, consulte [Determinación del número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
