---
title: "SQLParamData, función | Documentos de Microsoft"
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
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 019b15aa5a4bd27bd96261d016fbaaebe0fc366c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlparamdata-function"></a>SQLParamData, función
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLParamData** se utiliza junto con **SQLPutData** para proporcionar datos de parámetro en tiempo de ejecución de la instrucción y con **SQLGetData** para recuperar datos de parámetro de salida transmitidos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ValuePtrPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver la dirección de la *ParameterValuePtr* especificado en el búfer **SQLBindParameter** (para los datos de parámetro) o la dirección de la *TargetValuePtr* especificado en el búfer **SQLBindCol** (para los datos de columna), tal y como figura en el campo de registro de descriptor SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLParamData** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLParamData** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El valor de datos identificado por la *ValueType* argumento en **SQLBindParameter** para los parámetros enlazados no se pudieron convertir al tipo de datos identificado por la *ParameterType*argumento en **SQLBindParameter**.<br /><br /> Devuelve el valor de datos para un parámetro de enlazado como SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT no se pudo convertir al tipo de datos identificado por la *ValueType* argumento en **SQLBindParameter**.<br /><br /> (Si no se pudieron convertir los valores de datos para una o varias filas, pero una o más filas se devolvieron correctamente, esta función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|22026|Datos de cadena, desigualdad de longitud|El tipo de información de SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "Y" y se enviaron menos datos para un parámetro de tiempo (el tipo de datos fue SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos de tipo long) que se especificó con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**.<br /><br /> El tipo de información de SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "Y" y menos datos se enviaron para una columna long (tipo de datos fue SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos de tipo long) que se especificaron en el búfer de longitud correspondiente a una columna en una fila de datos que se ha agregado o actualizado con **SQLBulkOperations** o actualizados con **SQLSetPos**.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*; a continuación, se llama nuevo a la función en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) la llamada de función anterior no fue una llamada a **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, o **SQLSetPos** donde el devolver código fue SQL_NEED_DATA o la llamada de función anterior produjo una llamada a **SQLPutData**.<br /><br /> La llamada de función anterior produjo una llamada a **SQLParamData**.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLParamData** se llamó la función.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelve SQL_NEED_DATA. **SQLCancel** se llamó antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador que se corresponde con el *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
 Si **SQLParamData** se llama durante el envío de datos para un parámetro en una instrucción SQL, puede devolver cualquier SQLSTATE que puede ser devueltos por la función se llama para ejecutar la instrucción (**SQLExecute** o **SQLExecDirect**). Si se llama al enviar datos de una columna que se va a actualizar o agregar con **SQLBulkOperations** o se actualiza con **SQLSetPos**, puede devolver cualquier SQLSTATE, que puede ser devueltos por ** SQLBulkOperations** o **SQLSetPos**.  
  
## <a name="comments"></a>Comentarios  
 **SQLParamData** se puede llamar para proporcionar datos de datos en ejecución de dos usos: datos de parámetro que se usará en una llamada a **SQLExecute** o **SQLExecDirect**, o los datos de columna que se utilizará Cuando se actualiza o se agregan mediante una llamada a una fila **SQLBulkOperations** o actualizar a través de una llamada a **SQLSetPos**. En tiempo de ejecución, **SQLParamData** devuelve a la aplicación el controlador de un indicador de los datos que se requiere.  
  
 Cuando una aplicación llama **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos**, el controlador devuelve SQL_NEED_ DATOS si necesita datos de datos en ejecución. Una aplicación, a continuación, llama a **SQLParamData** para determinar qué datos se deben enviar. Si el controlador requiere que los datos de parámetro, el controlador devuelve en el * \*ValuePtrPtr* el valor que la aplicación se coloca en el búfer de conjunto de filas del búfer de salida. La aplicación puede utilizar este valor para determinar qué datos de parámetro que se está solicitando el controlador. Si el controlador requiere que los datos de columna, el controlador devuelve en el * \*ValuePtrPtr* almacenar en búfer la dirección que originalmente estaba enlazada la columna, como se indica a continuación:  
  
 *Enlazado dirección* + *enlace desplazamiento* + ((*número de fila* – 1) x *tamaño del elemento*)  
  
 donde se definen las variables como se indica en la tabla siguiente.  
  
|Variable|Description|  
|--------------|-----------------|  
|*Enlazado de dirección*|La dirección especificada con la *TargetValuePtr* argumento en **SQLBindCol**.|  
|*Desplazamiento de enlace*|El valor almacenado en la dirección especificada con el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Número de fila*|El número basado en 1 de la fila del conjunto de filas. Para capturar varias filas, que es el valor predeterminado, es 1.|  
|*Tamaño del elemento*|El valor del atributo de instrucción SQL_ATTR_ROW_BIND_TYPE para los búferes de datos y de longitud/indicador.|  
  
 También devuelve SQL_NEED_DATA, que es un indicador a la aplicación que debe llamar a **SQLPutData** para enviar los datos.  
  
 La aplicación llama **SQLPutData** tantas veces como sea necesario para enviar los datos de datos en ejecución para la columna o parámetro. Después de haber enviado todos los datos para la columna o parámetro, la aplicación llama a **SQLParamData** nuevo. Si **SQLParamData** nuevo devuelve SQL_NEED_DATA, se deben enviar los datos de otro parámetro o columna. Por lo tanto, llama a la aplicación de nuevo **SQLPutData**. Si todos los datos de datos en ejecución se ha enviado para todos los parámetros o columnas, a continuación, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el valor de * \*ValuePtrPtr* no está definido, y se puede ejecutar la instrucción SQL o el **SQLBulkOperations** o **SQLSetPos** llamada puede ser procesada.  
  
 Si **SQLParamData** proporciona datos de parámetro para una búsqueda instrucción update o delete que no afecta a las filas del origen de datos, la llamada a **SQLParamData** devuelve SQL_NO_DATA.  
  
 Para obtener más información acerca de los datos de parámetro de modo de datos en ejecución se pasa en tiempo de ejecución de la instrucción, vea "Pasar valores de parámetro" en [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) y [enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md). Para obtener más información acerca de los datos de columna de forma de datos en ejecución se actualiza o se agregan, vea la sección "Usar SQLSetPos" en [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Realizar masiva actualizaciones Using Bookmarks" en [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), y [datos de tipo Long y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** se puede llamar para recuperar los parámetros de salida transmitidos. Cuando **SQLMoreResults**, **SQLExecute**, **SQLGetData**, o **SQLExecDirect** devuelve SQL_PARAM_DATA_AVAILABLE, llame a **SQLParamData** para determinar qué parámetro tiene un valor disponible. Para obtener más información sobre SQL_PARAM_DATA_AVAILABLE y los parámetros de salida transmitidos, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con un parámetro|[SQLBindParameter, función](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de un parámetro en una instrucción|[SQLDescribeParam, función](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Ejecutar una instrucción SQL|[SQLExecDirect, función](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[SQLExecute, función](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[SQLPutData, función](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
