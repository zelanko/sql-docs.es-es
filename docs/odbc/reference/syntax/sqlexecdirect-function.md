---
title: Función SQLExecDirect | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ed580bd89dc7bf4c1f0af520f43f6ca8d616a1b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733733"
---
# <a name="sqlexecdirect-function"></a>Función SQLExecDirect
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: 92 ISO  
  
 **Resumen**  
 **SQLExecDirect** ejecuta una instrucción preparable, utilizando los valores actuales de las variables de marcador de parámetro, si existe algún parámetro en la instrucción. **SQLExecDirect** es la forma más rápida para enviar una instrucción SQL para ejecutar una sola vez.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *StatementText*  
 [Entrada] Instrucción SQL que se ejecutará.  
  
 *TextLength*  
 [Entrada] Longitud de **StatementText* en caracteres.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLExecDirect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLExecDirect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01001|Conflicto de operación de cursor|\**StatementText* contenida en una posición instrucción update o delete, y no hay filas o más de una fila se eliminó o actualizó. (Para obtener más información acerca de las actualizaciones a más de una fila, vea la descripción de la SQL_ATTR_SIMULATE_CURSOR *atributo* en **SQLSetStmtAttr**.)<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01003|Valor NULL eliminado en la función Set.|El argumento *StatementText* contenía una función de conjunto (como **AVG**, **MAX**, **MIN**, y así sucesivamente), pero no la **recuento**  establecer función y el argumento nulo se eliminaron los valores antes de aplica la función. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Cadena o datos binarios devuelven para una entrada y salida o parámetro de salida dieron como resultado el truncamiento de carácter no en blanco o datos binarios que no son NULL. Si fuese un valor de cadena, era truncado a la derecha. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01006|Privilegio no revocado|\**StatementText* contiene un **REVOCAR** instrucción y el usuario no tiene el privilegio especificado. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01007|Privilegio no concedido|*\*StatementText* era un **GRANT** instrucción y el usuario no se podrían conceder el privilegio especificado.|  
