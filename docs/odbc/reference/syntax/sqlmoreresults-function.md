---
title: Función SQLMoreResults (SQLMoreResults) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78bbb277e4b783eb46c79f59939a1080feae2b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304746"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults (función)
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: ODBC  
  
 **Resumen**  
 **SQLMoreResults** determina si hay más resultados disponibles en una instrucción que contiene instrucciones **SELECT**, **UPDATE**, **INSERT**o **DELETE** y, si es así, inicializa el procesamiento de esos resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLMoreResults** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLMoreResults** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S02|El valor de la opción ha cambiado|El valor de un atributo de instrucción cambió a medida que se procesaba el lote. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función **SQLMoreResults** y, antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función **SQLMoreResults** en *StatementHandle*.<br /><br /> Se llamó a la función **SQLMoreResults** y, antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLMoreResults** .<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **Las** instrucciones SELECT devuelven conjuntos de resultados. **Las**instrucciones UPDATE , **INSERT**y **DELETE** devuelven un recuento de filas afectadas. Si alguna de estas instrucciones se procesa por lotes, se envía con matrices de parámetros (numerados en orden de parámetros crecientes, en el orden en que aparecen en el lote) o en procedimientos, pueden devolver varios conjuntos de resultados o recuentos de filas. Para obtener información acerca de lotes de instrucciones y matrices de parámetros, vea [Lotes de instrucciones SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) y matrices de valores de [parámetros](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Después de ejecutar el lote, la aplicación se coloca en el primer conjunto de resultados. La aplicación puede llamar a **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, **SQLSetPos**y todas las funciones de metadatos, en el primer o cualquier conjunto de resultados posterior, tal como lo haría si hubiera un solo conjunto de resultados. Una vez que se realiza con el primer conjunto de resultados, la aplicación llama a **SQLMoreResults** para pasar al siguiente conjunto de resultados. Si hay otro conjunto de resultados o recuento disponible, **SQLMoreResults** devuelve SQL_SUCCESS e inicializa el conjunto de resultados o el recuento para el procesamiento adicional. Si aparecen instrucciones de generación de recuento de filas entre instrucciones de generación de conjuntos de resultados, se pueden repasar llamando a **SQLMoreResults**. Después de llamar a **SQLMoreResults** para las instrucciones **UPDATE**, **INSERT**o **DELETE,** una aplicación puede llamar a **SQLRowCount**.  
  
 Si había un conjunto de resultados actual con filas no capturadas, **SQLMoreResults** descarta ese conjunto de resultados y hace que el siguiente conjunto de resultados o recuento esté disponible. Si se han procesado todos los resultados, **SQLMoreResults** devuelve SQL_NO_DATA. Para algunos controladores, los parámetros de salida y los valores devueltos no están disponibles hasta que se hayan procesado todos los conjuntos de resultados y recuentos de filas. Para estos controladores, los parámetros de salida y los valores devueltos estarán disponibles cuando **SQLMoreResults** devuelve SQL_NO_DATA.  
  
 Los enlaces que se establecieron para el conjunto de resultados anterior siguen siendo válidos. Si las estructuras de columna son diferentes para este conjunto de resultados, a continuación, llamar a **SQLFetch** o **SQLFetchScroll** puede dar lugar a un error o truncamiento. Para evitar esto, la aplicación tiene que llamar a **SQLBindCol** para volver a enlazar explícitamente según corresponda (o hacerlo estableciendo campos descriptores). Como alternativa, la aplicación puede llamar a **SQLFreeStmt** con una *opción* de SQL_UNBIND para desenlazar todos los búferes de columna.  
  
 Los valores de los atributos de instrucción, como el tipo de cursor, la simultaneidad del cursor, el tamaño del conjunto de claves o la longitud máxima, pueden cambiar a medida que la aplicación navega por el lote mediante llamadas a **SQLMoreResults**. Si esto sucede, **SQLMoreResults** devolverá SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 (el valor de opción ha cambiado).  
  
 Al llamar a **SQLCloseCursor**, o **SQLFreeStmt** con una *opción* de SQL_CLOSE, se descartan todos los conjuntos de resultados y recuentos de filas que estaban disponibles como resultado de la ejecución del lote. El identificador de instrucción vuelve al estado asignado o preparado. Llamar a **SQLCancel** para cancelar una función de ejecución asincrónica cuando se ha ejecutado un lote y el identificador de instrucción está en el estado ejecutado, colocado por cursor o asincrónico da como resultado todos los conjuntos de resultados y recuentos de filas generados por el lote que se descarta si la llamada de cancelación se realizó correctamente. A continuación, la instrucción vuelve al estado preparado o asignado.  
  
 Si un lote de instrucciones o un procedimiento mezcla otras instrucciones SQL con instrucciones **SELECT**, **UPDATE**, **INSERT**y **DELETE,** estas otras instrucciones no afectan a **SQLMoreResults**.  
  
 Para obtener más información, consulte [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Si una instrucción de actualización, inserción o eliminación buscada en un lote de instrucciones no afecta a ninguna fila del origen de datos, **SQLMoreResults** devuelve SQL_SUCCESS. Esto es diferente del caso de una instrucción de actualización, inserción o eliminación buscada que se ejecuta a través de **SQLExecDirect**, **SQLExecute**o **SQLParamData**, que devuelve SQL_NO_DATA si no afecta a ninguna fila del origen de datos. Si una aplicación llama a **SQLRowCount** para recuperar el recuento de filas después de que una llamada a **SQLMoreResults** no haya afectado a ninguna fila, **SQLRowCount** devolverá SQL_NO_DATA.  
  
 Para obtener información adicional acerca de la secuenciación válida de las funciones de procesamiento de resultados, consulte [Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .  
  
 Para obtener más información acerca de SQL_PARAM_DATA_AVAILABLE y parámetros de salida transmitidos, vea Recuperar parámetros de [salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilidad de recuentos de filas  
 Cuando un lote contiene varias instrucciones de generación de recuento de filas consecutivas, es posible que estos recuentos de filas se acumulan en un solo recuento de filas. Por ejemplo, si un lote tiene cinco instrucciones insert, ciertos orígenes de datos son capaces de devolver cinco recuentos de filas individuales. Algunos otros orígenes de datos devuelven solo un recuento de filas que representa la suma de los cinco recuentos de filas individuales.  
  
 Cuando un lote contiene una combinación de instrucciones de generación de conjuntos de resultados y de generación de recuento de filas, los recuentos de filas pueden o no estar disponibles en absoluto. El comportamiento del controlador con respecto a la disponibilidad de recuentos de filas se enumera en el tipo de información SQL_BATCH_ROW_COUNT disponible a través de una llamada a **SQLGetInfo**. Por ejemplo, supongamos que el lote contiene un **select**, seguido de dos **INSERT**s y otro **SELECT**. A continuación, es posible realizar los siguientes casos:  
  
-   Los recuentos de filas correspondientes a las dos instrucciones **INSERT** no están disponibles en absoluto. La primera llamada a **SQLMoreResults** le colocará en el conjunto de resultados de la segunda instrucción **SELECT.**  
  
-   Los recuentos de filas correspondientes a las dos instrucciones **INSERT** están disponibles individualmente. (Una llamada a **SQLGetInfo** no devuelve el bit SQL_BRC_ROLLED_UP para el tipo de información SQL_BATCH_ROW_COUNT.) La primera llamada a **SQLMoreResults** le colocará en el recuento de filas de la primera **INSERT**y la segunda llamada le colocará en el recuento de filas del segundo **INSERT**. La tercera llamada a **SQLMoreResults** le colocará en el conjunto de resultados de la segunda instrucción **SELECT.**  
  
-   Los recuentos de filas correspondientes a los dos **INSERT** se acumulan en un único recuento de filas que está disponible. (Una llamada a **SQLGetInfo** devuelve el bit SQL_BRC_ROLLED_UP para el tipo de información SQL_BATCH_ROW_COUNT.) La primera llamada a **SQLMoreResults** le colocará en el recuento de filas enrollados y la segunda llamada a **SQLMoreResults** le colocará en el conjunto de resultados de la segunda **SELECT**.  
  
 Algunos controladores hacen que los recuentos de filas solo estén disponibles para lotes explícitos y no para procedimientos almacenados.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de parte o la totalidad de una columna de datos|[Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
