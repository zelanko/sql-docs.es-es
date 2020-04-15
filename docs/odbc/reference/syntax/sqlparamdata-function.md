---
title: Función SQLParamData (SQLParamData) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ed149e125e3231d670c6ddbd4569ff5ccee5c15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306926"
---
# <a name="sqlparamdata-function"></a>Función SQLParamData
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLParamData** se usa junto con **SQLPutData** para proporcionar datos de parámetros en tiempo de ejecución de instrucciones y con **SQLGetData** para recuperar datos de parámetros de salida transmitidos.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ValuePtrPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver la dirección del búfer *ParameterValuePtr* especificado en **SQLBindParameter** (para datos de parámetro) o la dirección del búfer *TargetValuePtr* especificado en **SQLBindCol** (para datos de columna), tal como se incluye en el campo de registro del descriptor de SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLParamData** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLParamData** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|El valor de datos identificado por el *ValueType* argumento en **SQLBindParameter** para el parámetro enlazado no se pudo convertir al tipo de datos identificado por el *ParameterType* argumento en **SQLBindParameter**.<br /><br /> El valor de datos devuelto para un parámetro enlazado como SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT no se pudo convertir al tipo de datos identificado por el *ValueType* argumento en **SQLBindParameter**.<br /><br /> (Si no se pudieron convertir los valores de datos de una o varias filas, pero se devolvieron correctamente una o varias filas, esta función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|22026|Datos de cadena, desigualdad de longitud|El tipo de información SQL_NEED_LONG_DATA_LEN **de SQLGetInfo** era "Y" y se enviaron menos datos para un parámetro long (el tipo de datos se SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo) que se especificó con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**.<br /><br /> El tipo de información SQL_NEED_LONG_DATA_LEN **de SQLGetInfo** era "Y" y se enviaron menos datos para una columna larga (el tipo de datos se SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo) que se especificó en el búfer de longitud correspondiente a una columna de una fila de datos que se agregó o actualizó con **SQLBulkOperations** o se actualizó con **SQLSetPos**.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*; a continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) La llamada de función anterior no era una llamada a **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**o **SQLSetPos** donde se SQL_NEED_DATA el código de retorno, o la llamada de función anterior era una llamada a **SQLPutData**.<br /><br /> La llamada de función anterior era una llamada a **SQLParamData**.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLParamData** .<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. **SQLCancel** se llamó antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador que corresponde a *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 Si se llama a **SQLParamData** al enviar datos para un parámetro en una instrucción SQL, puede devolver cualquier SQLSTATE que pueda devolver la función a la que se llama para ejecutar la instrucción (**SQLExecute** o **SQLExecDirect**). Si se llama al enviar datos de una columna que se actualiza o agrega con **SQLBulkOperations** o se actualiza con **SQLSetPos**, puede devolver cualquier SQLSTATE que **SQLBulkOperations** o **SQLSetPos**pueda devolver .  
  
## <a name="comments"></a>Comentarios  
 **SQLParamData** se puede llamar para proporcionar datos en ejecución para dos usos: datos de parámetro que se usarán en una llamada a **SQLExecute** o **SQLExecDirect**, o datos de columna que se usarán cuando una fila se actualiza o se agrega mediante una llamada a **SQLBulkOperations** o se actualiza mediante una llamada a **SQLSetPos**. En tiempo de ejecución, **SQLParamData** devuelve a la aplicación un indicador de los datos que requiere el controlador.  
  
 Cuando una aplicación llama a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos**, el controlador devuelve SQL_NEED_DATA si necesita datos en ejecución. A continuación, una aplicación llama a **SQLParamData** para determinar qué datos enviar. Si el controlador requiere datos de parámetro, el controlador devuelve en el * \*ValuePtrPtr* búfer de salida el valor que la aplicación puso en el búfer de conjunto de filas. La aplicación puede utilizar este valor para determinar qué datos de parámetro solicita el controlador. Si el controlador requiere datos de columna, el controlador devuelve en el * \*valuePtrPtr* búfer la dirección que la columna estaba enlazada originalmente, como se indica a continuación:  
  
 *Desplazamiento* + de*enlace* de dirección enlazada + (( Número de*fila* - 1) x Tamaño *del elemento*)  
  
 donde las variables se definen como se indica en la tabla siguiente.  
  
|Variable|Descripción|  
|--------------|-----------------|  
|*Dirección enlazada*|La dirección especificada con el *TargetValuePtr* argumento en **SQLBindCol**.|  
|*Desplazamiento de enlace*|Valor almacenado en la dirección especificada con el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Row Number*|El número basado en 1 de la fila del conjunto de filas. Para las capturas de una sola fila, que son el valor predeterminado, este es 1.|  
|*Tamaño del elemento*|El valor del atributo de instrucción SQL_ATTR_ROW_BIND_TYPE para los búferes de datos y de longitud/indicador.|  
  
 También devuelve SQL_NEED_DATA, que es un indicador a la aplicación que debe llamar a **SQLPutData** para enviar los datos.  
  
 La aplicación llama a **SQLPutData** tantas veces como sea necesario para enviar los datos en ejecución para la columna o parámetro. Después de que se han enviado todos los datos para la columna o parámetro, la aplicación llama **sqlParamData** de nuevo. Si **SQLParamData** devuelve de nuevo SQL_NEED_DATA, los datos deben enviarse para otro parámetro o columna. Por lo tanto, la aplicación vuelve a llamar a **SQLPutData**. Si se han enviado todos los datos en ejecución para todos los parámetros o columnas, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el valor de * \*ValuePtrPtr* es indefinido y se puede ejecutar la instrucción SQL o se puede procesar la llamada **SQLBulkOperations** o **SQLSetPos.**  
  
 Si **SQLParamData** proporciona datos de parámetro para una instrucción de actualización o eliminación buscada que no afecta a ninguna fila en el origen de datos, la llamada a **SQLParamData** devuelve SQL_NO_DATA.  
  
 Para obtener más información acerca de cómo se pasan los datos de parámetros de datos en ejecución en tiempo de ejecución de la instrucción, vea "Pasar valores de parámetro" en [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) y [Enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md). Para obtener más información acerca de cómo se actualizan o agregan los datos de columna de datos en ejecución, vea la sección "Uso de SQLSetPos" en [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Realizar actualizaciones masivas mediante marcadores" en [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)y [Datos largos y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** se puede llamar para recuperar parámetros de salida transmitidos. Cuando **SQLMoreResults**, **SQLExecute**, **SQLGetData**o **SQLExecDirect** devuelve SQL_PARAM_DATA_AVAILABLE, llame a **SQLParamData** para determinar qué parámetro tiene un valor disponible. Para obtener más información acerca de SQL_PARAM_DATA_AVAILABLE y parámetros de salida transmitidos, vea Recuperar parámetros de [salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información sobre un parámetro en una instrucción|[Función SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Envío de datos de parámetros en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
