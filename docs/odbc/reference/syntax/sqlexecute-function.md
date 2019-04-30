---
title: Función SQLExecute | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad8aec58fea182c080d55217db94ea2cda08184b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259241"
---
# <a name="sqlexecute-function"></a>Función SQLExecute
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLExecute** ejecuta una instrucción preparada, con los valores actuales de las variables de marcador de parámetro si los marcadores de parámetros existen en la instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLExecute(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLExecute** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLExecute** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01001|Conflicto de operación de cursor|La instrucción preparada asociada con el *StatementHandle* contenida en una posición instrucción update o delete, y no hay filas o más de una fila se eliminó o actualizó. (Para obtener más información acerca de las actualizaciones a más de una fila, vea la descripción de la SQL_ATTR_SIMULATE_CURSOR *atributo* en **SQLSetStmtAttr**.)<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01003|Valor NULL eliminado en la función Set.|La instrucción preparada asociada *StatementHandle* contenía una función de conjunto (como **AVG**, **MAX**, **MIN**, y así sucesivamente), pero no el **recuento** establecer función y el argumento nulo se eliminaron los valores antes de aplica la función. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Cadena o datos binarios devueltos para un parámetro de salida como resultado el truncamiento de carácter no en blanco o datos binarios que no son NULL. Si fuese un valor de cadena, era truncado a la derecha. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01006|Privilegio no revocado|La instrucción preparada asociada con el *StatementHandle* era un **REVOCAR** instrucción y el usuario no tiene el privilegio especificado. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01007|Privilegio no concedido|La instrucción preparada asociada con el *StatementHandle* era un **GRANT** instrucción y el usuario no se podrían conceder el privilegio especificado.|  
|01S02|Valor de opción cambiado|Un atributo de instrucción especificado no era válido debido a las condiciones de trabajo de implementación, por lo que temporalmente se ha sustituido por un valor similar. (**SQLGetStmtAttr** se puede llamar para determinar cuál es el valor sustituido temporalmente.) El valor de reemplazo es válido para el *StatementHandle* hasta que se cierra el cursor, momento en que el atributo de instrucción revierte a su valor anterior. Los atributos de instrucción que se pueden cambiar son: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT y SQL_ATTR_SIMULATE_CURSOR. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S07|Truncamiento fraccionario|Los datos devueltos para una entrada y salida o se truncó el parámetro de salida que se trunca la parte fraccionaria de un tipo de datos numéricos o se trunca la parte fraccionaria del componente de un tipo de datos de hora, marca de tiempo o intervalo de tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07002|Campo COUNT incorrecto|El número de parámetros especificados en **SQLBindParameter** era menor que el número de parámetros en la instrucción SQL contenidas en \* *StatementText*.<br /><br /> **SQLBindParameter** se llamó con *ParameterValuePtr* establecido en un puntero nulo, *StrLen_or_IndPtr* no establecido en SQL_NULL_DATA o SQL_DATA_AT_EXEC, y *InputOutputType*  no se establece en SQL_PARAM_OUTPUT, para que el número de parámetros especificado en **SQLBindParameter** era mayor que el número de parámetros en la instrucción SQL contenidas en **StatementText* .|  
|07006|Infracción del atributo de tipo de datos restringido|El valor de datos identificado por el *ValueType* argumento en **SQLBindParameter** para el parámetro dependiente no se pudo convertir al tipo de datos identificado por el *ParameterType*argumento en **SQLBindParameter**.<br /><br /> Devuelve el valor de datos para un parámetro de enlazado como SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT no se pudo convertir al tipo de datos identificado por el *ValueType* argumento en **SQLBindParameter**.<br /><br /> (Si no se podrían convertir los valores de datos para una o varias filas, pero una o más filas se devolvieron correctamente, esta función devuelve SQL_SUCCESS_WITH_INFO).|  
|07007|Infracción de valor de parámetro restringido|El tipo de parámetro SQL_PARAM_INPUT_OUTPUT_STREAM solo se usa para un parámetro que se envía y recibe datos en partes. No se permite un búfer de entrada enlazado para este tipo de parámetro.<br /><br /> Este error se produce cuando el tipo de parámetro es SQL_PARAM_INPUT_OUTPUT y cuando la \* *StrLen_or_IndPtr* especificado en **SQLBindParameter** no es igual a SQL_NULL_DATA, SQL_DEFAULT_ PARAM, SQL_LEN_DATA_AT_EXEC(len) o SQL_DATA_AT_EXEC.|  
|07S01|Uso no válido de parámetro predeterminado|Establece un valor de parámetro, con **SQLBindParameter**, era SQL_DEFAULT_PARAM y el parámetro correspondiente no es un parámetro para una invocación del procedimiento canónica de ODBC.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|21S02|Grado de la tabla derivada no coincide con la lista de columnas|La instrucción preparada asociada con el *StatementHandle* contenidos un **CREATE VIEW** instrucción y la lista de columnas incompletas (el número de columnas especificadas de la vista en el  *identificador de la columna* argumentos de la instrucción SQL) contiene los nombres más que el número de columnas en la tabla derivada definida por el *especificación de consulta* argumento de la instrucción SQL.|  
|22001|Cadena de datos, truncamiento por la derecha|La asignación de un carácter o un valor binario a una columna producía el truncamiento de no están en blanco (carácter) o distinto de null (binarios) caracteres o bytes.|  
|22002|Variable de indicador necesaria pero no proporcionado|Datos nulos estaba enlazados a un parámetro de salida cuyo *StrLen_or_IndPtr* establecido por **SQLBindParameter** era un puntero nulo.|  
|22003|Valor numérico fuera del intervalo|La instrucción preparada asociada con el *StatementHandle* contiene un parámetro numérico enlazado y el valor del parámetro ocasiona la parte entera (en contraposición a fraccionarios) el número que se truncan cuando se asigna a la categoría asociada columna de tabla.<br /><br /> Devuelve un valor numérico (como numérico o cadena) para uno o más parámetros de entrada y salida o de salida habría causado la parte entera (en contraposición a fraccionarios) del número que se va a truncar.|  
|22007|Formato de datetime no válido|La instrucción preparada asociada con el *StatementHandle* contenía una instrucción SQL que contiene una fecha, hora o estructura de marca de tiempo como un parámetro dependiente, y el parámetro era, respectivamente, una fecha no válida, hora, o marca de tiempo.<br /><br /> Un parámetro de entrada y salida o de salida estaba enlazado a una fecha, hora o estructura de marca de tiempo C, y un valor en el parámetro devuelto era, respectivamente, una fecha no válida, la hora o marca de tiempo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22008|Desbordamiento del campo DateTime|La instrucción preparada asociada con el *StatementHandle* independiente de una instrucción SQL que contiene una expresión de fecha y hora que, cuando se calcula que dieron lugar a una fecha, hora o marca de tiempo de estructura que no era válida.<br /><br /> Calcula una expresión de fecha y hora para una entrada y salida o parámetro de salida dieron lugar a una fecha, hora o estructura de C de la marca de tiempo que no era válido.|  
|22012|División por cero|La instrucción preparada asociada con el *StatementHandle* contiene una expresión aritmética que ha provocado la división por cero.<br /><br /> Una expresión aritmética calculado para una entrada y salida o parámetro de salida dio como resultado de división por cero.|  
|22015|Desbordamiento de campo de intervalo|*\*StatementText* contiene un parámetro numérico o de intervalo exacto que, cuando se convierte en un intervalo del tipo de datos SQL, causó una pérdida de dígitos significativos.<br /><br /> *\*StatementText* contiene un parámetro de intervalo con más de un campo que, cuando se convierte en un tipo de datos numéricos en una columna, no tenía ninguna representación del tipo de datos numérico.<br /><br /> *\*StatementText* contenía datos de parámetro que se asignó a un intervalo de tipo SQL y no había ninguna representación del valor del tipo C en el intervalo de tipo SQL.<br /><br /> Asignación de un parámetro de entrada y salida o de salida que era un valor numérico exacto o intervalo de tipo SQL a un tipo de intervalo C causado una pérdida de dígitos significativos.<br /><br /> Cuando un parámetro de entrada y salida o de salida se asigna a una estructura de intervalo de C, no hubo ninguna representación de los datos de la estructura de datos de intervalo.|  
|22018|Valor de carácter no válido para especificación cast|*\*StatementText* contenía un tipo de C que era un numérico exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor de la columna no era un literal válido de tipo C enlazado.<br /><br /> Cuando se devuelve un parámetro de entrada y salida o de salida, el tipo SQL era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo de C era SQL_C_CHAR; y el valor de la columna no es un literal válido del tipo SQL enlazado.|  
|22019|Carácter de escape no válido|La instrucción preparada asociada *StatementHandle* contenidos un **como** predicado con un **ESCAPE** en el **donde** cláusula, y la longitud de los siguientes caracteres de escape **ESCAPE** no es igual a 1.|  
|22025|Secuencia de escape no válido|La instrucción preparada asociada *StatementHandle* contenidos "**como** _valor de patrón_ **ESCAPE** _escape carácter_"en el **donde** cláusula y el carácter que sigue el carácter de escape en el valor de patrón no era uno de"%"o"_".|  
|23000|Infracción de restricción de integridad|La instrucción preparada asociada con el *StatementHandle* contiene un parámetro. El valor del parámetro era NULL para una columna definida como NOT NULL en la columna de tabla asociada, se proporcionó un valor duplicado para una columna que se restringen para contener solo valores únicos o se infringió alguna otra restricción de integridad.|  
|24000|Estado de cursor no válido|Un cursor se coloca en el *StatementHandle* por **SQLFetch** o **SQLFetchScroll**. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*.<br /><br /> La instrucción preparada asociada con el *StatementHandle* contiene una actualización por posición o eliminar statemen, t y el cursor se coloca antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis, infracción de acceso|El usuario no tiene permiso para ejecutar la instrucción preparada asociada con el *StatementHandle*.|  
|44000|Infracción de WITH CHECK OPTION|La instrucción preparada asociada *StatementHandle* contiene un **insertar** instrucción puede realizadas en una tabla vista o una tabla derivada de la tabla mostrada en la que se creó mediante la especificación de **WITH CHECK OPTION**, de modo que uno o más filas afectadas por la **insertar** instrucción ya no estará presente en la tabla mostrada.<br /><br /> La instrucción preparada asociada con el *StatementHandle* contiene un **actualización** instrucción puede realizadas en una tabla vista o una tabla derivada de la tabla mostrada en la que se creó mediante la especificación de **WITH CHECK OPTION**, de modo que uno o más filas afectadas por la **actualización** instrucción ya no estará presente en la tabla mostrada.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLExecute** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) el *StatementHandle* no estaba preparado.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|Establece un valor de parámetro, con **SQLBindParameter**, era un puntero nulo y no es el valor de parámetro de longitud 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Establece un valor de parámetro, con **SQLBindParameter**, no era un puntero nulo; el tipo de datos C era SQL_C_BINARY o SQL_C_CHAR; y el valor de parámetro de longitud era menor que 0 pero no era SQL_NTS, SQL_NULL_DATA, SQL_DEFAULT_PARAM o SQL_DATA_ AT_EXEC, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valor de longitud del parámetro enlazado por **SQLBindParameter** estaba establecido en SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY, o un tipo de datos específicos del origen de datos long; y la información de SQL_NEED_LONG_DATA_LEN Escriba en **SQLGetInfo** era "S".|  
|HY105|Tipo de parámetro no válido|El valor especificado para el argumento *InputOutputType* en **SQLBindParameter** era SQL_PARAM_OUTPUT y el parámetro era un parámetro de entrada.|  
|HY109|Posición del cursor no válido|La instrucción preparada era una actualización por posición o una instrucción delete, y se coloca el cursor (por **SQLSetPos** o **SQLFetchScroll**) en una fila que se había eliminada o no se pudo obtener.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y se ha establecido el atributo de instrucción SQL_ATTR_CURSOR_TYPE a un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 **SQLExecute** puede devolver cualquier SQLSTATE, que puede devolver **SQLPrepare**, en función de si el origen de datos se evalúa como la instrucción SQL asociada con la instrucción.  
  
