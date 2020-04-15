---
title: Función SQLExecDirect (SQLExecDirect) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecDirect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecDirect
helpviewer_keywords:
- SQLExecDirect function [ODBC]
ms.assetid: 985fcee1-f204-425c-bdd1-deb0e7d7bbd9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5739e397467deb684a4cd6c7b13a507f30b53fa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286115"
---
# <a name="sqlexecdirect-function"></a>Función SQLExecDirect
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLExecDirect** ejecuta una instrucción preparable, utilizando los valores actuales de las variables de marcador de parámetro si existen parámetros en la instrucción. **SQLExecDirect** es la forma más rápida de enviar una instrucción SQL para la ejecución única.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *StatementText*  
 [Entrada] Instrucción SQL que se va a ejecutar.  
  
 *TextLength*  
 [Entrada] Longitud de **StatementText* en caracteres.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLExecDirect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLExecDirect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflicto de operación del cursor|\**StatementText* contenía una instrucción update o delete posicionada, y no se actualizaron o eliminaron filas o más de una fila. (Para obtener más información acerca de las actualizaciones de más de una fila, vea la descripción del *atributo* SQL_ATTR_SIMULATE_CURSOR en **SQLSetStmtAttr**.)<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01003|Valor NULL eliminado en la función set|El argumento *StatementText* contenía una función set (como **AVG**, **MAX**, **MIN**, etc.), pero no la función **COUNT** set y los valores de argumento NULL se eliminaron antes de aplicar la función. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|Los datos de cadena o binarios devueltos para un parámetro de entrada/salida o salida dieron como resultado el truncamiento de caracteres no en blanco o datos binarios no NULL. Si era un valor de cadena, se truncaba a la derecha. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01006|Privilegio no revocado|\**StatementText* contenía una instrucción **REVOKE** y el usuario no tenía el privilegio especificado. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01007|Privilegio no concedido|StatementText era una instrucción **GRANT** y no se podía conceder al usuario el privilegio especificado. * \**|  
