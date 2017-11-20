---
title: "Función SQLPrepare | Documentos de Microsoft"
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
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2bdb9a85c14f3636286ea9ca97ea173c9c2b65a4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlprepare-function"></a>Función SQLPrepare
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLPrepare** prepara una cadena SQL para la ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *StatementText*  
 [Entrada] Cadena de texto SQL.  
  
 *TextLength*  
 [Entrada] Longitud de **StatementText* en caracteres.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLPrepare** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLPrepare** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02 DE SQLSTATE|Ha cambiado el valor de opción|Un atributo de instrucción especificada no era válido debido a las condiciones de trabajo de implementación, por lo que un valor similar se sustituye temporalmente. (**SQLGetStmtAttr** puede llamar para determinar cuál es el valor sustituido temporalmente.) El valor de reemplazo es válido para la *StatementHandle* hasta que se cierra el cursor. Los atributos de instrucción que se pueden cambiar son: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|21S01|Lista de valores insertados no coincide con la lista de columnas|\**StatementText* contiene un **insertar** instrucción y el número de valores que se va a insertar no coincidía con el grado de la tabla derivada.|  
|21S02|Grado de la tabla derivada no coincide con la lista de columnas|\**StatementText* contiene un **CREATE VIEW** instrucción y el número de nombres especificado no es el mismo grado que la tabla derivada definido por la especificación de consulta.|  
|22018|Valor de carácter no válido para especificación cast|**StatementText* contenía una instrucción SQL que contenía un literal o un parámetro y el valor no es compatible con el tipo de datos de la columna de tabla asociada.|  
|22019|Carácter de escape no válido|El argumento *StatementText* contiene un **como** predicado con un **ESCAPE** en el **donde** cláusula y la longitud de la conversión siguiente carácter **ESCAPE** no era igual a 1.|  
|22025|Secuencia de escape no válido|El argumento *StatementText* contenidos "**como** *valor de patrón* **ESCAPE** *decarácterdeescape*"en la **donde** cláusula y el carácter que sigue al carácter de escape en el valor de patrón era"%"ni"_".|  
|24000|Estado de cursor no válido|(DM) un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** si se hubiese llamado.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** si no se hubiese llamado.|  
|34000|Nombre de cursor no válido|\**StatementText* contiene una posición **eliminar** o una posición **actualización**, y no se ha abierto el cursor al que hace referencia la instrucción que se está preparada.|  
|3D000|Nombre de catálogo no válido|El nombre de catálogo especificado en *StatementText* no era válido.|  
|3F000|Nombre de esquema no válido|El nombre de esquema especificado en *StatementText* no era válido.|  
|42000|Error de sintaxis, infracción de acceso|\**StatementText* contenía una instrucción SQL que no se puede o contenía un error de sintaxis.<br /><br /> **StatementText* contenía una instrucción para que el usuario no tiene los privilegios necesarios.|  
|42S01|Tabla base o vista ya existe.|\**StatementText* contiene un **CREATE TABLE** o **CREATE VIEW** (instrucción) y el nombre de la tabla o vista nombre especificado ya existe.|  
|42S02|No se encontró la vista o tabla base|\**StatementText* contiene un **DROP TABLE** o un **DROP VIEW** (instrucción) y el nombre de la tabla especificada o la vista nombre no existe.<br /><br /> \**StatementText* contiene un **ALTER TABLE** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **CREATE VIEW** (instrucción) y un nombre de la tabla o vista definida por la especificación de consulta de nombre no existe.<br /><br /> \**StatementText* contiene un **CREATE INDEX** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **GRANT** o **REVOCAR** (instrucción) y el nombre de la tabla especificada o la vista nombre no existe.<br /><br /> \**StatementText* contiene un **seleccione** (instrucción) y un nombre de la tabla especificada o no existe el nombre de la vista.<br /><br /> \**StatementText* contiene un **eliminar**, **insertar**, o **actualización** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **CREATE TABLE** instrucción y una tabla especificada en una restricción (que hacen referencia a una tabla distinta de lo que se va a crear) no existe.|  
|42S11|Ya existe un índice|\**StatementText* contiene un **CREATE INDEX** instrucción y el nombre del índice especificado ya existían.|  
|42S12|No se encontró el índice|\**StatementText* contiene un **DROP INDEX** instrucción y el nombre del índice especificado no existe.|  
|42S21|Ya existe una columna|\**StatementText* contiene un **ALTER TABLE** instrucción y la columna especificada en el **agregar** cláusula no es única o identifica una columna existente en la tabla base.|  
|42S22|No se encontró la columna|\**StatementText* contiene un **CREATE INDEX** (instrucción) y uno o más de la columna de nombres especificados en la lista de columnas no existía.<br /><br /> \**StatementText* contiene un **GRANT** o **REVOCAR** instrucción y un nombre de columna especificado no existe.<br /><br /> \**StatementText* contiene un **seleccione**, **eliminar**, **insertar**, o **actualización** instrucción y una columna especificada nombre no existe.<br /><br /> \**StatementText* contiene un **CREATE TABLE** instrucción y una columna especificada en una restricción (que hacen referencia a una tabla distinta de lo que se va a crear) no existe.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*, y, a continuación, se llama a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero null|(DM) *StatementText* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLPrepare** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el argumento *TextLength* era menor o igual a 0, pero no es igual a SQL_NTS.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|La configuración de simultaneidad no era válida para el tipo de cursor definido.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera expirado antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 La aplicación llama **SQLPrepare** para enviar una instrucción SQL al origen de datos para la preparación. Para obtener más información sobre la ejecución preparada, vea [ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md). La aplicación puede incluir uno o más marcadores de parámetros en la instrucción SQL. Para incluir un marcador de parámetro, la aplicación incrusta un signo de interrogación (?) en la cadena SQL en la posición adecuada. Para obtener información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Si una aplicación usa **SQLPrepare** para preparar y **SQLExecute** para enviar un **confirmar** o **reversión** (instrucción), no será interoperar entre productos DBMS. Para confirmar o revertir una transacción, llame a **SQLEndTran**.  
  
 El controlador puede modificar la instrucción para utilizar el formulario de SQL que utiliza el origen de datos y, a continuación, enviarla al origen de datos para la preparación. En concreto, el controlador modifica las secuencias de escape que se utiliza para definir la sintaxis SQL para determinadas características. (Para obtener una descripción de la gramática de instrucción SQL, vea [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) y [Apéndice C: SQL gramática](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Para el controlador, un identificador de instrucción es similar a un identificador de instrucción de código SQL incrustado. Si el origen de datos admite identificadores de instrucción, el controlador puede enviar un identificador de instrucción y los valores de parámetro para el origen de datos.  
  
 Después de prepara una instrucción, la aplicación utiliza el identificador de instrucción para hacer referencia a la instrucción en posteriores llamadas a funciones. Volver a ejecutar la instrucción preparada asociada al identificador de instrucción mediante una llamada a **SQLExecute** hasta que la aplicación libera la instrucción con una llamada a **SQLFreeStmt** con la opción SQL_DROP o hasta que se usa el identificador de instrucción en una llamada a **SQLPrepare**, **SQLExecDirect**, o una de las funciones de catálogo (**SQLColumns**,  **SQLTables**, y así sucesivamente). Una vez que la aplicación prepara una instrucción, puede solicitar información sobre el formato del conjunto de resultados. Para algunas implementaciones, una llamada a **SQLDescribeCol** o **SQLDescribeParam** después **SQLPrepare** podría no ser tan eficaz como una llamada a la función después de **SQLExecute** o **SQLExecDirect**.  
  
 Algunos controladores no se pueden devolver errores de sintaxis o las infracciones de acceso cuando la aplicación llama **SQLPrepare**. Un controlador puede controlar los errores de sintaxis e infracciones de acceso, solo los errores de sintaxis, o errores de sintaxis ni las infracciones de acceso. Por lo tanto, una aplicación debe ser capaz de tratar estas condiciones al llamar a posteriores relacionadas con funciones como **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**, y **SQLExecute**.  
  
 Dependiendo de las capacidades del controlador y el origen de datos, información de parámetros (por ejemplo, tipos de datos) se puede comprobar cuando se prepara la instrucción (si se han enlazado todos los parámetros) o cuando se ejecuta (si no se han enlazado todos los parámetros). Para obtener una interoperabilidad máxima, una aplicación debe desenlazar todos los parámetros que se aplican a una instrucción SQL anterior antes de preparar una nueva instrucción SQL en la misma instrucción. Esto evita los errores que se deban a la anterior información de parámetros que se aplican a la nueva instrucción.  
  
> [!IMPORTANT]  
>  Confirmar una transacción, ya sea llamando explícitamente a **SQLEndTran** o cuando se trabaja en modo de confirmación automática, puede hacer que el origen de datos eliminar los planes de acceso para todas las instrucciones en una conexión. Para obtener más información, vea los tipos de información SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y [efecto de las transacciones en los cursores y las instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), y [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador de instrucción|[SQLAllocHandle, función](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un búfer con un parámetro|[SQLBindParameter, función](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecutar una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ejecutar una instrucción SQL|[SQLExecDirect, función](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[SQLExecute, función](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Devuelve el número de filas afectadas por una instrucción|[SQLRowCount, función](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Establecer un nombre de cursor|[SQLSetCursorName, función](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

