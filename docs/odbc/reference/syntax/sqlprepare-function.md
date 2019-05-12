---
title: Función SQLPrepare | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c77f8e6bd137b557b150ba91c143abb5438778c8
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536630"
---
# <a name="sqlprepare-function"></a>Función SQLPrepare
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLPrepare** prepara una cadena de SQL para su ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02|Valor de opción cambiado|Un atributo de instrucción especificado no era válido debido a las condiciones de trabajo de implementación, por lo que temporalmente se ha sustituido por un valor similar. (**SQLGetStmtAttr** se puede llamar para determinar cuál es el valor sustituido temporalmente.) El valor de reemplazo es válido para el *StatementHandle* hasta que se cierra el cursor. Los atributos de instrucción que se pueden cambiar son: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|21S01|Lista de valores insertados no coincide con la lista de columnas|\**StatementText* contiene un **insertar** instrucción y el número de valores que se va a insertar no coincidía con el grado de la tabla derivada.|  
|21S02|Grado de la tabla derivada no coincide con la lista de columnas|\**StatementText* contiene un **CREATE VIEW** instrucción y el número de nombres especificado no es el mismo grado que la tabla derivada definido por la especificación de consulta.|  
|22018|Valor de carácter no válido para especificación cast|**StatementText* contenía una instrucción SQL que contenía un literal o un parámetro y el valor no era compatible con el tipo de datos de la columna de tabla asociada.|  
|22019|Carácter de escape no válido|El argumento *StatementText* contiene un **como** predicado con un **ESCAPE** en el **donde** cláusula y la longitud del escape siguiente carácter **ESCAPE** no es igual a 1.|  
|22025|Secuencia de escape no válido|El argumento *StatementText* contenidos "**como** _valor de patrón_ **ESCAPE** _decarácterdeescape_"en el **donde** cláusula y el carácter que sigue el carácter de escape en el valor de patrón no era"%"ni"_".|  
|24000|Estado de cursor no válido|(DM) un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** hubiera llamado.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|34000|Nombre de cursor no válido|\**StatementText* contenida en una posición **eliminar** o una posición **actualización**, y no se ha abierto el cursor al que hace referencia la instrucción que se está preparada.|  
|3D000|Nombre del catálogo no válido|El nombre de catálogo especificado en *StatementText* no era válido.|  
|3F000|Nombre de esquema no válido|El nombre de esquema especificado en *StatementText* no era válido.|  
|42000|Error de sintaxis, infracción de acceso|\**StatementText* contenía una instrucción SQL que no se ha preparable o contenía un error de sintaxis.<br /><br /> **StatementText* contenía una instrucción para que el usuario no tenía los privilegios necesarios.|  
|42S01|Tabla o vista base ya existe.|\**StatementText* contiene un **CREATE TABLE** o **CREATE VIEW** instrucción y el nombre de la tabla o vista de nombre especificado ya existe.|  
|42S02|No se encuentra la vista o tabla base|\**StatementText* contiene un **DROP TABLE** o un **DROP VIEW** instrucción y el nombre de la tabla especificada o vista de nombre no existe.<br /><br /> \**StatementText* contiene un **ALTER TABLE** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **CREATE VIEW** instrucción y un nombre de la tabla o vista no existía nombre definido por la especificación de consulta.<br /><br /> \**StatementText* contiene un **CREATE INDEX** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **GRANT** o **REVOCAR** instrucción y el nombre de la tabla especificada o vista de nombre no existe.<br /><br /> \**StatementText* contiene un **seleccione** instrucción y un nombre de tabla especificado o la vista de nombre no existe.<br /><br /> \**StatementText* contiene un **eliminar**, **insertar**, o **actualización** instrucción y el nombre de tabla especificado no existe.<br /><br /> \**StatementText* contiene un **CREATE TABLE** no existía instrucción y una tabla especificada en una restricción (referencia a una tabla distinta que se va a crear).|  
|42S11|El índice ya existe|\**StatementText* contiene un **CREATE INDEX** instrucción y el nombre del índice especificado ya existían.|  
|42S12|No se encontró el índice|\**StatementText* contiene un **DROP INDEX** instrucción y el nombre del índice especificado no existe.|  
|42S21|Ya existe una columna|\**StatementText* contiene un **ALTER TABLE** instrucción y la columna especificada en el **agregar** cláusula no es única o identifica una columna existente en la tabla base.|  
|42S22|No se encontró la columna|\**StatementText* contiene un **CREATE INDEX** instrucción y uno o varios de la columna de nombres especificados en la lista de columnas no existía.<br /><br /> \**StatementText* contiene un **GRANT** o **REVOCAR** instrucción y un nombre de columna especificado no existe.<br /><br /> \**StatementText* contiene un **seleccione**, **eliminar**, **insertar**, o **actualización** instrucción y un nombre de columna especificado no existía.<br /><br /> \**StatementText* contiene un **CREATE TABLE** no existía instrucción y una columna especificada en una restricción (referencia a una tabla distinta que se va a crear).|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*, y, a continuación, se llamó a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero nulo|(DM) *StatementText* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLPrepare** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el argumento *TextLength* era menor o igual a 0, pero no es igual a SQL_NTS.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|La configuración de simultaneidad no era válida para el tipo de cursor definido.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y se ha establecido el atributo de instrucción SQL_ATTR_CURSOR_TYPE a un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 La aplicación llama a **SQLPrepare** para enviar una instrucción SQL al origen de datos para la preparación. Para obtener más información sobre la ejecución preparada, vea [ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md). La aplicación puede incluir uno o más marcadores de parámetros en la instrucción SQL. Para incluir un marcador de parámetro, la aplicación inserta un signo de interrogación (?) en la cadena SQL en la posición adecuada. Para obtener información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Si una aplicación utiliza **SQLPrepare** para preparar y **SQLExecute** para enviar un **confirmar** o **reversión** instrucción, no será interoperar entre productos DBMS. Para confirmar o revertir una transacción, llamar a **SQLEndTran**.  
  
 El controlador puede modificar la instrucción para utilizar el formulario de SQL que utiliza el origen de datos y, a continuación, enviarla al origen de datos para la preparación. En concreto, el controlador modifica las secuencias de escape que se usan para definir la sintaxis SQL para determinadas características. (Para obtener una descripción de gramática de instrucción SQL, consulte [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) y [Apéndice C: Gramática de SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Para el controlador, un identificador de instrucción es similar a un identificador de instrucción de código SQL incrustado. Si el origen de datos es compatible con los identificadores de instrucción, el controlador puede enviar un identificador de instrucción y los valores de parámetro para el origen de datos.  
  
 Después de prepara una instrucción, la aplicación utiliza el identificador de instrucción para hacer referencia a la instrucción en posteriores llamadas de función. La instrucción preparada asociada con el identificador de instrucción puede volver a ejecutar mediante una llamada a **SQLExecute** hasta que la aplicación libera la instrucción con una llamada a **SQLFreeStmt** con la opción SQL_DROP o hasta que se usa el identificador de instrucción en una llamada a **SQLPrepare**, **SQLExecDirect**, o una de las funciones de catálogo (**SQLColumns**,  **SQLTables**, y así sucesivamente). Una vez que la aplicación prepara una instrucción, puede solicitar información sobre el formato del conjunto de resultados. Para algunas implementaciones, una llamada a **SQLDescribeCol** o **SQLDescribeParam** después **SQLPrepare** podría no ser tan eficaz como una llamada a la función después de **SQLExecute** o **SQLExecDirect**.  
  
 Algunos controladores no se pueden devolver errores de sintaxis o las infracciones de acceso cuando la aplicación llama **SQLPrepare**. Un controlador puede controlar los errores de sintaxis e infracciones de acceso, solo los errores de sintaxis, o errores de sintaxis ni las infracciones de acceso. Por lo tanto, una aplicación debe ser capaz de tratar estas situaciones, cuando una llamada subsiguiente como funciones relacionadas **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**, y **SQLExecute**.  
  
 Según las capacidades del controlador y el origen de datos, información de parámetros (por ejemplo, los tipos de datos) podría estar protegido cuando se prepara la instrucción (si se han enlazado todos los parámetros) o cuando se ejecuta (si no se han enlazado todos los parámetros). Para obtener la máxima interoperatividad, una aplicación debe desenlazar todos los parámetros que se aplican a una instrucción SQL anterior antes de preparar una nueva instrucción SQL en la misma instrucción. Esto evita los errores producidos por la antigua información de parámetros que se va a aplicar a la instrucción nuevo.  
  
> [!IMPORTANT]  
>  Confirmar una transacción, ya sea llamando explícitamente **SQLEndTran** o al trabajar en modo de confirmación automática, puede hacer que el origen de datos eliminar los planes de acceso para todas las instrucciones en una conexión. Para obtener más información, vea los tipos de información SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y [efecto de las transacciones en los cursores y las instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), y [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador de instrucción|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un búfer con un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecutar una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Devuelve el número de filas afectadas por una instrucción|[Función SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
