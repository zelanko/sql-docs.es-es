---
title: Función SQLParamData | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ffba9afd0609bab57cdaa182b650f7bd5a0fb34
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606824"
---
# <a name="sqlparamdata-function"></a>Función SQLParamData
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: 92 ISO  
  
 **Resumen**  
 **SQLParamData** se utiliza junto con **SQLPutData** para suministrar los datos de parámetro en tiempo de ejecución de la instrucción y con **SQLGetData** para recuperar los datos del parámetro de salida transmitidos.  
  
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
 [Salida] Puntero a un búfer en el que se va a devolver la dirección de la *ParameterValuePtr* especificado en el búfer **SQLBindParameter** (para datos de parámetro) o la dirección de la *TargetValuePtr* especificado en el búfer **SQLBindCol** (para los datos de columna), la medida indicada en el campo de registro de descriptor SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLParamData** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLParamData** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El valor de datos identificado por el *ValueType* argumento en **SQLBindParameter** para el parámetro dependiente no se pudo convertir al tipo de datos identificado por el *ParameterType*argumento en **SQLBindParameter**.<br /><br /> Devuelve el valor de datos para un parámetro de enlazado como SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT no se pudo convertir al tipo de datos identificado por el *ValueType* argumento en **SQLBindParameter**.<br /><br /> (Si no se podrían convertir los valores de datos para una o varias filas, pero una o más filas se devolvieron correctamente, esta función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|22026|Datos de cadena, desigualdad de longitud|El tipo de información SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "S" y se enviaron menos datos para un parámetro largo (el tipo de datos era un tipo de datos específico del origen de datos long, SQL_LONGVARBINARY o SQL_LONGVARCHAR) que se ha especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**.<br /><br /> El tipo de información SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "S" y se enviaron menos datos para una columna long (el tipo de datos era un tipo de datos específico del origen de datos long, SQL_LONGVARBINARY o SQL_LONGVARCHAR) que se especificó en el búfer de longitud correspondiente a una columna en una fila de datos que se ha agregado o actualizado con **SQLBulkOperations** o actualizados con **SQLSetPos**.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*; a continuación, se llamó la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) la llamada de función anterior no era una llamada a **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, o **SQLSetPos** donde el devolver el código era SQL_NEED_DATA o la llamada de función anterior era una llamada a **SQLPutData**.<br /><br /> La llamada de función anterior produjo una llamada a **SQLParamData**.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLParamData** se llamó a la función.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelve SQL_NEED_DATA. **SQLCancel** llamó antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador que se corresponde con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 Si **SQLParamData** se llama durante el envío de datos para un parámetro en una instrucción SQL, puede devolver cualquier SQLSTATE que puede ser devueltos por la función se llama para ejecutar la instrucción (**SQLExecute** o **SQLExecDirect**). Si se llama durante el envío de datos para una columna que se va a actualizar o agregar con **SQLBulkOperations** o se actualiza con **SQLSetPos**, puede devolver cualquier SQLSTATE, que puede devolver  **SQLBulkOperations** o **SQLSetPos**.  
  
## <a name="comments"></a>Comentarios  
 **SQLParamData** puede llamarse para suministrar datos a datos en ejecución para los dos usos: datos de parámetro que se usará en una llamada a **SQLExecute** o **SQLExecDirect**, o datos de la columna que se utiliza cuando una fila se actualiza o agrega mediante una llamada a **SQLBulkOperations** o se actualiza mediante una llamada a **SQLSetPos**. En tiempo de ejecución **SQLParamData** devuelve a la aplicación requiere de un indicador de los datos que el controlador.  
  
 Cuando una aplicación llama **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos**, el controlador devuelve SQL_NEED_ DATOS si necesita datos de datos en ejecución. Una aplicación, a continuación, llama a **SQLParamData** para determinar qué datos se deben enviar. Si el controlador requiere datos de parámetro, el controlador devuelve en el  *\*ValuePtrPtr* el valor que la aplicación se coloca en el búfer de conjunto de filas del búfer de salida. La aplicación puede usar este valor para determinar los datos de parámetro que se está solicitando el controlador. Si el controlador requiere datos de columna, el controlador devuelve en el  *\*ValuePtrPtr* almacenar en búfer la dirección que originalmente se enlazó la columna, como se indica a continuación:  
  
 *Enlazado dirección* + *enlace desplazamiento* + ((*número de fila* – 1) x *ElementSize*)  
  
 donde se definen las variables como se indica en la tabla siguiente.  
  
|Variable|Descripción|  
|--------------|-----------------|  
|*Enlazado de dirección*|La dirección especificada con el *TargetValuePtr* argumento en **SQLBindCol**.|  
|*Desplazamiento de enlace*|El valor almacenado en la dirección especificada con el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Número de fila*|Número de la fila del conjunto de filas basado en 1. Capturas de fila única, que son el valor predeterminado, esto es 1.|  
|*Tamaño del elemento*|El valor del atributo de instrucción SQL_ATTR_ROW_BIND_TYPE para los búferes de datos y de longitud/indicador.|  
  
 También devuelve SQL_NEED_DATA, que es un indicador para la aplicación que debe llamar a **SQLPutData** para enviar los datos.  
  
 La aplicación llama a **SQLPutData** tantas veces como sea necesario para enviar los datos de datos en ejecución para la columna o parámetro. Después de haber enviado todos los datos para la columna o parámetro, la aplicación llama a **SQLParamData** nuevo. Si **SQLParamData** nuevo devuelve SQL_NEED_DATA, se deben enviar los datos para otra columna o parámetro. Por lo tanto, llama la aplicación de nuevo **SQLPutData**. Si todos los datos de datos en ejecución se ha enviado para todos los parámetros o columnas, a continuación, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el valor de  *\*ValuePtrPtr* no está definido, y se puede ejecutar la instrucción SQL o el **SQLBulkOperations** o **SQLSetPos** se puede procesar la llamada.  
  
 Si **SQLParamData** proporciona datos de parámetro para una búsqueda instrucción update o delete que no afecta a todas las filas en el origen de datos, la llamada a **SQLParamData** devuelve SQL_NO_DATA.  
  
 Para obtener más información acerca de los datos de parámetro de modo de datos en ejecución se pasa en tiempo de ejecución de la instrucción, vea "Pasar valores de parámetro" en [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) y [enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md). Para obtener más información acerca de los datos de columna de forma de datos en ejecución se actualiza o agrega, vea la sección "Uso SQLSetPos" en [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Realizar masiva actualizaciones utilizando marcadores" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), y [datos de tipo Long y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** se puede llamar para recuperar los parámetros de salida transmitidos. Cuando **SQLMoreResults**, **SQLExecute**, **SQLGetData**, o **SQLExecDirect** devuelve SQL_PARAM_DATA_AVAILABLE, llame a **SQLParamData** para determinar qué parámetro tiene un valor disponible. Para obtener más información acerca de los parámetros de salida transmitidos y SQL_PARAM_DATA_AVAILABLE, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de un parámetro en una instrucción|[Función SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
