---
title: "SQLExecDirect, función | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fdf6183eda2b66263a8ff27664d046640b94ea95
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlexecdirect-function"></a>SQLExecDirect, función
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLExecDirect** ejecuta una instrucción puede, mediante los valores actuales de las variables de marcador de parámetro, si existe algún parámetro en la instrucción. **SQLExecDirect** es la forma más rápida para enviar una instrucción SQL para ejecutar una sola vez.  
  
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
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01001|Conflicto de operación de cursor|\**StatementText* independiente una posición instrucción update o delete, y no hay filas o más de una fila se actualiza o elimina. (Para obtener más información sobre las actualizaciones en más de una fila, vea la descripción de la SQL_ATTR_SIMULATE_CURSOR *atributo* en **SQLSetStmtAttr**.)<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01003|Valor NULL eliminado en la función Set.|El argumento *StatementText* contiene una función set (como **AVG**, **MAX**, **MIN**, y así sucesivamente), pero no el **recuento**  establece la función y el argumento es NULL se eliminaron los valores antes de que se aplique la función. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|Datos de cadena o binarios devuelven para una entrada/salida o parámetro de salida que se produjo el truncamiento de carácter que no esté vacía o datos binarios no NULL. Si ha realizado un valor de cadena, era truncado a la derecha. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01006|Privilegio no revocado|\**StatementText* contiene un **REVOCAR** instrucción y el usuario no tenía el privilegio especificado. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01007|No se ha concedido el privilegio|*\*StatementText* era una **GRANT** instrucción y el usuario no se pudieron conceder el privilegio especificado.|  
|01S02 DE SQLSTATE|Ha cambiado el valor de opción|Un atributo de instrucción especificada no era válido debido a las condiciones de trabajo de implementación, por lo que un valor similar se sustituye temporalmente. (**SQLGetStmtAttr** puede llamar para determinar cuál es el valor sustituido temporalmente.) El valor de reemplazo es válido para la *StatementHandle* hasta que se cierra el cursor, momento en que el atributo de instrucción revierte a su valor anterior. Los atributos de instrucción que se pueden cambiar son:<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S07|Truncamiento fraccionario|Los datos devuelvan para una entrada/salida o parámetro de salida se truncaron tal que se trunca la parte fraccionaria de un tipo de datos numéricos o se trunca la parte fraccionaria del componente de un tipo de datos de hora, una marca de tiempo o intervalo de tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07002|Campo COUNT incorrecto|El número de parámetros especificados en **SQLBindParameter** era menor que el número de parámetros en la instrucción SQL contenidos en \* *StatementText*.<br /><br /> **SQLBindParameter** se llamó con *ParameterValuePtr* establecido en un puntero nulo, *StrLen_or_IndPtr* no establecido en SQL_NULL_DATA o SQL_DATA_AT_EXEC, y  *InputOutputType* no se establece en SQL_PARAM_OUTPUT, para que el número de parámetros especificado en **SQLBindParameter** era mayor que el número de parámetros en la instrucción SQL contenidos en **StatementText*.|  
|07006|Infracción del atributo de tipo de datos restringido|El valor de datos identificado por la *ValueType* argumento en **SQLBindParameter** para los parámetros enlazados no se pudieron convertir al tipo de datos identificado por la *ParameterType*argumento en **SQLBindParameter**.<br /><br /> Devuelve el valor de datos para un parámetro de enlazado como SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT no se pudo convertir al tipo de datos identificado por la *ValueType* argumento en **SQLBindParameter**.<br /><br /> (Si no se pudieron convertir los valores de datos para una o varias filas, pero una o más filas se devolvieron correctamente, esta función devuelve SQL_SUCCESS_WITH_INFO).|  
|07007|Infracción de valor de parámetro restringido|El tipo de parámetro SQL_PARAM_INPUT_OUTPUT_STREAM sólo se utiliza para un parámetro que envía y recibe datos en partes. Un búfer de entrada enlazado no está permitido para este tipo de parámetro.<br /><br /> Este error se produce cuando el tipo de parámetro es SQL_PARAM_INPUT_OUTPUT y cuando la \* *StrLen_or_IndPtr* especificado en **SQLBindParameter** no es igual a SQL_NULL_DATA, SQL_DEFAULT_ PARAM, SQL_LEN_DATA_AT_EXEC(len) o SQL_DATA_AT_EXEC.|  
|07S01|Uso no válido de parámetro predeterminado|Establece un valor de parámetro, con **SQLBindParameter**, era SQL_DEFAULT_PARAM y el parámetro correspondiente no tenía un valor predeterminado.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|21S01|Lista de valores insertados no coincide con la lista de columnas|\**StatementText* contiene un **insertar** instrucción y el número de valores que se va a insertar no coincidía con el grado de la tabla derivada.|  
|21S02|Grado de la tabla derivada no coincide con la lista de columnas|\**StatementText* contiene un **CREATE VIEW** instrucción y la lista de columnas no calificado (el número de columnas especificadas para la vista en la *identificador de la columna* argumentos de la instrucción SQL instrucción) contiene nombres más que el número de columnas de la tabla derivada definida por el *especificación de consulta* argumento de la instrucción SQL.|  
|22001|Datos de cadena truncados por la derecha|La asignación de un carácter o un valor binario a una columna generó el truncamiento de los datos de caracteres que no esté vacía o datos binarios no null.|  
|22002|Variable de indicador necesaria, pero no se ha suministrado|Se ha enlazado a datos NULL para un parámetro de salida cuyo *StrLen_or_IndPtr* establecido por **SQLBindParameter** era un puntero nulo.|  
|22003|Valor numérico fuera del intervalo|**StatementText* contenía una instrucción SQL que contiene un parámetro numérico enlazado o un literal de y el valor ocasiona la parte entera (en lugar de fracciones) del número se trunque cuando se asigna a la columna de tabla asociada.<br /><br /> Devuelve un valor numérico (como numérico o cadena) para uno o más parámetros de entrada/salida o de salida habría provocado la parte entera (en lugar de fracciones) del número se trunque.|  
|22007|Formato de datetime no válido|**StatementText* contenía una instrucción SQL que contiene una fecha, hora o estructura de marca de tiempo como un parámetro de enlace y el parámetro era, respectivamente, una fecha no válida, una hora o una marca de tiempo.<br /><br /> Un parámetro de entrada/salida o de salida se enlazó a una fecha, hora o estructura de marca de tiempo C, y un valor en el parámetro devuelto era, respectivamente, una fecha no válida, una hora o una marca de tiempo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22008|Desbordamiento del campo de fecha y hora|**StatementText* independiente de una instrucción SQL que contiene una expresión de fecha y hora que, cuando calcula, dan como resultado una fecha, hora o marca de tiempo de la estructura que no era válida.<br /><br /> Calcula una expresión de fecha y hora para una entrada/salida o parámetro de salida que se produjo en una fecha, la hora o la estructura de C de la marca de tiempo que no era válido.|  
|22012|División por cero|**StatementText* contenía una instrucción SQL que contiene una expresión aritmética que ha provocado la división por cero.<br /><br /> Una expresión aritmética calculado para una entrada/salida o parámetro de salida dio como resultado de división por cero.|  
|22015|Desbordamiento del campo de intervalo|*\*StatementText* contiene un parámetro numérico o intervalo exacto que, cuando se convierte a un tipo de datos SQL de intervalo, causó una pérdida de dígitos significativos.<br /><br /> *\*StatementText* contiene un parámetro de intervalo con más de un campo que, cuando se convierte a un tipo de datos numéricos en una columna, no tenía ninguna representación en el tipo de datos numérico.<br /><br /> *\*StatementText* contenía datos de parámetro que se asignan a un tipo SQL de intervalo y no había ninguna representación del valor del tipo de C en el intervalo de tipo SQL.<br /><br /> Asignación de un parámetro de entrada/salida o de salida que era un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causado una pérdida de dígitos significativos.<br /><br /> Cuando un parámetro de entrada/salida o de salida se asigna a una estructura de intervalo C, no había ninguna representación de los datos de la estructura de datos de intervalo.|  
|22018|Valor de carácter no válido para especificación cast|*\*StatementText* incluidos en un tipo de C que era una numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos character; y el valor de la columna no es un literal válido del tipo de C enlazado.<br /><br /> Cuando se devuelve un parámetro de entrada/salida o de salida, el tipo SQL era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo de C era SQL_C_CHAR; y el valor de la columna no es un literal válido del tipo SQL enlazado.|  
|22019|Carácter de escape no válido|\**StatementText* contenía una instrucción SQL que contenía una **como** predicado con un **ESCAPE** en el **donde** cláusula y la longitud de la conversión siguiente carácter **ESCAPE** no era igual a 1.|  
|22025|Secuencia de escape no válido|\**StatementText* contenía una instrucción SQL que contiene "**como** *valor de patrón* **ESCAPE** *decarácterdeescape*"en la **donde** cláusula y el carácter que sigue al carácter de escape en el valor de patrón no era uno de"%"o"_".|  
|23000|Infracción de restricción de integridad|**StatementText* contenía una instrucción SQL que contiene un parámetro o un literal. El valor del parámetro era nulo para una columna definida como NOT NULL en la columna de tabla asociada, se proporcionó un valor duplicado para una columna restringida para que contenga solamente valores únicos o se ha infringido alguna otra restricción de integridad.|  
|24000|Estado de cursor no válido|Un cursor se coloca en el *StatementHandle* por **SQLFetch** o **SQLFetchScroll**. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y se devuelve el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto pero no está colocado en el *StatementHandle*.<br /><br /> **StatementText* independiente una posición instrucción update o delete, y el cursor se coloca antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|34000|Nombre de cursor no válido|**StatementText* independiente una posición instrucción update o delete y no abrió el cursor al que hace referencia la instrucción que se está ejecutando.|  
|3D000|Nombre de catálogo no válido|El nombre de catálogo especificado en *StatementText* no era válido.|  
|3F000|Nombre de esquema no válido|El nombre de esquema especificado en *StatementText* no era válido.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis, infracción de acceso|\**StatementText* contenía una instrucción SQL que no se puede o contenía un error de sintaxis.<br /><br /> El usuario no tiene permiso para ejecutar la instrucción SQL contenida en **StatementText*.|  
|42S01|Tabla base o vista ya existe.|\**StatementText* contiene un **CREATE TABLE** o **CREATE VIEW** (instrucción) y el nombre de la tabla o vista nombre especificado ya existe.|  
|42S02|No se encontró la vista o tabla base|\**StatementText* contiene un **DROP TABLE** o un **DROP VIEW** (instrucción) y el nombre de la tabla especificada o la vista nombre no existe.<br /><br /> \**StatementText* contiene un **ALTER TABLE** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **CREATE VIEW** (instrucción) y un nombre de la tabla o vista definida por la especificación de consulta de nombre no existe.<br /><br /> \**StatementText* contiene un **CREATE INDEX** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **GRANT** o **REVOCAR** (instrucción) y el nombre de la tabla especificada o la vista nombre no existe.<br /><br /> \**StatementText* contiene un **seleccione** (instrucción) y un nombre de la tabla especificada o no existe el nombre de la vista.<br /><br /> \**StatementText* contiene un **eliminar**, **insertar**, o **actualización** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **CREATE TABLE** instrucción y una tabla especificada en una restricción (que hacen referencia a una tabla distinta de lo que se va a crear) no existe.<br /><br /> \**StatementText* contiene un **CREATE SCHEMA** (instrucción) y un nombre de la tabla especificada o no existe el nombre de la vista.|  
|42S11|Ya existe un índice|\**StatementText* contiene un **CREATE INDEX** instrucción y el nombre del índice especificado ya existían.<br /><br /> \**StatementText* contiene un **CREATE SCHEMA** instrucción y el nombre del índice especificado ya existían.|  
|42S12|No se encontró el índice|\**StatementText* contiene un **DROP INDEX** instrucción y el nombre del índice especificado no existe.|  
|42S21|Ya existe una columna|\**StatementText* contiene un **ALTER TABLE** instrucción y la columna especificada en el **agregar** cláusula no es única o identifica una columna existente en la tabla base.|  
|42S22|No se encontró la columna|\**StatementText* contiene un **CREATE INDEX** (instrucción) y uno o más de la columna de nombres especificados en la lista de columnas no existía.<br /><br /> \**StatementText* contiene un **GRANT** o **REVOCAR** instrucción y un nombre de columna especificado no existe.<br /><br /> \**StatementText* contiene un **seleccione**, **eliminar**, **insertar**, o **actualización** instrucción y una columna especificada nombre no existe.<br /><br /> \**StatementText* contiene un **CREATE TABLE** instrucción y una columna especificada en una restricción (que hacen referencia a una tabla distinta de lo que se va a crear) no existe.<br /><br /> \**StatementText* contiene un **CREATE SCHEMA** instrucción y un nombre de columna especificado no existe.|  
|44000|Infracción de WITH CHECK OPTION|El argumento *StatementText* contiene un **insertar** instrucción realizadas en una tabla vista o una tabla que se deriva de la tabla mostrada que se creó mediante la especificación de **WITH CHECK OPTION**, de forma que uno o más filas afectadas por la **insertar** instrucción ya no estará presente en la tabla mostrada.<br /><br /> El argumento *StatementText* contiene un **actualización** instrucción realizadas en una tabla vista o una tabla que se deriva de la tabla mostrada que se creó mediante la especificación de **WITH CHECK OPTION**, de forma que uno o más filas afectadas por la **actualización** instrucción ya no estará presente en la tabla mostrada.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*. A continuación, se llama a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero null|(DM) **StatementText* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLExecDirect** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el argumento *TextLength* era menor o igual a 0, pero no es igual a SQL_NTS.<br /><br /> Establece un valor de parámetro, con **SQLBindParameter**, era un puntero nulo, y el valor de longitud del parámetro no es 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Establece un valor de parámetro, con **SQLBindParameter**, no era un puntero nulo; el tipo de datos de C era SQL_C_BINARY o SQL_C_CHAR; y el valor de longitud del parámetro era menor que 0 pero no SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_ PARAM, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Enlaza un valor de longitud del parámetro **SQLBindParameter** era establecido en SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY, o un tipo de datos específicos del origen de datos largos; y la información de SQL_NEED_LONG_DATA_LEN Escriba en **SQLGetInfo** era "Y".|  
|HY105|Tipo de parámetro no válido|El valor especificado para el argumento *InputOutputType* en **SQLBindParameter** era SQL_PARAM_OUTPUT y el parámetro era un parámetro de entrada.|  
|HY109|Posición del cursor no válido|\**StatementText* independiente una posición instrucción update o delete, y se coloca el cursor (por **SQLSetPos** o **SQLFetchScroll**) en una fila que se eliminó o no se puede capturar.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta finalizó antes de que el origen de datos devuelve el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 La aplicación llama **SQLExecDirect** para enviar una instrucción SQL al origen de datos. Para obtener más información acerca de la ejecución directa, vea [la ejecución directa](../../../odbc/reference/develop-app/direct-execution-odbc.md). El controlador modifica la instrucción para utilizar el formulario de SQL que utiliza el origen de datos y, a continuación, envía al origen de datos. En concreto, el controlador modifica las secuencias de escape que se utiliza para definir ciertas características de SQL. Para obtener la sintaxis de las secuencias de escape, vea [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
 La aplicación puede incluir uno o más marcadores de parámetros en la instrucción SQL. Para incluir un marcador de parámetro, la aplicación incrusta un signo de interrogación (?) en la instrucción SQL en la posición adecuada. Para obtener información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Si la instrucción SQL es un **seleccione** instrucción y si la aplicación llamó a **SQLSetCursorName** para asociar un cursor con una instrucción, a continuación, el controlador utiliza el cursor especificado. En caso contrario, el controlador genera un nombre de cursor.  
  
 Si el origen de datos está en modo de confirmación manual (lo que requiere la iniciación de transacción explícita) y ya no se ha iniciado una transacción, el controlador inicia una transacción antes de enviar la instrucción SQL. Para obtener más información, consulte [modo de confirmación Manual](../../../odbc/reference/develop-app/manual-commit-mode.md).  
  
 Si una aplicación usa **SQLExecDirect** para enviar un **confirmar** o **reversión** (instrucción), no se puede interoperar entre productos DBMS. Para confirmar o revertir una transacción, una aplicación llama **SQLEndTran**.  
  
 Si **SQLExecDirect** encuentra un parámetro de datos en ejecución, devuelve SQL_NEED_DATA. La aplicación envía los datos mediante **SQLParamData** y **SQLPutData**. Vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), y [enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Si **SQLExecDirect** ejecuta una actualización por búsqueda, inserción o una instrucción delete que no afecta a las filas del origen de datos, la llamada a **SQLExecDirect** devuelve SQL_NO_DATA.  
  
 Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1 y la instrucción SQL contiene al menos un marcador de parámetro, **SQLExecDirect** se ejecutará la instrucción SQL una vez para cada conjunto de valores de parámetro las matrices que señala el *ParameterValuePointer* argumento en la llamada a **SQLBindParameter**. Para obtener más información, consulte [matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Si los marcadores están activados y se ejecuta una consulta que no es compatible con marcadores, el controlador debería intentar convertir el entorno a uno que admite marcadores cambiando un valor de atributo y devolver 01S02 SQLSTATE (valor de opción cambiado). Si no se puede cambiar el atributo, el controlador debería devolver SQLSTATE HY024 (valor de atributo no válido).  
  
> [!NOTE]  
>  Cuando se usa la agrupación de conexiones, una aplicación no debe ejecutar instrucciones SQL que cambian la base de datos o en el contexto de la base de datos, como el **USE** *base de datos* instrucción en SQL Server, que cambia el catálogo utilizado por un origen de datos.  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), y [ODBC programa de ejemplo](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecutar una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ejecutar una instrucción SQL preparada|[SQLExecute, función](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Recopilación de varias filas de datos|[SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver un nombre de cursor|[Función SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Capturar parte o la totalidad de una columna de datos|[SQLGetData, función](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Devuelve el siguiente parámetro para enviar datos|[SQLParamData, función](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Preparar una instrucción de ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[SQLPutData, función](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Establecer un nombre de cursor|[SQLSetCursorName, función](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|Establecer un atributo de instrucción|[SQLSetStmtAttr, función](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

