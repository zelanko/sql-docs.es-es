---
title: Función SQLPrepare (SQLPrepare) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9aedd665df2a943627207902d592d597c503c63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306886"
---
# <a name="sqlprepare-function"></a>Función SQLPrepare
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLPrepare** prepara una cadena SQL para la ejecución.  
  
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
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLPrepare** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLPrepare** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opción cambiado|Un atributo de instrucción especificado no era válido debido a las condiciones de trabajo de implementación, por lo que se sustituyó temporalmente un valor similar. (**SQLGetStmtAttr** se puede llamar para determinar cuál es el valor sustituido temporalmente.) El valor sustituto es válido para el *StatementHandle* hasta que se cierra el cursor. Los atributos de instrucción que se pueden cambiar son: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|21S01|Insertar lista de valores no coincide con la lista de columnas|\**StatementText* contenía una instrucción **INSERT** y el número de valores que se insertarán no coincidía con el grado de la tabla derivada.|  
|21S02|El grado de la tabla derivada no coincide con la lista de columnas|\**StatementText* contenía una instrucción **CREATE VIEW** y el número de nombres especificado no es el mismo grado que la tabla derivada definida por la especificación de consulta.|  
|22018|Valor de carácter no válido para la especificación de conversión|**StatementText* contenía una instrucción SQL que contenía un literal o parámetro y el valor era incompatible con el tipo de datos de la columna de tabla asociada.|  
|22019|Carácter de escape no válido|El argumento *StatementText* contenía un predicado **LIKE** con un **ESCAPE** en la cláusula **WHERE,** y la longitud del carácter de escape que sigue a **ESCAPE** no era igual a 1.|  
|22025|Secuencia de escape no válida|El argumento *StatementText* contenía "**LIKE** _pattern value_ **ESCAPE** _escape character_" en la cláusula **WHERE,** y el carácter que sigue al carácter de escape en el valor del patrón no era "%" ni "_".|  
|24000|Estado de cursor no válido|(DM) un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** se había llamado.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|34000|Nombre de cursor no válido|\**StatementText* contenía un **DELETE** posicionado o un **UPDATE**posicionado , y el cursor al que hace referencia la instrucción que se está preparando no estaba abierto.|  
|3D000|Nombre de catálogo no válido|El nombre del catálogo especificado en *StatementText* no era válido.|  
|3F000|Nombre de esquema no válido|El nombre de esquema especificado en *StatementText* no era válido.|  
|42000|Error de sintaxis o violación de acceso|\**StatementText* contenía una instrucción SQL que no se puede preparar o contiene un error de sintaxis.<br /><br /> **StatementText* contenía una instrucción para la que el usuario no tenía los privilegios necesarios.|  
|42S01|La tabla base o la vista ya existen|\**StatementText* contenía una instrucción **CREATE TABLE** o **CREATE VIEW,** y el nombre de tabla o el nombre de vista especificado ya existe.|  
|42S02|Tabla base o vista no encontrada|\**StatementText* contenía una **instrucción DROP TABLE** o **DROP VIEW,** y el nombre de tabla o el nombre de vista especificados no existían.<br /><br /> \**StatementText* contenía una instrucción **ALTER TABLE** y el nombre de tabla especificado no existía.<br /><br /> \**StatementText* contenía una instrucción **CREATE VIEW** y no existía un nombre de tabla o un nombre de vista definido por la especificación de consulta.<br /><br /> \**StatementText* contenía una instrucción **CREATE INDEX** y el nombre de tabla especificado no existía.<br /><br /> \**StatementText* contenía una instrucción **GRANT** o **REVOKE** y el nombre de tabla o el nombre de vista especificados no existían.<br /><br /> \**StatementText* contenía una instrucción **SELECT** y no existía un nombre de tabla o un nombre de vista especificado.<br /><br /> \**StatementText* contenía una instrucción **DELETE**, **INSERT**o **UPDATE** y el nombre de tabla especificado no existía.<br /><br /> \**StatementText* contenía una instrucción **CREATE TABLE** y no existía una tabla especificada en una restricción (que hacía referencia a una tabla distinta de la que se está creando).|  
|42S11|El índice ya existe|\**StatementText* contenía una instrucción **CREATE INDEX** y el nombre de índice especificado ya existía.|  
|42S12|Indice no encontrado|\**StatementText* contenía una instrucción **DROP INDEX** y el nombre de índice especificado no existía.|  
|42S21|Columna ya existe|\**StatementText* contenía una instrucción **ALTER TABLE** y la columna especificada en la cláusula **ADD** no es única o identifica una columna existente en la tabla base.|  
|42S22|Columna no encontrada|\**StatementText* contenía una instrucción **CREATE INDEX** y uno o varios de los nombres de columna especificados en la lista de columnas no existían.<br /><br /> \**StatementText* contenía una instrucción **GRANT** o **REVOKE** y no existía un nombre de columna especificado.<br /><br /> \**StatementText* contenía una instrucción **SELECT**, **DELETE**, **INSERT**o **UPDATE** y no existía un nombre de columna especificado.<br /><br /> \**StatementText* contenía una instrucción **CREATE TABLE** y no existía una columna especificada en una restricción (que hacía referencia a una tabla distinta de la que se está creando).|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*, y, a continuación, se llamó a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|(DM) *StatementText* era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLPrepare.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El argumento *TextLength* era menor o igual que 0 pero no igual a SQL_NTS.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|La configuración de simultaneidad no era válida para el tipo de cursor definido.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 La aplicación llama a **SQLPrepare** para enviar una instrucción SQL al origen de datos para su preparación. Para obtener más información acerca de la ejecución preparada, vea [Ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md). La aplicación puede incluir uno o varios marcadores de parámetro en la instrucción SQL. Para incluir un marcador de parámetro, la aplicación incrusta un signo de interrogación (?) en la cadena SQL en la posición adecuada. Para obtener información sobre los parámetros, consulte [Parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Si una aplicación utiliza **SQLPrepare** para preparar y **SQLExecute** para enviar una instrucción **COMMIT** o **ROLLBACK,** no será interoperable entre los productos DBMS. Para confirmar o revertir una transacción, llame a **SQLEndTran**.  
  
 El controlador puede modificar la instrucción para usar la forma de SQL utilizada por el origen de datos y, a continuación, enviarla al origen de datos para su preparación. En particular, el controlador modifica las secuencias de escape utilizadas para definir la sintaxis SQL para ciertas características. (Para obtener una descripción de la gramática de instrucciones SQL, vea [Secuencias](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) de escape en ODBC y [Apéndice C: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Para el controlador, un identificador de instrucción es similar a un identificador de instrucción en código SQL incrustado. Si el origen de datos admite identificadores de instrucción, el controlador puede enviar un identificador de instrucción y valores de parámetro al origen de datos.  
  
 Después de preparar una instrucción, la aplicación utiliza el identificador de instrucción para hacer referencia a la instrucción en llamadas de función posteriores. La instrucción preparada asociada con el identificador de instrucción se puede volver a ejecutar llamando a **SQLExecute** hasta que la aplicación libere la instrucción con una llamada a **SQLFreeStmt** con la opción SQL_DROP o hasta que se use el identificador de instrucción en una llamada a **SQLPrepare**, **SQLExecDirect**o una de las funciones de catálogo (**SQLColumns**, **SQLTables**, etc.). Una vez que la aplicación prepara una instrucción, puede solicitar información sobre el formato del conjunto de resultados. Para algunas implementaciones, llamar a **SQLDescribeCol** o **SQLDescribeParam** después de **SQLPrepare** podría no ser tan eficaz como llamar a la función después de **SQLExecute** o **SQLExecDirect**.  
  
 Algunos controladores no pueden devolver errores de sintaxis ni infracciones de acceso cuando la aplicación llama a **SQLPrepare**. Un controlador puede controlar errores de sintaxis y infracciones de acceso, solo errores de sintaxis o ni errores de sintaxis ni infracciones de acceso. Por lo tanto, una aplicación debe ser capaz de controlar estas condiciones al llamar a funciones relacionadas posteriores como **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**y **SQLExecute**.  
  
 Dependiendo de las capacidades del controlador y el origen de datos, la información de parámetros (como los tipos de datos) se puede comprobar cuando se prepara la instrucción (si se han enlazado todos los parámetros) o cuando se ejecuta (si no se han enlazado todos los parámetros). Para obtener la máxima interoperabilidad, una aplicación debe desenlazar todos los parámetros que se aplicaron a una instrucción SQL antigua antes de preparar una nueva instrucción SQL en la misma instrucción. Esto evita errores que se deben a la información de parámetros antiguos que se aplica a la nueva instrucción.  
  
> [!IMPORTANT]  
>  Confirmar una transacción, ya sea llamando explícitamente a **SQLEndTran** o trabajando en modo de confirmación automática, puede hacer que el origen de datos elimine los planes de acceso para todas las instrucciones de una conexión. Para obtener más información, vea los tipos de información SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y [Efecto de las transacciones en cursores e instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)y [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un identificador de instrucción|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un búfer a un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecución de una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Devolver el número de filas afectadas por una instrucción|[Función SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
