---
title: SQLMoreResults (función) | Documentos de Microsoft
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
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1905665f1505cd484a6d2ab5c1f83008efc2298
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults (función)
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLMoreResults** determina si existen más resultados en una instrucción que lo contiene **seleccione**, **actualización**, **insertar**, o  **ELIMINAR** instrucciones y, si es así, inicializa procesar para esos resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE O SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLMoreResults** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL _HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLMoreResults** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02 DE SQLSTATE|Ha cambiado el valor de la opción|El valor de un atributo de instrucción que se cambiaron como el lote se está procesando. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. El **SQLMoreResults** se llamó a función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* . La **SQLMoreResults** función llamó de nuevo en el *StatementHandle*.<br /><br /> El **SQLMoreResults** se llamó a función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*  desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLMoreResults** se llamó la función.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **Seleccione** instrucciones devuelven conjuntos de resultados. **ACTUALIZACIÓN**, **insertar**, y **eliminar** instrucciones devuelven un recuento de filas afectadas. Si alguna de estas instrucciones se procesan por lotes, se ha enviado con matrices de parámetros (se numeran de forma ascendente, orden de los parámetros, en el orden en que aparecen en el lote) o en procedimientos, pueden devolver varios conjuntos de resultados o recuentos de filas. Para obtener información acerca de los lotes de instrucciones y las matrices de parámetros, vea [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) y [matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Después de ejecutar el lote, la aplicación se coloca en el primer conjunto de resultados. La aplicación puede llamar a **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll** , **SQLSetPos**y todas las funciones de metadatos en los conjuntos de resultados de primer o las subsiguientes, al igual que lo haría si hubiera un conjunto de resultados único. Una vez que termine con el primer conjunto de resultados, la aplicación llama a **SQLMoreResults** para desplazarse hasta el siguiente conjunto de resultados. Si está disponible, otro conjunto de resultados o recuento de **SQLMoreResults** devuelve SQL_SUCCESS e inicializa el conjunto de resultados o la cuenta para su posterior procesamiento. Si las instrucciones de generación de recuento de filas aparecen entre las instrucciones set: generar como resultado, pueden ejecutar paso paso por una llamada a **SQLMoreResults**. Después de llamar a **SQLMoreResults** para **actualización**, **insertar**, o **eliminar** instrucciones, una aplicación puede llamar a **SQLRowCount**.  
  
 Si no hay un conjunto con las filas no recuperadas de resultados actual **SQLMoreResults** descarta ese conjunto de resultados y hace que el siguiente conjunto de resultados o se reflejará disponibles. Si se han procesado todos los resultados, **SQLMoreResults** devuelve SQL_NO_DATA. Para algunos de los controladores, parámetros de salida y valores devueltos no están disponibles hasta que se han procesado todos los conjuntos de resultados y recuentos de filas. Para este tipo de los controladores, los parámetros de salida y devolver valores estén disponibles cuando **SQLMoreResults** devuelve SQL_NO_DATA.  
  
 Todos los enlaces que se han establecido para el anterior conjunto de resultados siga siendo válidos. Si las estructuras de columna son diferentes para este conjunto de resultados, a continuación, llamar a **SQLFetch** o **SQLFetchScroll** puede producir un error o truncamiento. Para evitar esto, la aplicación tiene que llamar a **SQLBindCol** explícitamente Reenlazar según corresponda (o para hacerlo, establezca los campos de descriptor). Como alternativa, puede llamar la aplicación **SQLFreeStmt** con una *opción* SQL_UNBIND para desenlazar todos los búferes de columna.  
  
 Pueden cambiar los valores de atributos de instrucción, como el tipo de cursor, simultaneidad de cursor, tamaño de conjunto de claves o la longitud máxima, como la aplicación se desplaza a través del lote mediante llamadas a **SQLMoreResults**. Si esto ocurre, **SQLMoreResults** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 de SQLState (el valor de la opción ha cambiado).  
  
 Al llamar a **SQLCloseCursor**, o **SQLFreeStmt** con una *opción* de SQL_CLOSE, descarta todos los conjuntos de resultados y recuentos de filas que estaban disponibles como resultado de la ejecución de el lote. Devuelve el identificador de instrucción en el estado asignado o preparado. Al llamar a **SQLCancel** para cancelar una función que se ejecuta de forma asincrónica cuando se ha ejecutado un lote y el identificador de instrucción está en ejecutada, cursor se sitúa, o estado asincrónico da como resultado todos los resultados conjuntos y recuentos de filas genera el lote que se descarta si la llamada de cancelación se realizó correctamente. La instrucción, a continuación, vuelve al estado preparado o asignado.  
  
 Si un lote de instrucciones y un procedimiento mezcla otras instrucciones SQL con **seleccione**, **actualización**, **insertar**, y **eliminar** instrucciones, no afectan estas otras instrucciones **SQLMoreResults**.  
  
 Para obtener más información, consulte [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Si una búsqueda, insert, instrucción update o delete en un lote de instrucciones no afecta a las filas del origen de datos, **SQLMoreResults** devuelve SQL_SUCCESS. Esto es diferente del caso de una actualización por búsqueda, insert o delete, instrucción que se ejecuta a través de **SQLExecDirect**, **SQLExecute**, o **SQLParamData**, que devuelve SQL_NO_DATA si no afecta a las filas del origen de datos. Si una aplicación llama **SQLRowCount** para recuperar el recuento de filas después de llamar a **SQLMoreResults** no ha afectado a ninguna fila, **SQLRowCount** devuelve SQL_NO_DATA.  
  
 Para obtener información adicional sobre la secuenciación válida de funciones de procesamiento de los resultados, vea [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obtener más información sobre SQL_PARAM_DATA_AVAILABLE y los parámetros de salida transmitidos, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilidad de recuentos de filas  
 Cuando un lote contiene varias instrucciones de generación de recuento de filas consecutivas, es posible que estos recuentos de filas se acumulan en el recuento de una sola fila. Por ejemplo, si un lote tiene cinco instrucciones insert, a continuación, algunos orígenes de datos tienen la capacidad de devolver cinco recuentos de filas individuales. Algunos otros orígenes de datos devuelven el recuento de una sola fila que representa la suma de los cinco recuentos de filas individuales.  
  
 Cuando un lote contiene una combinación de instrucciones de generación de recuento de filas y conjunto de resultados: generar, recuentos de filas pueden o no estén disponibles en absoluto. El comportamiento del controlador con respecto a la disponibilidad de recuentos de filas es de tipo enumerado en el tipo de información de SQL_BATCH_ROW_COUNT disponible a través de una llamada a **SQLGetInfo**. Por ejemplo, suponga que el lote contiene una **seleccione**, seguido de dos **insertar**s y otro **seleccione**. A continuación, son posibles los siguientes casos:  
  
-   El recuento de filas correspondientes a las dos **insertar** instrucciones no están disponibles en absoluto. La primera llamada a **SQLMoreResults** se colocará en el conjunto de resultados de la segunda **seleccione** instrucción.  
  
-   El recuento de filas correspondientes a las dos **insertar** instrucciones están disponibles de forma individual. (Una llamada a **SQLGetInfo** no devuelve el bit SQL_BRC_ROLLED_UP para el tipo de información de SQL_BATCH_ROW_COUNT.) La primera llamada a **SQLMoreResults** se colocará en el recuento de filas de la primera **insertar**, y la segunda llamada se colocará en el recuento de filas del segundo **insertar**. La tercera llamada a **SQLMoreResults** se colocará en el conjunto de resultados de la segunda **seleccione** instrucción.  
  
-   El recuento de filas correspondientes a las dos **inserta** se consolidan en un recuento de filas único que está disponible. (Una llamada a **SQLGetInfo** devuelve el SQL_BRC_ROLLED_UP bit para el tipo de información de SQL_BATCH_ROW_COUNT.) La primera llamada a **SQLMoreResults** se colocará en el recuento de filas consolidadas y la segunda llamada a **SQLMoreResults** se colocará en el conjunto de resultados de la segunda **seleccione**.  
  
 Ciertos controladores de disponer de recuentos de filas solamente para los lotes explícitos y no para los procedimientos almacenados.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Cancelar el procesamiento de una instrucción|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Capturar una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Capturar parte o la totalidad de una columna de datos|[Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
