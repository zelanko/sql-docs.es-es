---
title: Función SQLRowCount | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 04a4e5061a80fec51361e82c57102df8e3fa34c8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlrowcount-function"></a>Función SQLRowCount
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLRowCount** devuelve el número de filas afectadas por un **actualización**, **insertar**, o **eliminar** instrucción; un SQL_ADD SQL_UPDATE_BY_BOOKMARK o SQL_ Operación de DELETE_BY_BOOKMARK en **SQLBulkOperations**; o una operación SQL_UPDATE o SQL_DELETE de **SQLSetPos**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *RowCountPtr*  
 [Salida] Señala a un búfer en el que se va a devolver un recuento de filas. Para **actualización**, **insertar**, y **eliminar** las instrucciones para las operaciones SQL_ADD, SQL_UPDATE_BY_BOOKMARK y SQL_DELETE_BY_BOOKMARK en  **SQLBulkOperations**y para las operaciones SQL_UPDATE o SQL_DELETE **SQLSetPos**, el valor devuelto en **RowCountPtr* es el número de filas afectadas por la solicitud o – 1 si el número de filas afectadas no está disponible.  
  
 Cuando **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos o SQLMoreResults** se llama, el SQL_DIAG_ROW_COUNT campo de la estructura de datos de diagnóstico está establecido en el recuento de filas y se almacena en caché el recuento de filas de una manera depende de la implementación. **SQLRowCount** devuelve el valor de número de fila en caché. El valor de número de fila en caché es válido hasta que el identificador de instrucción se vuelve a establecer el estado preparado o asignado, se vuelve a ejecutar la instrucción, o **SQLCloseCursor** se llama. Tenga en cuenta que si una función se ha llamado desde que se estableció el campo SQL_DIAG_ROW_COUNT, el valor devuelto por **SQLRowCount** puede variar desde el valor del campo SQL_DIAG_ROW_COUNT porque el campo SQL_DIAG_ROW_COUNT se restablece en 0 por cualquier llamada de función.  
  
 Para otras instrucciones y funciones, el controlador puede definir el valor devuelto en \* *RowCountPtr*. Por ejemplo, algunos orígenes de datos puede devolver el número de filas devueltas por una **seleccione** instrucción o una función de catálogo antes de capturar las filas.  
  
> [!NOTE]  
>  Muchos orígenes de datos no pueden devolver el número de filas en un conjunto de resultados antes descargarlas; Para obtener una interoperabilidad máxima, las aplicaciones no deben confiar en este comportamiento.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLRowCount** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLRowCount** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLRowCount** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llama a la función antes de llamar a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** para el  *StatementHandle*.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Si la última instrucción SQL ejecutada en el identificador de instrucción no era un **actualización**, **insertar**, o **eliminar** instrucción o si la *operación* argumento de la llamada anterior a **SQLBulkOperations** no era SQL_ADD, SQL_UPDATE_BY_BOOKMARK ni SQL_DELETE_BY_BOOKMARK, o si la *operación* argumento en la llamada anterior a  **SQLSetPos** no era SQL_UPDATE ni SQL_DELETE, el valor de **RowCountPtr* está definida por el controlador. Para obtener más información, consulte [determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
