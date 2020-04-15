---
title: Función SQLExecute ?????????? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecute
helpviewer_keywords:
- SQLExecute function [ODBC]
ms.assetid: 9286a01d-cde2-4b90-af94-9fd7f8da48bf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5306567aebc229a8bc9d1d3c91bcbd8e79391752
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286075"
---
# <a name="sqlexecute-function"></a>Función SQLExecute
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLExecute** ejecuta una instrucción preparada, utilizando los valores actuales de las variables de marcador de parámetro si existen marcadores de parámetro en la instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLExecute(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLExecute** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLExecute** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflicto de operación del cursor|La instrucción preparada asociada con el *StatementHandle* contenía una instrucción update o delete posicionada, y no se actualizaron o eliminaron filas o más de una fila. (Para obtener más información acerca de las actualizaciones de más de una fila, vea la descripción del *atributo* SQL_ATTR_SIMULATE_CURSOR en **SQLSetStmtAttr**.)<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01003|Valor NULL eliminado en la función set|La instrucción preparada asociada a *StatementHandle* contenía una función set (como **AVG**, **MAX**, **MIN**, etc.), pero no la función **count** set y los valores de argumento NULL se eliminaron antes de aplicar la función. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|Los datos de cadena o binarios devueltos para un parámetro de salida dieron como resultado el truncamiento de caracteres no en blanco o datos binarios no NULL. Si era un valor de cadena, se truncaba a la derecha. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01006|Privilegio no revocado|La instrucción preparada asociada a *StatementHandle* era una instrucción **REVOKE** y el usuario no tenía el privilegio especificado. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01007|Privilegio no concedido|La instrucción preparada asociada a *StatementHandle* era una instrucción **GRANT** y no se podía conceder al usuario el privilegio especificado.|  
|01S02|Valor de opción cambiado|Un atributo de instrucción especificado no era válido debido a las condiciones de trabajo de implementación, por lo que se sustituyó temporalmente un valor similar. (**SQLGetStmtAttr** se puede llamar para determinar cuál es el valor sustituido temporalmente.) El valor sustituto es válido para *StatementHandle* hasta que se cierra el cursor, momento en el que el atributo de instrucción vuelve a su valor anterior. Los atributos de instrucción que se pueden cambiar son: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT y SQL_ATTR_SIMULATE_CURSOR. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamiento fraccionario|Los datos devueltos para un parámetro de entrada/salida o salida se truncaron de modo que la parte fraccionaria de un tipo de datos numérico se truncó o se truncó la parte fraccionaria del componente de tiempo de un tipo de datos de tiempo, marca de tiempo o intervalo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07002|Campo COUNT incorrecto|El número de parámetros especificado en **SQLBindParameter** era menor que el \*número de parámetros de la instrucción SQL contenida en *StatementText*.<br /><br /> **SQLBindParameter** se llamó con *ParameterValuePtr* establecido en un puntero nulo, *no StrLen_or_IndPtr* establecido en SQL_NULL_DATA o SQL_DATA_AT_EXEC y *InputOutputType* no establecido en SQL_PARAM_OUTPUT, por lo que el número de parámetros especificados en **SQLBindParameter** era mayor que el número de parámetros de la instrucción SQL contenida en **StatementText*.|  
|07006|Infracción de atributo de tipo de datos restringido|El valor de datos identificado por el *ValueType* argumento en **SQLBindParameter** para el parámetro enlazado no se pudo convertir al tipo de datos identificado por el *ParameterType* argumento en **SQLBindParameter**.<br /><br /> El valor de datos devuelto para un parámetro enlazado como SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT no se pudo convertir al tipo de datos identificado por el *ValueType* argumento en **SQLBindParameter**.<br /><br /> (Si los valores de datos de una o más filas no se pudieron convertir, pero se devolvieron correctamente una o varias filas, esta función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07007|Infracción del valor de parámetro restringido|El tipo de parámetro SQL_PARAM_INPUT_OUTPUT_STREAM solo se utiliza para un parámetro que envía y recibe datos en partes. No se permite un búfer enlazado de entrada para este tipo de parámetro.<br /><br /> Este error se producirá cuando se SQL_PARAM_INPUT_OUTPUT \*el tipo de parámetro y cuando el *StrLen_or_IndPtr* especificado en **SQLBindParameter** no es igual a SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_LEN_DATA_AT_EXEC(len) o SQL_DATA_AT_EXEC.|  
|07S01|Uso no válido del parámetro predeterminado|Un valor de parámetro, establecido con **SQLBindParameter**, se SQL_DEFAULT_PARAM y el parámetro correspondiente no era un parámetro para una invocación de procedimiento canónico ODBC.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|21S02|El grado de la tabla derivada no coincide con la lista de columnas|La instrucción preparada asociada a *StatementHandle* contenía una instrucción **CREATE VIEW** y la lista de columnas no calificadas (el número de columnas especificadas para la vista en los argumentos de identificador de *columna* de la instrucción SQL) contenía más nombres que el número de columnas de la tabla derivada definida por el argumento *de especificación* de consulta de la instrucción SQL.|  
|22001|Datos de cadena, truncamiento a la derecha|La asignación de un carácter o valor binario a una columna dio lugar a la truncación de caracteres o bytes no en blanco (carácter) o no nulos (binarios).|  
|22002|Variable indicador requerida pero no suministrada|Null datos se enlazan a un parámetro de salida cuya *StrLen_or_IndPtr* establecido por **SQLBindParameter** era un puntero nulo.|  
|22003|Valor numérico fuera del rango|La instrucción preparada asociada a *StatementHandle* contenía un parámetro numérico enlazado y el valor del parámetro hizo que toda la parte (en lugar de fraccionaria) del número se truncase cuando se asigna a la columna de tabla asociada.<br /><br /> Devolver un valor numérico (como numérico o cadena) para uno o más parámetros de entrada/salida o salida habría provocado que se truncase la parte total (en lugar de fracción) del número.|  
|22007|Formato de fecha y hora no válido|La instrucción preparada asociada a *StatementHandle* contenía una instrucción SQL que contenía una estructura de fecha, hora o marca de tiempo como parámetro enlazado, y el parámetro era, respectivamente, una fecha, hora o marca de tiempo no válida.<br /><br /> Un parámetro de entrada/salida o salida se enlazaba a una estructura C de fecha, hora o marca de tiempo, y un valor en el parámetro devuelto era, respectivamente, una fecha, hora o marca de tiempo no válida. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|22008|Desbordamiento de campo de fecha y hora|La instrucción preparada asociada a *StatementHandle* contenía una instrucción SQL que contenía una expresión datetime que, cuando se calculaba, daba como resultado una estructura de fecha, hora o marca de tiempo que no era válida.<br /><br /> Una expresión datetime calculada para un parámetro de entrada/salida o salida dio como resultado una estructura C de fecha, hora o marca de tiempo que no era válida.|  
|22012|División por cero|La instrucción preparada asociada con el *StatementHandle* contenía una expresión aritmética que provocaba la división por cero.<br /><br /> Una expresión aritmética calculada para un parámetro de entrada/salida o salida dio como resultado la división por cero.|  
|22015|Desbordamiento de campo de intervalo|StatementText contenía un parámetro numérico o de intervalo exacto que, cuando se convierte en un tipo de datos SQL de intervalo, causó una pérdida de dígitos significativos. * \**<br /><br /> StatementText contenía un parámetro interval con más de un campo que, cuando se convierte en un tipo de datos numérico en una columna, no tenía ninguna representación en el tipo de datos numérico. * \**<br /><br /> StatementText contenía datos de parámetros asignados a un tipo SQL de intervalo y no había ninguna representación del valor del tipo C en el tipo SQL de intervalo. * \**<br /><br /> La asignación de un parámetro de entrada/salida o salida que era un tipo SQL numérico o de intervalo exacto a un tipo de intervalo C causó una pérdida de dígitos significativos.<br /><br /> Cuando se asignó un parámetro de entrada/salida o salida a una estructura de intervalo C, no había ninguna representación de los datos en la estructura de datos de intervalo.|  
|22018|Valor de carácter no válido para la especificación de conversión|StatementText contenía un tipo C que era un número exacto o aproximado, un datetime o un tipo de datos de intervalo; * \** el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna no era un literal válido del tipo C enlazado.<br /><br /> Cuando se devolvía un parámetro de entrada/salida o salida, el tipo SQL era un tipo de datos numérico exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo C se SQL_C_CHAR; y el valor de la columna no era un literal válido del tipo SQL enlazado.|  
|22019|Carácter de escape no válido|La instrucción preparada asociada con *StatementHandle* contenía un predicado **LIKE** con un **ESCAPE** en la cláusula **WHERE** y la longitud del carácter de escape que sigue a **ESCAPE** no era igual a 1.|  
|22025|Secuencia de escape no válida|La instrucción preparada asociada con *StatementHandle* contenía **"LIKE** _pattern value_ **ESCAPE** _escape character"_ en la cláusula **WHERE** y el carácter que sigue al carácter de escape en el valor de patrón no era uno de "%" o "_".|  
|23000|Violación de la restricción de integridad|La instrucción preparada asociada a *StatementHandle* contenía un parámetro. El valor del parámetro era NULL para una columna definida como NOT NULL en la columna de tabla asociada, se proporcionó un valor duplicado para una columna restringida para contener solo valores únicos o se violó alguna otra restricción de integridad.|  
|24000|Estado de cursor no válido|SQLFetch o **SQLFetchScroll**colocaron un cursor en *StatementHandle.* **SQLFetch** El Administrador de controladores devuelve este error si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y lo devuelve el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.<br /><br /> Se ha abierto un cursor en *StatementHandle*.<br /><br /> La instrucción preparada asociada con el *StatementHandle* contenía una actualización posicionada o eliminar aestaro,t y el cursor se colocó antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis o violación de acceso|El usuario no tenía permiso para ejecutar la instrucción preparada asociada con *StatementHandle*.|  
|44000|Infracción de WITH CHECK OPTION|La instrucción preparada asociada a *StatementHandle* contenía una instrucción **INSERT** realizada en una tabla vista o una tabla derivada de la tabla vista que se creó especificando **WITH CHECK OPTION**, de forma que una o varias filas afectadas por la instrucción **INSERT** ya no estarán presentes en la tabla vista.<br /><br /> La instrucción preparada asociada a *StatementHandle* contenía una instrucción **UPDATE** realizada en una tabla vista o en una tabla derivada de la tabla vista que se creó especificando **WITH CHECK OPTION**, de modo que una o varias filas afectadas por la instrucción **UPDATE** ya no estarán presentes en la tabla vista.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLExecute.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) El *StatementHandle* no fue preparado.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|Un valor de parámetro, establecido con **SQLBindParameter**, era un puntero nulo y el valor de longitud del parámetro no era 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valor de parámetro, establecido con **SQLBindParameter**, no era un puntero nulo; el tipo de datos C era SQL_C_BINARY o SQL_C_CHAR; y el valor de longitud del parámetro era menor que 0 pero no era SQL_NTS, SQL_NULL_DATA, SQL_DEFAULT_PARAM o SQL_DATA_AT_EXEC, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valor de longitud de parámetro enlazado por **SQLBindParameter** se estableció en SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo; y el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo** era "Y".|  
|HY105|Tipo de parámetro no válido|El valor especificado para el argumento *InputOutputType* en **SQLBindParameter** se SQL_PARAM_OUTPUT y el parámetro era un parámetro de entrada.|  
|HY109|Posición del cursor no válida|La instrucción preparada era una instrucción de actualización o eliminación posicionada y el cursor se colocó (por **SQLSetPos** o **SQLFetchScroll**) en una fila que se había eliminado o no se pudo recuperar.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 **SQLExecute** puede devolver cualquier SQLSTATE que **SQLPrepare**pueda devolver, en función de cuándo el origen de datos evalúa la instrucción SQL asociada a la instrucción.  
  
## <a name="comments"></a>Comentarios  
 **SQLExecute** ejecuta una instrucción preparada por **SQLPrepare**. Después de que la aplicación procesa o descarta los resultados de una llamada a **SQLExecute**, la aplicación puede llamar a **SQLExecute** de nuevo con nuevos valores de parámetro. Para obtener más información acerca de la ejecución preparada, vea [Ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
 Para ejecutar una instrucción **SELECT** más de una vez, la aplicación debe llamar a **SQLCloseCursor** antes de volver a ejecutar la instrucción **SELECT.**  
  
 Si el origen de datos está en modo de confirmación manual (que requiere un inicio de transacción explícito) y aún no se ha iniciado una transacción, el controlador inicia una transacción antes de enviar la instrucción SQL. Para más información, consulte [Transacciones](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Si una aplicación utiliza **SQLPrepare** para preparar y **SQLExecute** para enviar una instrucción **COMMIT** o **ROLLBACK,** no será interoperable entre los productos DBMS. Para confirmar o revertir una transacción, llame a **SQLEndTran**.  
  
 Si **SQLExecute** encuentra un parámetro de datos en ejecución, devuelve SQL_NEED_DATA. La aplicación envía los datos mediante **SQLParamData** y **SQLPutData**. Vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)y [Enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Si **SQLExecute** ejecuta una instrucción de actualización, inserción o eliminación buscada que no afecta a ninguna fila del origen de datos, la llamada a **SQLExecute** devuelve SQL_NO_DATA.  
  
 Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1 y la instrucción SQL contiene al menos un marcador de parámetro, **SQLExecute** ejecuta la instrucción SQL una vez para cada conjunto de valores de parámetro en las matrices señaladas por el * \*ParameterValuePtr* argumento en las llamadas a **SQLBindParameter**. Para obtener más información, consulte [Matrices de valores de parámetros](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Si los marcadores están habilitados y se ejecuta una consulta que no admite marcadores, el controlador debe intentar coaccionar el entorno a uno que admita marcadores cambiando un valor de atributo y devolviendo SQLSTATE 01S02 (valor de opción cambiado). Si no se puede cambiar el atributo, el controlador debe devolver SQLSTATE HY024 (valor de atributo no válido).  
  
> [!NOTE]  
>  Cuando se usa la agrupación de conexiones, una aplicación no debe ejecutar instrucciones SQL que cambien la base de datos o el contexto de la base de datos, como la instrucción **USE** _database_ en SQL ServerSQL Server, que cambia el catálogo utilizado por un origen de datos.  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)y [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Cierre del cursor|[Función SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Ejecución de una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Obtención de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Liberar un identificador de declaración|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Devolver un nombre de cursor|[Función SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Obtención de parte o la totalidad de una columna de datos|[Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Devolver el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Preparación de una declaración para la ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Envío de datos de parámetros en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
