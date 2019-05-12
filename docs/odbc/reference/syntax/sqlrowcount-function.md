---
title: SQLRowCount Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ccc858603fc5662f380c5d3ae48d777005ddac4
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537162"
---
# <a name="sqlrowcount-function"></a>Función SQLRowCount
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLRowCount** devuelve el número de filas afectadas por una **actualización**, **insertar**, o **eliminar** instrucción; un SQL_ADD SQL_UPDATE_BY_BOOKMARK o SQL_ Operación DELETE_BY_BOOKMARK en **SQLBulkOperations**; o una operación SQL_UPDATE o SQL_DELETE de **SQLSetPos**.  
  
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
 [Salida] Señala a un búfer en el que se va a devolver un recuento de filas. Para **actualización**, **insertar**, y **eliminar** las instrucciones para las operaciones SQL_ADD SQL_UPDATE_BY_BOOKMARK y SQL_DELETE_BY_BOOKMARK en  **SQLBulkOperations**y para las operaciones SQL_UPDATE o SQL_DELETE en **SQLSetPos**, el valor devuelto en **RowCountPtr* es el número de filas afectadas por la solicitud o -1 si el número de filas afectadas no está disponible.  
  
 Cuando **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos o SQLMoreResults** se denomina el SQL_DIAG_ROW_COUNT campo de la estructura de datos de diagnóstico se establece en el recuento de filas y el recuento de filas se almacena en caché de forma depende de la implementación. **SQLRowCount** devuelve el valor de recuento de fila almacenada en caché. El valor de número de fila almacenada en caché es válido hasta que el identificador de instrucción se vuelve a establecer el estado preparado o asignado, se vuelve a ejecutar la instrucción, o **SQLCloseCursor** se llama. Tenga en cuenta que si llama a una función que se ha establecido el campo SQL_DIAG_ROW_COUNT, el valor devuelto por **SQLRowCount** puede ser diferente del valor en el campo SQL_DIAG_ROW_COUNT porque el campo SQL_DIAG_ROW_COUNT se restablece a 0 por cualquier llamada de función.  
  
 Para otras instrucciones y funciones, el controlador puede definir el valor devuelto en \* *RowCountPtr*. Por ejemplo, algunos orígenes de datos pueden ser capaz de devolver el número de filas devueltas por una **seleccione** instrucción o una función de catálogo antes de capturar las filas.  
  
> [!NOTE]  
>  Muchos orígenes de datos no pueden devolver el número de filas en un conjunto de resultados antes descargarlas; Para obtener la máxima interoperatividad, las aplicaciones no deben basarse en este comportamiento.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLRowCount** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLRowCount** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLRowCount** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) que se llamó la función antes de llamar a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** para el  *StatementHandle*.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Si la última instrucción SQL que se ejecuta en el identificador de instrucción no era un **actualización**, **insertar**, o **eliminar** instrucción o si el *operación* argumento de la llamada anterior a **SQLBulkOperations** no era SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK, o si el *operación* argumento en la llamada anterior a  **SQLSetPos** no era SQL_UPDATE o SQL_DELETE, el valor de **RowCountPtr* está definido por el controlador. Para obtener más información, consulte [determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
