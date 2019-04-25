---
title: Función SQLMoreResults | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a680f5579b241f6b279f5ecc994d32c8fad784f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465941"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults (función)
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLMoreResults** determina si están disponibles en una instrucción que contiene los resultados más **seleccione**, **actualización**, **insertar**, o  **ELIMINAR** instrucciones y, si es así, inicializa procese dichos resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE, OR SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLMoreResults** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL _HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLMoreResults** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02|Ha cambiado el valor de opción|El valor de un atributo de instrucción cambiado como el lote se está procesando. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. El **SQLMoreResults** se llamó a la función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* . El **SQLMoreResults** función se llamó de nuevo en el *StatementHandle*.<br /><br /> El **SQLMoreResults** se llamó a la función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*  desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLMoreResults** se llamó a la función.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **Seleccione** instrucciones devuelven conjuntos de resultados. **ACTUALIZACIÓN**, **insertar**, y **eliminar** instrucciones devuelven un recuento de filas afectadas. Si alguna de estas instrucciones se procesan por lotes, enviado con las matrices de parámetros (numerados en sentido ascendente del parámetro, en el orden en que aparecen en el lote) o en procedimientos, pueden devolver varios conjuntos de resultados o recuentos de filas. Para obtener información acerca de los lotes de instrucciones y las matrices de parámetros, vea [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) y [matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Después de ejecutar el lote, la aplicación se coloca en el primer conjunto de resultados. La aplicación puede llamar a **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll** , **SQLSetPos**y todas las funciones de metadatos en los conjuntos de resultados de las subsiguientes o primera, al igual que lo haría si hubiera solo un único conjunto de resultados. Una vez que termine con el primer conjunto de resultados, la aplicación llama a **SQLMoreResults** para desplazarse hasta el siguiente conjunto de resultados. Si está disponible, otro conjunto de resultados o recuento **SQLMoreResults** devuelve SQL_SUCCESS e inicializa el conjunto de resultados o la cuenta para su procesamiento adicional. Si las instrucciones de generación de recuento de fila aparecen entre ellos como resultado la generación de conjunto de instrucciones, puede adelantar la tecla TAB una llamada a **SQLMoreResults**. Después de llamar a **SQLMoreResults** para **actualización**, **insertar**, o **eliminar** instrucciones, una aplicación puede llamar a **SQLRowCount**.  
  
 Si se ha producido un conjunto con las filas no recuperadas de resultados actual **SQLMoreResults** descarta ese conjunto de resultados y hace que el siguiente conjunto de resultados o contar disponibles. Si se han procesado todos los resultados, **SQLMoreResults** devuelve SQL_NO_DATA. Para algunos de los controladores, los parámetros de salida y valores devueltos no están disponibles hasta que se han procesado todos los conjuntos de resultados y recuentos de filas. Para esos controladores, los parámetros de salida y devolver valores estén disponibles cuando **SQLMoreResults** devuelve SQL_NO_DATA.  
  
 Todos los enlaces que se establecieron el anterior conjunto de resultados todavía siguen siendo válidos. Si las estructuras de columna son diferentes para este conjunto de resultados, a continuación, llamar a **SQLFetch** o **SQLFetchScroll** puede producir un error o truncamiento. Para evitar esto, la aplicación tiene que llamar a **SQLBindCol** explícitamente Reenlazar según corresponda (o para hacerlo, establezca los campos de descriptor). Como alternativa, puede llamar la aplicación **SQLFreeStmt** con un *opción* SQL_UNBIND para desenlazar todos los búferes de columna.  
  
 Pueden cambiar los valores de atributos de instrucción, como tipo de cursor, simultaneidad de cursor, tamaño del conjunto de claves o la longitud máxima, como la aplicación navega por el lote mediante llamadas a **SQLMoreResults**. Si esto ocurre, **SQLMoreResults** devolverá SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 de SQLState (el valor de la opción ha cambiado).  
  
 Una llamada a **SQLCloseCursor**, o **SQLFreeStmt** con un *opción* de SQL_CLOSE, descarta todos los conjuntos de resultados y recuentos de filas que estaban disponibles como resultado de la ejecución de el lote. Devuelve el identificador de instrucción en el estado asignado o preparado. Una llamada a **SQLCancel** para cancelar una función que se ejecuta de forma asincrónica cuando se ha ejecutado un lote y el identificador de instrucción en ejecutada, coloca de cursor, o estado asincrónico conjuntos de resultados en todos los resultados y recuentos de filas genera el lote que se descarte si la llamada de cancelación se realizó correctamente. La instrucción, a continuación, vuelve al estado preparado o asignado.  
  
 Si un lote de instrucciones o un procedimiento de mezcla con otras instrucciones SQL **seleccione**, **actualización**, **insertar**, y **eliminar** instrucciones, no afectan estas otras instrucciones **SQLMoreResults**.  
  
 Para obtener más información, consulte [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Si una búsqueda, insert, instrucción update o delete en un lote de instrucciones no afecta a todas las filas en el origen de datos, **SQLMoreResults** devuelve SQL_SUCCESS. Esto es diferente en el caso de una actualización por búsqueda, insertar o eliminar la instrucción que se ejecuta a través de **SQLExecDirect**, **SQLExecute**, o **SQLParamData**, que devuelve SQL_NO_DATA si no afecta a todas las filas en el origen de datos. Si una aplicación llama a **SQLRowCount** para recuperar el recuento de filas después de llamar a **SQLMoreResults** no ha afectado a ninguna fila, **SQLRowCount** devuelve SQL_NO_DATA.  
  
 Para obtener más información acerca de la secuenciación válida de funciones de procesamiento de los resultados, vea [Apéndice B: Las tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obtener más información acerca de los parámetros de salida transmitidos y SQL_PARAM_DATA_AVAILABLE, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilidad de los recuentos de filas  
 Cuando un lote contiene varias instrucciones de generación de recuento de filas consecutivas, es posible que estos recuentos de filas se acumulan en el recuento de filas de una sola. Por ejemplo, si un lote tiene cinco instrucciones insert, algunos orígenes de datos son capaces de devolver cinco recuentos de filas individuales. Algunos otros orígenes de datos devuelven recuento solo una fila que representa la suma de los cinco recuentos de filas individuales.  
  
 Cuando un lote contiene una combinación de instrucciones de generación de recuento de fila y generar conjunto de resultados, recuentos de filas pueden o no esté disponibles en absoluto. El comportamiento del controlador con respecto a la disponibilidad de los recuentos de filas se enumera en el tipo de información de SQL_BATCH_ROW_COUNT disponible a través de una llamada a **SQLGetInfo**. Por ejemplo, suponga que el lote contiene un **seleccione**, seguido de dos **insertar**s y otra **seleccione**. A continuación, son posibles los casos siguientes:  
  
-   El recuento de filas correspondientes a las dos **insertar** instrucciones no están disponibles en absoluto. La primera llamada a **SQLMoreResults** colocará en el conjunto de resultados de la segunda **seleccione** instrucción.  
  
-   El recuento de filas correspondientes a las dos **insertar** instrucciones están disponibles de forma individual. (Una llamada a **SQLGetInfo** no devuelve el bit SQL_BRC_ROLLED_UP para el tipo de información SQL_BATCH_ROW_COUNT.) La primera llamada a **SQLMoreResults** colocará en el recuento de filas del primer **insertar**, y la segunda llamada colocará en el recuento de filas del segundo **insertar**. La tercera llamada a **SQLMoreResults** colocará en el conjunto de resultados de la segunda **seleccione** instrucción.  
  
-   El recuento de filas correspondientes a las dos **inserta** se consolidan en un recuento de filas único que está disponible. (Una llamada a **SQLGetInfo** devuelve el SQL_BRC_ROLLED_UP bit para el tipo de información SQL_BATCH_ROW_COUNT.) La primera llamada a **SQLMoreResults** colocará en el recuento de filas consolidadas y la segunda llamada a **SQLMoreResults** colocará en el conjunto de resultados de la segunda **seleccione**.  
  
 Determinados controladores que recuentos de filas esté disponible solo para los lotes explícitos y no para los procedimientos almacenados.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Capturando la totalidad o parte de una columna de datos|[Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