## <a name="comments"></a>Comentarios  
 **SQLExecute** ejecuta una instrucción preparada por **SQLPrepare**. Después de la aplicación procesa o descarta los resultados de una llamada a **SQLExecute**, la aplicación puede llamar a **SQLExecute** nuevo con los nuevos valores de parámetro. Para obtener más información sobre la ejecución preparada, vea [ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
 Para ejecutar un **seleccione** instrucción más de una vez, la aplicación debe llamar a **SQLCloseCursor** antes deteniéndose el **seleccione** instrucción.  
  
 Si el origen de datos está en modo de confirmación manual (Requerir inicio de transacciones explícitas) y ya no se ha iniciado una transacción, el controlador inicia una transacción antes de enviar la instrucción SQL. Para obtener más información, consulte [transacciones](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Si una aplicación utiliza **SQLPrepare** para preparar y **SQLExecute** para enviar un **confirmar** o **reversión** instrucción, no será interoperar entre productos DBMS. Para confirmar o revertir una transacción, llamar a **SQLEndTran**.  
  
 Si **SQLExecute** encuentra un parámetro de datos en ejecución, devuelve SQL_NEED_DATA. La aplicación envía los datos mediante **SQLParamData** y **SQLPutData**. Consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), y [enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Si **SQLExecute** ejecuta una actualización por búsqueda, inserción o instrucción delete que no afecta a todas las filas en el origen de datos, la llamada a **SQLExecute** devuelve SQL_NO_DATA.  
  
 Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1 y la instrucción SQL contiene al menos un marcador de parámetro, **SQLExecute** ejecuta la instrucción SQL una vez para cada conjunto de valores de parámetros en las matrices que señala el  *\*ParameterValuePtr* argumento en las llamadas a **SQLBindParameter**. Para obtener más información, consulte [matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Si se habilitan los marcadores y se ejecuta una consulta que no es compatible con marcadores, el controlador debe intentar convertir el entorno a uno que admite marcadores al cambiar un valor de atributo y devolver 01S02 de SQLSTATE SQLSTATE (valor de opción cambiado). Si no se puede cambiar el atributo, el controlador debe devolver SQLSTATE HY024 (valor de atributo no válido).  
  
> [!NOTE]  
>  Cuando se usa la agrupación de conexiones, una aplicación no debe ejecutar instrucciones SQL que cambian la base de datos o en el contexto de la base de datos, como el **USE** _base de datos_ instrucción en SQL Server, que cambia el catálogo que se usa un origen de datos.  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), y [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Cierre el cursor|[Función SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Ejecutar una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Recopilación de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Liberar un identificador de instrucción|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Devuelve un nombre de cursor|[Función SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Capturando la totalidad o parte de una columna de datos|[Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Devuelve el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Preparar una instrucción de ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