|01S02|Valor de opción cambiado|Un atributo de instrucción especificado no era válido debido a las condiciones de trabajo de implementación, por lo que temporalmente se ha sustituido por un valor similar. (**SQLGetStmtAttr** se puede llamar para determinar cuál es el valor sustituido temporalmente.) El valor de reemplazo es válido para el *StatementHandle* hasta que se cierra el cursor, momento en que el atributo de instrucción revierte a su valor anterior. Los atributos de instrucción que se pueden cambiar son:<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S07|Truncamiento fraccionario|Los datos devueltos para una entrada y salida o se truncó el parámetro de salida que se trunca la parte fraccionaria de un tipo de datos numéricos o se trunca la parte fraccionaria del componente de un tipo de datos de hora, marca de tiempo o intervalo de tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07002|Campo COUNT incorrecto|El número de parámetros especificados en **SQLBindParameter** era menor que el número de parámetros en la instrucción SQL contenidas en \* *StatementText*.<br /><br /> **SQLBindParameter** se llamó con *ParameterValuePtr* establecido en un puntero nulo, *StrLen_or_IndPtr* no establecido en SQL_NULL_DATA o SQL_DATA_AT_EXEC, y *InputOutputType*  no se establece en SQL_PARAM_OUTPUT, para que el número de parámetros especificado en **SQLBindParameter** era mayor que el número de parámetros en la instrucción SQL contenidas en **StatementText* .|  
|07006|Infracción del atributo de tipo de datos restringido|El valor de datos identificado por el *ValueType* argumento en **SQLBindParameter** para el parámetro dependiente no se pudo convertir al tipo de datos identificado por el *ParameterType*argumento en **SQLBindParameter**.<br /><br /> Devuelve el valor de datos para un parámetro de enlazado como SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT no se pudo convertir al tipo de datos identificado por el *ValueType* argumento en **SQLBindParameter**.<br /><br /> (Si no se podrían convertir los valores de datos para una o varias filas, pero una o más filas se devolvieron correctamente, esta función devuelve SQL_SUCCESS_WITH_INFO).|  
|07007|Infracción de valor de parámetro restringido|El tipo de parámetro SQL_PARAM_INPUT_OUTPUT_STREAM solo se usa para un parámetro que se envía y recibe datos en partes. No se permite un búfer de entrada enlazado para este tipo de parámetro.<br /><br /> Este error se produce cuando el tipo de parámetro es SQL_PARAM_INPUT_OUTPUT y cuando la \* *StrLen_or_IndPtr* especificado en **SQLBindParameter** no es igual a SQL_NULL_DATA, SQL_DEFAULT_ PARAM, SQL_LEN_DATA_AT_EXEC(len) o SQL_DATA_AT_EXEC.|  
|07S01|Uso no válido de parámetro predeterminado|Establece un valor de parámetro, con **SQLBindParameter**, era SQL_DEFAULT_PARAM y el parámetro correspondiente no tiene un valor predeterminado.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|21S01|Lista de valores insertados no coincide con la lista de columnas|\**StatementText* contiene un **insertar** instrucción y el número de valores que se va a insertar no coincidía con el grado de la tabla derivada.|  
|21S02|Grado de la tabla derivada no coincide con la lista de columnas|\**StatementText* contenidos un **CREATE VIEW** instrucción y la lista de columnas incompletas (el número de columnas especificadas de la vista en el *identificador de columna* argumentos de la instrucción SQL instrucción) contiene los nombres más que el número de columnas en la tabla derivada definida por el *especificación de consulta* argumento de la instrucción SQL.|  
|22001|Cadena de datos, truncamiento por la derecha|La asignación de un carácter o un valor binario a una columna producía el truncamiento de datos de caracteres que no esté vacía o datos binarios que no son null.|  
|22002|Variable de indicador necesaria pero no proporcionado|Datos nulos estaba enlazados a un parámetro de salida cuyo *StrLen_or_IndPtr* establecido por **SQLBindParameter** era un puntero nulo.|  
|22003|Valor numérico fuera del intervalo|**StatementText* contenía una instrucción SQL que contenían un parámetro numérico enlazado o literal y el valor ocasiona la parte entera (en contraposición a fraccionarios) el número que se truncan cuando se asigna a la columna de tabla asociada.<br /><br /> Devuelve un valor numérico (como numérico o cadena) para uno o más parámetros de entrada y salida o de salida habría causado la parte entera (en contraposición a fraccionarios) del número que se va a truncar.|  
|22007|Formato de datetime no válido|**StatementText* contenía una instrucción SQL que contiene una fecha, hora o estructura de marca de tiempo como un parámetro dependiente, y el parámetro era, respectivamente, una fecha no válida, la hora o marca de tiempo.<br /><br /> Un parámetro de entrada y salida o de salida estaba enlazado a una fecha, hora o estructura de marca de tiempo C, y un valor en el parámetro devuelto era, respectivamente, una fecha no válida, la hora o marca de tiempo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22008|Desbordamiento del campo DateTime|**StatementText* independiente de una instrucción SQL que contiene una expresión de fecha y hora que, cuando se calcula que dieron lugar a una fecha, hora o marca de tiempo de estructura que no era válida.<br /><br /> Calcula una expresión de fecha y hora para una entrada y salida o parámetro de salida dieron lugar a una fecha, hora o estructura de C de la marca de tiempo que no era válido.|  
|22012|División por cero|**StatementText* contenía una instrucción SQL que contiene una expresión aritmética que ha provocado la división por cero.<br /><br /> Una expresión aritmética calculado para una entrada y salida o parámetro de salida dio como resultado de división por cero.|  
|22015|Desbordamiento de campo de intervalo|*\*StatementText* contiene un parámetro numérico o de intervalo exacto que, cuando se convierte en un intervalo del tipo de datos SQL, causó una pérdida de dígitos significativos.<br /><br /> *\*StatementText* contiene un parámetro de intervalo con más de un campo que, cuando se convierte en un tipo de datos numéricos en una columna, no tenía ninguna representación del tipo de datos numérico.<br /><br /> *\*StatementText* contenía datos de parámetro que se asignó a un intervalo de tipo SQL y no había ninguna representación del valor del tipo C en el intervalo de tipo SQL.<br /><br /> Asignación de un parámetro de entrada y salida o de salida que era un valor numérico exacto o intervalo de tipo SQL a un tipo de intervalo C causado una pérdida de dígitos significativos.<br /><br /> Cuando un parámetro de entrada y salida o de salida se asigna a una estructura de intervalo de C, no hubo ninguna representación de los datos de la estructura de datos de intervalo.|  
|22018|Valor de carácter no válido para especificación cast|*\*StatementText* contenía un tipo de C que era un numérico exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor de la columna no era un literal válido de tipo C enlazado.<br /><br /> Cuando se devuelve un parámetro de entrada y salida o de salida, el tipo SQL era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo de C era SQL_C_CHAR; y el valor de la columna no es un literal válido del tipo SQL enlazado.|  
|22019|Carácter de escape no válido|\**StatementText* contenía una instrucción SQL que contenía una **como** predicado con un **ESCAPE** en el **donde** cláusula y la longitud del escape siguiente carácter **ESCAPE** no es igual a 1.|  
|22025|Secuencia de escape no válido|\**StatementText* contenía una instrucción SQL que contiene "**como** *valor de patrón* **ESCAPE** *carácter de escape* "en el **donde** cláusula y el carácter que sigue el carácter de escape en el valor de patrón no era uno de"%"o"_".|  
|23000|Infracción de restricción de integridad|**StatementText* contenía una instrucción SQL que incluye un parámetro o un literal. El valor del parámetro era NULL para una columna definida como NOT NULL en la columna de tabla asociada, se proporcionó un valor duplicado para una columna que se restringen para contener solo valores únicos o se infringió alguna otra restricción de integridad.|  
|24000|Estado de cursor no válido|Un cursor se coloca en el *StatementHandle* por **SQLFetch** o **SQLFetchScroll**. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto pero no está colocado en el *StatementHandle*.<br /><br /> **StatementText* contenida en una posición instrucción update o delete, y el cursor se coloca antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|34000|Nombre de cursor no válido|**StatementText* contenida en una posición instrucción update o delete, y no estaba abierto el cursor al que hace referencia la instrucción que se está ejecutando.|  
|3D000|Nombre del catálogo no válido|El nombre de catálogo especificado en *StatementText* no era válido.|  
|3F000|Nombre de esquema no válido|El nombre de esquema especificado en *StatementText* no era válido.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis, infracción de acceso|\**StatementText* contenía una instrucción SQL que no se ha preparable o contenía un error de sintaxis.<br /><br /> El usuario no tiene permiso para ejecutar la instrucción SQL contenida en **StatementText*.|  
|42S01|Tabla o vista base ya existe.|\**StatementText* contiene un **CREATE TABLE** o **CREATE VIEW** instrucción y el nombre de la tabla o vista de nombre especificado ya existe.|  
|42S02|No se encuentra la vista o tabla base|\**StatementText* contiene un **DROP TABLE** o un **DROP VIEW** instrucción y el nombre de la tabla especificada o vista de nombre no existe.<br /><br /> \**StatementText* contiene un **ALTER TABLE** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **CREATE VIEW** instrucción y un nombre de la tabla o vista no existía nombre definido por la especificación de consulta.<br /><br /> \**StatementText* contiene un **CREATE INDEX** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **GRANT** o **REVOCAR** instrucción y el nombre de la tabla especificada o vista de nombre no existe.<br /><br /> \**StatementText* contiene un **seleccione** instrucción y un nombre de tabla especificado o la vista de nombre no existe.<br /><br /> \**StatementText* contiene un **eliminar**, **insertar**, o **actualización** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **CREATE TABLE** no existía instrucción y una tabla especificada en una restricción (referencia a una tabla distinta que se va a crear).<br /><br /> \**StatementText* contiene un **CREATE SCHEMA** instrucción y un nombre de tabla especificado o la vista de nombre no existe.|  
|42S11|El índice ya existe|\**StatementText* contiene un **CREATE INDEX** instrucción y el nombre del índice especificado ya existían.<br /><br /> \**StatementText* contiene un **CREATE SCHEMA** instrucción y el nombre del índice especificado ya existían.|  
|42S12|No se encontró el índice|\**StatementText* contiene un **DROP INDEX** instrucción y el nombre del índice especificado no existe.|  
|42S21|Ya existe una columna|\**StatementText* contiene un **ALTER TABLE** instrucción y la columna especificada en el **agregar** cláusula no es única o identifica una columna existente en la tabla base.|  
|42S22|No se encontró la columna|\**StatementText* contiene un **CREATE INDEX** instrucción y uno o varios de la columna de nombres especificados en la lista de columnas no existía.<br /><br /> \**StatementText* contiene un **GRANT** o **REVOCAR** instrucción y un nombre de columna especificado no existe.<br /><br /> \**StatementText* contiene un **seleccione**, **eliminar**, **insertar**, o **actualización** instrucción y un nombre de columna especificado no existía.<br /><br /> \**StatementText* contiene un **CREATE TABLE** no existía instrucción y una columna especificada en una restricción (referencia a una tabla distinta que se va a crear).<br /><br /> \**StatementText* contiene un **CREATE SCHEMA** instrucción y un nombre de columna especificado no existe.|  
|44000|Infracción de WITH CHECK OPTION|El argumento *StatementText* contiene un **insertar** instrucción puede realizadas en una tabla vista o una tabla derivada de la tabla mostrada en la que se creó mediante la especificación de **WITH CHECK OPTION**, de modo que uno o más filas afectadas por la **insertar** instrucción ya no estará presente en la tabla mostrada.<br /><br /> El argumento *StatementText* contiene un **actualización** instrucción puede realizadas en una tabla vista o una tabla derivada de la tabla mostrada en la que se creó mediante la especificación de **WITH CHECK OPTION**, de modo que uno o más filas afectadas por la **actualización** instrucción ya no estará presente en la tabla mostrada.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero nulo|(DM) **StatementText* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLExecDirect** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el argumento *TextLength* era menor o igual a 0, pero no es igual a SQL_NTS.<br /><br /> Establece un valor de parámetro, con **SQLBindParameter**, era un puntero nulo y no es el valor de parámetro de longitud 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Establece un valor de parámetro, con **SQLBindParameter**, no era un puntero nulo; el tipo de datos C era SQL_C_BINARY o SQL_C_CHAR; y el valor de parámetro de longitud era menor que 0 pero no era SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_ PARAM, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valor de longitud del parámetro enlazado por **SQLBindParameter** estaba establecido en SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY, o un tipo de datos específicos del origen de datos long; y la información de SQL_NEED_LONG_DATA_LEN Escriba en **SQLGetInfo** era "S".|  
|HY105|Tipo de parámetro no válido|El valor especificado para el argumento *InputOutputType* en **SQLBindParameter** era SQL_PARAM_OUTPUT y el parámetro era un parámetro de entrada.|  
|HY109|Posición del cursor no válido|\**StatementText* contenida en una posición instrucción update o delete, y se coloca el cursor (por **SQLSetPos** o **SQLFetchScroll**) en una fila que se había eliminada o no se pudo obtener.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y se ha establecido el atributo de instrucción SQL_ATTR_CURSOR_TYPE a un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 La aplicación llama a **SQLExecDirect** para enviar una instrucción SQL al origen de datos. Para obtener más información acerca de la ejecución directa, vea [ejecución directa](../../../odbc/reference/develop-app/direct-execution-odbc.md). El controlador modifica la instrucción para utilizar el formulario de SQL que utiliza el origen de datos y, a continuación, envía al origen de datos. En concreto, el controlador modifica las secuencias de escape que se utiliza para definir ciertas características de SQL. Para obtener la sintaxis de las secuencias de escape, consulte [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
 La aplicación puede incluir uno o más marcadores de parámetros en la instrucción SQL. Para incluir un marcador de parámetro, la aplicación inserta un signo de interrogación (?) en la instrucción SQL en la posición correcta. Para obtener información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Si la instrucción SQL es un **seleccione** instrucción y si la aplicación llama a **SQLSetCursorName** para asociar un cursor con una instrucción, a continuación, el controlador utiliza el cursor especificado. En caso contrario, el controlador genera un nombre de cursor.  
  
 Si el origen de datos está en modo de confirmación manual (Requerir inicio de transacciones explícitas) y ya no se ha iniciado una transacción, el controlador inicia una transacción antes de enviar la instrucción SQL. Para obtener más información, consulte [modo de confirmación Manual](../../../odbc/reference/develop-app/manual-commit-mode.md).  
  
 Si una aplicación utiliza **SQLExecDirect** para enviar un **confirmar** o **reversión** instrucción, no será interoperable entre productos DBMS. Para confirmar o revertir una transacción, una aplicación llama a **SQLEndTran**.  
  
 Si **SQLExecDirect** encuentra un parámetro de datos en ejecución, devuelve SQL_NEED_DATA. La aplicación envía los datos mediante **SQLParamData** y **SQLPutData**. Consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), y [enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Si **SQLExecDirect** ejecuta una actualización por búsqueda, inserción o instrucción delete que no afecta a todas las filas en el origen de datos, la llamada a **SQLExecDirect** devuelve SQL_NO_DATA.  
  
 Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1 y la instrucción SQL contiene al menos un marcador de parámetro, **SQLExecDirect** se ejecutará la instrucción SQL una vez para cada conjunto de valores de parámetro de las matrices que apunta el *ParameterValuePointer* argumento en la llamada a **SQLBindParameter**. Para obtener más información, consulte [matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Si los marcadores están activados y se ejecuta una consulta que no es compatible con marcadores, el controlador debe intentar convertir el entorno a uno que admite marcadores al cambiar un valor de atributo y devolver 01S02 de SQLSTATE SQLSTATE (valor de opción cambiado). Si no se puede cambiar el atributo, el controlador debe devolver SQLSTATE HY024 (valor de atributo no válido).  
  
> [!NOTE]  
>  Cuando se usa la agrupación de conexiones, una aplicación no debe ejecutar instrucciones SQL que cambian la base de datos o en el contexto de la base de datos, como el **USE** *base de datos* instrucción en SQL Server, que cambia el catálogo que se usa un origen de datos.  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), y [programa ODBC de ejemplo](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecutar una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Recopilación de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
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