|01S02|Valor de opción cambiado|Un atributo de instrucción especificado no era válido debido a las condiciones de trabajo de implementación, por lo que se sustituyó temporalmente un valor similar. (**SQLGetStmtAttr** se puede llamar para determinar cuál es el valor sustituido temporalmente.) El valor sustituto es válido para *StatementHandle* hasta que se cierra el cursor, momento en el que el atributo de instrucción vuelve a su valor anterior. Los atributos de instrucción que se pueden cambiar son:<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamiento fraccionario|Los datos devueltos para un parámetro de entrada/salida o salida se truncaron de modo que la parte fraccionaria de un tipo de datos numérico se truncó o se truncó la parte fraccionaria del componente de tiempo de un tipo de datos de tiempo, marca de tiempo o intervalo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07002|Campo COUNT incorrecto|El número de parámetros especificado en **SQLBindParameter** era menor que el \*número de parámetros de la instrucción SQL contenida en *StatementText*.<br /><br /> **SQLBindParameter** se llamó con *ParameterValuePtr* establecido en un puntero nulo, *no StrLen_or_IndPtr* establecido en SQL_NULL_DATA o SQL_DATA_AT_EXEC y *InputOutputType* no establecido en SQL_PARAM_OUTPUT, por lo que el número de parámetros especificados en **SQLBindParameter** era mayor que el número de parámetros de la instrucción SQL contenida en **StatementText*.|  
|07006|Infracción de atributo de tipo de datos restringido|El valor de datos identificado por el *ValueType* argumento en **SQLBindParameter** para el parámetro enlazado no se pudo convertir al tipo de datos identificado por el *ParameterType* argumento en **SQLBindParameter**.<br /><br /> El valor de datos devuelto para un parámetro enlazado como SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT no se pudo convertir al tipo de datos identificado por el *ValueType* argumento en **SQLBindParameter**.<br /><br /> (Si los valores de datos de una o más filas no se pudieron convertir, pero se devolvieron correctamente una o varias filas, esta función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07007|Infracción del valor de parámetro restringido|El tipo de parámetro SQL_PARAM_INPUT_OUTPUT_STREAM solo se utiliza para un parámetro que envía y recibe datos en partes. No se permite un búfer enlazado de entrada para este tipo de parámetro.<br /><br /> Este error se producirá cuando se SQL_PARAM_INPUT_OUTPUT \*el tipo de parámetro y cuando el *StrLen_or_IndPtr* especificado en **SQLBindParameter** no es igual a SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_LEN_DATA_AT_EXEC(len) o SQL_DATA_AT_EXEC.|  
|07S01|Uso no válido del parámetro predeterminado|Un valor de parámetro, establecido con **SQLBindParameter**, se SQL_DEFAULT_PARAM y el parámetro correspondiente no tenía un valor predeterminado.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|21S01|Insertar lista de valores no coincide con la lista de columnas|\**StatementText* contenía una instrucción **INSERT** y el número de valores que se insertarán no coincidía con el grado de la tabla derivada.|  
|21S02|El grado de la tabla derivada no coincide con la lista de columnas|\**StatementText* contenía una instrucción **CREATE VIEW** y la lista de columnas no calificadas (el número de columnas especificadas para la vista en los argumentos de identificador de *columna* de la instrucción SQL) contenía más nombres que el número de columnas de la tabla derivada definida por el argumento *de especificación* de consulta de la instrucción SQL.|  
|22001|Datos de cadena, truncamiento a la derecha|La asignación de un carácter o valor binario a una columna dio lugar a la truncación de datos de caracteres no en blanco o datos binarios no nulos.|  
|22002|Variable indicador requerida pero no suministrada|Null datos se enlazan a un parámetro de salida cuya *StrLen_or_IndPtr* establecido por **SQLBindParameter** era un puntero nulo.|  
|22003|Valor numérico fuera del rango|**StatementText* contenía una instrucción SQL que contenía un parámetro numérico enlazado o literal, y el valor hizo que toda la parte (en lugar de fraccionaria) del número se truncase cuando se asigna a la columna de tabla asociada.<br /><br /> Devolver un valor numérico (como numérico o cadena) para uno o más parámetros de entrada/salida o salida habría provocado que se truncase la parte total (en lugar de fracción) del número.|  
|22007|Formato de fecha y hora no válido|**StatementText* contenía una instrucción SQL que contenía una estructura de fecha, hora o marca de tiempo como parámetro enlazado, y el parámetro era, respectivamente, una fecha, hora o marca de tiempo no válida.<br /><br /> Un parámetro de entrada/salida o salida se enlazaba a una estructura C de fecha, hora o marca de tiempo, y un valor en el parámetro devuelto era, respectivamente, una fecha, hora o marca de tiempo no válida. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|22008|Desbordamiento de campo de fecha y hora|**StatementText* contenía una instrucción SQL que contenía una expresión datetime que, cuando se calculaba, daba como resultado una estructura de fecha, hora o marca de tiempo que no era válida.<br /><br /> Una expresión datetime calculada para un parámetro de entrada/salida o salida dio como resultado una estructura C de fecha, hora o marca de tiempo que no era válida.|  
|22012|División por cero|**StatementText* contenía una instrucción SQL que contenía una expresión aritmética que provocaba la división por cero.<br /><br /> Una expresión aritmética calculada para un parámetro de entrada/salida o salida dio como resultado la división por cero.|  
|22015|Desbordamiento de campo de intervalo|StatementText contenía un parámetro numérico o de intervalo exacto que, cuando se convierte en un tipo de datos SQL de intervalo, causó una pérdida de dígitos significativos. * \**<br /><br /> StatementText contenía un parámetro interval con más de un campo que, cuando se convierte en un tipo de datos numérico en una columna, no tenía ninguna representación en el tipo de datos numérico. * \**<br /><br /> StatementText contenía datos de parámetros asignados a un tipo SQL de intervalo y no había ninguna representación del valor del tipo C en el tipo SQL de intervalo. * \**<br /><br /> La asignación de un parámetro de entrada/salida o salida que era un tipo SQL numérico o de intervalo exacto a un tipo de intervalo C causó una pérdida de dígitos significativos.<br /><br /> Cuando se asignó un parámetro de entrada/salida o salida a una estructura de intervalo C, no había ninguna representación de los datos en la estructura de datos de intervalo.|  
|22018|Valor de carácter no válido para la especificación de conversión|StatementText contenía un tipo C que era un número exacto o aproximado, un datetime o un tipo de datos de intervalo; * \** el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna no era un literal válido del tipo C enlazado.<br /><br /> Cuando se devolvía un parámetro de entrada/salida o salida, el tipo SQL era un tipo de datos numérico exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo C se SQL_C_CHAR; y el valor de la columna no era un literal válido del tipo SQL enlazado.|  
|22019|Carácter de escape no válido|\**StatementText* contenía una instrucción SQL que contenía un predicado **LIKE** con un **ESCAPE** en la cláusula **WHERE** y la longitud del carácter de escape que sigue a **ESCAPE** no era igual a 1.|  
|22025|Secuencia de escape no válida|\**StatementText* contenía una instrucción SQL que contenía "**LIKE** _pattern value_ **ESCAPE** _escape character_" en la cláusula **WHERE,** y el carácter que sigue al carácter de escape en el valor de patrón no era uno de "%" o "_".|  
|23000|Violación de la restricción de integridad|**StatementText* contenía una instrucción SQL que contenía un parámetro o literal. El valor del parámetro era NULL para una columna definida como NOT NULL en la columna de tabla asociada, se proporcionó un valor duplicado para una columna restringida para contener solo valores únicos o se violó alguna otra restricción de integridad.|  
|24000|Estado de cursor no válido|SQLFetch o **SQLFetchScroll**colocaron un cursor en *StatementHandle.* **SQLFetch** El Administrador de controladores devuelve este error si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y lo devuelve el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.<br /><br /> Un cursor estaba abierto pero no colocado en *StatementHandle*.<br /><br /> **StatementText* contenía una instrucción update o delete posicionada, y el cursor se colocó antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|34000|Nombre de cursor no válido|**StatementText* contenía una instrucción update o delete posicionada, y el cursor al que hace referencia la instrucción que se está ejecutando no estaba abierto.|  
|3D000|Nombre de catálogo no válido|El nombre del catálogo especificado en *StatementText* no era válido.|  
|3F000|Nombre de esquema no válido|El nombre de esquema especificado en *StatementText* no era válido.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis o violación de acceso|\**StatementText* contenía una instrucción SQL que no se puede preparar o contiene un error de sintaxis.<br /><br /> El usuario no tenía permiso para ejecutar la instrucción SQL contenida en **StatementText*.|  
|42S01|La tabla base o la vista ya existen|\**StatementText* contenía una instrucción **CREATE TABLE** o **CREATE VIEW,** y el nombre de tabla o el nombre de vista especificado ya existe.|  
|42S02|Tabla base o vista no encontrada|\**StatementText* contenía una **instrucción DROP TABLE** o **DROP VIEW,** y el nombre de tabla o el nombre de vista especificados no existían.<br /><br /> \**StatementText* contenía una instrucción **ALTER TABLE** y el nombre de tabla especificado no existía.<br /><br /> \**StatementText* contenía una instrucción **CREATE VIEW** y no existía un nombre de tabla o un nombre de vista definido por la especificación de consulta.<br /><br /> \**StatementText* contenía una instrucción **CREATE INDEX** y el nombre de tabla especificado no existía.<br /><br /> \**StatementText* contenía una instrucción **GRANT** o **REVOKE** y el nombre de tabla o el nombre de vista especificados no existían.<br /><br /> \**StatementText* contenía una instrucción **SELECT** y no existía un nombre de tabla o un nombre de vista especificado.<br /><br /> \**StatementText* contenía una instrucción **DELETE**, **INSERT**o **UPDATE** y el nombre de tabla especificado no existía.<br /><br /> \**StatementText* contenía una instrucción **CREATE TABLE** y no existía una tabla especificada en una restricción (que hacía referencia a una tabla distinta de la que se está creando).<br /><br /> \**StatementText* contenía una instrucción **CREATE SCHEMA** y no existía un nombre de tabla o un nombre de vista especificado.|  
|42S11|El índice ya existe|\**StatementText* contenía una instrucción **CREATE INDEX** y el nombre de índice especificado ya existía.<br /><br /> \**StatementText* contenía una instrucción **CREATE SCHEMA** y el nombre de índice especificado ya existía.|  
|42S12|Indice no encontrado|\**StatementText* contenía una instrucción **DROP INDEX** y el nombre de índice especificado no existía.|  
|42S21|Columna ya existe|\**StatementText* contenía una instrucción **ALTER TABLE** y la columna especificada en la cláusula **ADD** no es única o identifica una columna existente en la tabla base.|  
|42S22|Columna no encontrada|\**StatementText* contenía una instrucción **CREATE INDEX** y uno o varios de los nombres de columna especificados en la lista de columnas no existían.<br /><br /> \**StatementText* contenía una instrucción **GRANT** o **REVOKE** y no existía un nombre de columna especificado.<br /><br /> \**StatementText* contenía una instrucción **SELECT**, **DELETE**, **INSERT**o **UPDATE** y no existía un nombre de columna especificado.<br /><br /> \**StatementText* contenía una instrucción **CREATE TABLE** y no existía una columna especificada en una restricción (que hacía referencia a una tabla distinta de la que se está creando).<br /><br /> \**StatementText* contenía una instrucción **CREATE SCHEMA** y no existía un nombre de columna especificado.|  
|44000|Infracción de WITH CHECK OPTION|El argumento *StatementText* contenía una instrucción **INSERT** realizada en una tabla vista o una tabla derivada de la tabla vista que se creó especificando **WITH CHECK OPTION**, de forma que una o varias filas afectadas por la instrucción **INSERT** ya no estarán presentes en la tabla vista.<br /><br /> El argumento *StatementText* contenía una instrucción **UPDATE** realizada en una tabla vista o una tabla derivada de la tabla vista que se creó especificando **WITH CHECK OPTION**, de modo que una o varias filas afectadas por la instrucción **UPDATE** ya no estarán presentes en la tabla vista.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|(DM) **StatementText* era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLExecDirect** .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El argumento *TextLength* era menor o igual que 0 pero no igual a SQL_NTS.<br /><br /> Un valor de parámetro, establecido con **SQLBindParameter**, era un puntero nulo y el valor de longitud del parámetro no era 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valor de parámetro, establecido con **SQLBindParameter**, no era un puntero nulo; el tipo de datos C era SQL_C_BINARY o SQL_C_CHAR; y el valor de longitud del parámetro era menor que 0 pero no era SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valor de longitud de parámetro enlazado por **SQLBindParameter** se estableció en SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo; y el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo** era "Y".|  
|HY105|Tipo de parámetro no válido|El valor especificado para el argumento *InputOutputType* en **SQLBindParameter** se SQL_PARAM_OUTPUT y el parámetro era un parámetro de entrada.|  
|HY109|Posición del cursor no válida|\**StatementText* contenía una instrucción update o delete posicionada y el cursor se colocó (por **SQLSetPos** o **SQLFetchScroll**) en una fila que se había eliminado o no se pudo recuperar.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 La aplicación llama a **SQLExecDirect** para enviar una instrucción SQL al origen de datos. Para obtener más información acerca de la ejecución directa, consulte [Ejecución directa](../../../odbc/reference/develop-app/direct-execution-odbc.md). El controlador modifica la instrucción para usar la forma de SQL utilizada por el origen de datos y, a continuación, la envía al origen de datos. En particular, el controlador modifica las secuencias de escape utilizadas para definir ciertas características en SQL. Para obtener la sintaxis de las secuencias de escape, vea [Secuencias](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)de escape en ODBC .  
  
 La aplicación puede incluir uno o varios marcadores de parámetro en la instrucción SQL. Para incluir un marcador de parámetro, la aplicación incrusta un signo de interrogación (?) en la instrucción SQL en la posición adecuada. Para obtener información sobre los parámetros, consulte [Parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Si la instrucción SQL es una instrucción **SELECT** y si la aplicación denominada **SQLSetCursorName** para asociar un cursor a una instrucción, el controlador utiliza el cursor especificado. De lo contrario, el controlador genera un nombre de cursor.  
  
 Si el origen de datos está en modo de confirmación manual (que requiere un inicio de transacción explícito) y aún no se ha iniciado una transacción, el controlador inicia una transacción antes de enviar la instrucción SQL. Para obtener más información, consulte [Modo de confirmación manual](../../../odbc/reference/develop-app/manual-commit-mode.md).  
  
 Si una aplicación utiliza **SQLExecDirect** para enviar una instrucción **COMMIT** o **ROLLBACK,** no será interoperable entre los productos DBMS. Para confirmar o revertir una transacción, una aplicación llama a **SQLEndTran**.  
  
 Si **SQLExecDirect** encuentra un parámetro de datos en ejecución, devuelve SQL_NEED_DATA. La aplicación envía los datos mediante **SQLParamData** y **SQLPutData**. Vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)y [Enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Si **SQLExecDirect** ejecuta una instrucción de actualización, inserción o eliminación buscada que no afecta a ninguna fila en el origen de datos, la llamada a **SQLExecDirect** devuelve SQL_NO_DATA.  
  
 Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1 y la instrucción SQL contiene al menos un marcador de parámetro, **SQLExecDirect** ejecutará la instrucción SQL una vez para cada conjunto de valores de parámetro de las matrices señaladas por el *ParameterValuePointer* argumento en la llamada a **SQLBindParameter**. Para obtener más información, consulte [Matrices de valores de parámetros](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Si los marcadores están activados y se ejecuta una consulta que no admite marcadores, el controlador debe intentar coaccionar el entorno a uno que admita marcadores cambiando un valor de atributo y devolviendo SQLSTATE 01S02 (valor de opción cambiado). Si no se puede cambiar el atributo, el controlador debe devolver SQLSTATE HY024 (valor de atributo no válido).  
  
> [!NOTE]  
>  Cuando se usa la agrupación de conexiones, una aplicación no debe ejecutar instrucciones SQL que cambien la base de datos o el contexto de la base de datos, como la instrucción **USE** _database_ en SQL ServerSQL Server, que cambia el catálogo utilizado por un origen de datos.  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)y [Programa ODBC](../../../odbc/reference/sample-odbc-program.md)de ejemplo .  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecución de una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Obtención de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
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
