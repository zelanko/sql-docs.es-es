---
title: Función SQLProcedureColumns (SQLProcedureColumns) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d81e44b116ed6f26319d31430999a61a8a17f21
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306856"
---
# <a name="sqlprocedurecolumns-function"></a>Función SQLProcedureColumns
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: ODBC  
  
 **Resumen**  
 **SQLProcedureColumns** devuelve la lista de parámetros de entrada y salida, así como las columnas que componen el conjunto de resultados para los procedimientos especificados. El controlador devuelve la información como un conjunto de resultados en la instrucción especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *CatalogName*  
 [Entrada] Nombre del catálogo de procedimientos. Si un controlador admite catálogos para algunos procedimientos pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica los procedimientos que no tienen catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadenas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente, y su caso es significativo. Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de esquema de procedimiento. Si un controlador admite esquemas para algunos procedimientos pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica los procedimientos que no tienen esquemas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *ProcName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de procedimiento.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *ProcName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *ProcName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **ProcName*.  
  
 *ColumnName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de columna.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *ColumnName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *ColumnName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength4*  
 [Entrada] Longitud en caracteres de **ColumnName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLProcedureColumns** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLProcedureColumns** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** se había llamado. El Administrador de controladores devuelve este error si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y lo devuelve el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLError** en el * \** búfer MessageText describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y el SQL_CATALOG_NAME *InfoType* devuelve que se admiten los nombres de catálogo.<br /><br /> (DM) el atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE y el argumento *SchemaName*, *ProcName*o *ColumnName* era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función aynschronous todavía se estaba ejecutando cuando se llamó a la función SQLProcedureColumns .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El valor de uno de los argumentos de longitud de nombre era menor que 0 pero no igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud de nombre superó el valor de longitud máxima para el nombre de catálogo, esquema, procedimiento o columna correspondiente.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo de procedimientos y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema de procedimiento y el controlador o el origen de datos no admite esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el esquema de procedimiento, el nombre del procedimiento o el nombre de columna, y el origen de datos no admite patrones de búsqueda para uno o varios de esos argumentos.<br /><br /> El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Esta función se utiliza normalmente antes de la ejecución de instrucciones para recuperar información sobre los parámetros de procedimiento y las columnas que componen el conjunto de resultados o conjuntos devueltos por el procedimiento, si existe. Para más información, vea [Procedimientos en Visual Basic](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  **SQLProcedureColumns** podría no devolver todas las columnas utilizadas por un procedimiento. Por ejemplo, un controlador puede devolver solo información sobre los parámetros utilizados por un procedimiento y no sobre las columnas de un conjunto de resultados que genera.  
  
 Los argumentos *SchemaName*, *ProcName*y *ColumnName* aceptan patrones de búsqueda. Para obtener más información acerca de los patrones de búsqueda válidos, vea Argumentos de valor de [patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de las funciones de catálogo ODBC, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
 **SQLProcedureColumns** devuelve los resultados como un conjunto de resultados estándar, ordenados por PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME y COLUMN_TYPE. Los nombres de columna se devuelven para cada procedimiento en el siguiente orden: el nombre del valor devuelto, los nombres de cada parámetro en la invocación del procedimiento (en orden de llamada) y, a continuación, los nombres de cada columna del conjunto de resultados devuelto por el procedimiento (en orden de columna).  
  
 Las aplicaciones deben enlazar columnas específicas del controlador en relación con el final del conjunto de resultados. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
 Para determinar las longitudes reales de las columnas PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME y COLUMN_NAME, una aplicación puede llamar a **SQLGetInfo** con las opciones SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_PROCEDURE_NAME_LEN y SQL_MAX_COLUMN_NAME_LEN.  
  
 Se ha cambiado el nombre de las siguientes columnas para ODBC 3. *x*. Los cambios en el nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones se enlazan por número de columna.  
  
|Columna ODBC 2.0|ODBC 3. *x* columna|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMIENTO _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Las siguientes columnas se han agregado al conjunto de resultados devuelto por **SQLProcedureColumns** para ODBC 3. *x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 En la tabla siguiente se enumeran las columnas del conjunto de resultados. El controlador puede definir columnas adicionales más allá de la columna 19 (IS_NULLABLE). Una aplicación debe obtener acceso a columnas específicas del controlador mediante la cuenta regresiva desde el final del conjunto de resultados en lugar de especificar una posición ordinal explícita. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
|Nombre de la columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Nombre del catálogo de procedimientos; NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunos procedimientos, pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellos procedimientos que no tienen catálogos.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Nombre del esquema de procedimiento; NULL si no es aplicable al origen de datos. Si un controlador admite esquemas para algunos procedimientos pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellos procedimientos que no tienen esquemas.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar no NULL|Nombre del procedimiento. Se devuelve una cadena vacía para un procedimiento que no tiene un nombre.|  
|COLUMN_NAME (ODBC 2.0)|4|Varchar no NULL|Nombre de columna de procedimiento. El controlador devuelve una cadena vacía para una columna de procedimiento que no tiene un nombre.|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint no NULL|Define la columna de procedimiento como un parámetro o una columna de conjunto de resultados:<br /><br /> SQL_PARAM_TYPE_UNKNOWN: La columna de procedimiento es un parámetro cuyo tipo es desconocido. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT: La columna de procedimiento es un parámetro de entrada. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: La columna de procedimiento es un parámetro de entrada/salida. (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT: La columna de procedimiento es un parámetro de salida. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: la columna de procedimiento es el valor devuelto del procedimiento. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: la columna de procedimiento es una columna de conjunto de resultados. (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint no NULL|Tipo de datos SQL. Puede ser un tipo de datos SQL ODBC o un tipo de datos SQL específico del controlador. Para los tipos de datos datetime e interval, esta columna devuelve los tipos de datos concisos (por ejemplo, SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Para obtener una lista de tipos de datos SQL ODBC válidos, vea Tipos de [datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en apéndice D: tipos de datos. Para obtener información acerca de los tipos de datos SQL específicos del controlador, consulte la documentación del controlador.|  
|TYPE_NAME (ODBC 2.0)|7|Varchar no NULL|Nombre de tipo de datos dependiente del origen de datos; por ejemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" o "CHAR ( ) FOR BIT DATA".|  
|COLUMN_SIZE (ODBC 2.0)|8|Entero|El tamaño de columna de la columna de procedimiento en el origen de datos. NULL se devuelve para los tipos de datos donde el tamaño de columna no es aplicable. Para obtener más información acerca de la precisión, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos.|  
|BUFFER_LENGTH (ODBC 2.0)|9|Entero|La longitud en bytes de datos transferidos en una operación **SQLGetData** o **SQLFetch** si se especifica SQL_C_DEFAULT. Para los datos numéricos, este tamaño puede ser diferente del tamaño de los datos almacenados en el origen de datos. Para obtener más información, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)de visualización , en Apéndice D: Tipos de datos.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|Los dígitos decimales de la columna de procedimiento en el origen de datos. NULL se devuelve para los tipos de datos donde los dígitos decimales no son aplicables. Para obtener más información acerca de los dígitos decimales, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)de visualización , en Apéndice D: Tipos de datos.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|Para los tipos de datos numéricos, 10 o 2.<br /><br /> Si es 10, los valores de COLUMN_SIZE y DECIMAL_DIGITS dan el número de dígitos decimales permitidos para la columna. Por ejemplo, una columna DECIMAL(12,5) devolvería un NUM_PREC_RADIX de 10, un COLUMN_SIZE de 12 y un DECIMAL_DIGITS de 5; una columna FLOAT podría devolver un NUM_PREC_RADIX de 10, un COLUMN_SIZE de 15 y un DECIMAL_DIGITS de NULL.<br /><br /> Si 2, los valores de COLUMN_SIZE y DECIMAL_DIGITS dan el número de bits permitidos en la columna. Por ejemplo, una columna FLOAT podría devolver un NUM_PREC_RADIX de 2, un COLUMN_SIZE de 53 y un DECIMAL_DIGITS de NULL.<br /><br /> NULL se devuelve para los tipos de datos donde NUM_PREC_RADIX no es aplicable.|  
|NULLABLE (ODBC 2.0)|12|Smallint no NULL|Si la columna de procedimiento acepta un valor NULL:<br /><br /> SQL_NO_NULLS: la columna de procedimiento no acepta valores NULL.<br /><br /> SQL_NULLABLE: la columna de procedimiento acepta valores NULL.<br /><br /> SQL_NULLABLE_UNKNOWN: No se sabe si la columna de procedimiento acepta valores NULL.|  
|MARCAS (ODBC 2.0)|13|Varchar|Una descripción de la columna de procedimiento.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|Valor predeterminado de la columna.<br /><br /> Si se especificó NULL como valor predeterminado, esta columna es la palabra NULL, no entre comillas. Si el valor predeterminado no se puede representar sin truncamiento, esta columna contiene TRUNCATED, sin comillas simples envolventes. Si no se especificó ningún valor predeterminado, esta columna es NULL.<br /><br /> El valor de COLUMN_DEF se puede utilizar para generar una nueva definición de columna, excepto cuando contiene el valor TRUNCATED.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint no NULL|El valor del tipo de datos SQL tal como aparece en el campo SQL_DESC_TYPE del descriptor. Esta columna es la misma que la columna DATA_TYPE, excepto para los tipos de datos datetime e interval.<br /><br /> Para los tipos de datos datetime e interval, el campo SQL_DATA_TYPE del conjunto de resultados devolverá SQL_INTERVAL o SQL_DATETIME y el campo SQL_DATETIME_SUB de datos devolverá el subcódigo para el tipo de datos de intervalo o fecha y hora específico. (Véase [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|El código de subtipo para los tipos de datos datetime e interval. Para otros tipos de datos, esta columna devuelve un VALOR NULL.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Entero|La longitud máxima en bytes de una columna de tipo de carácter o de tipo de datos binarios. Para todos los demás tipos de datos, esta columna devuelve NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer no NULL|Para los parámetros de entrada y salida, la posición ordinal del parámetro en la definición del procedimiento (en el orden del parámetro creciente, a partir de 1). Para un valor devuelto (si existe), se devuelve 0. Para las columnas del conjunto de resultados, la posición ordinal de la columna en el conjunto de resultados, con la primera columna del conjunto de resultados es el número 1. Si hay varios conjuntos de resultados, las posiciones ordinales de columna se devuelven de una manera específica del controlador.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"NO" si la columna no incluye los archivos NULL.<br /><br /> "SI" si la columna puede incluir NULLs.<br /><br /> Esta columna devuelve una cadena de longitud cero si no se conoce la nulabilidad.<br /><br /> Se siguen las normas ISO para determinar la nulabilidad. Un DBMS que cumpla la norma ISO SQL no puede devolver una cadena vacía.<br /><br /> El valor devuelto para esta columna es diferente del valor devuelto para la columna NULLABLE. (Consulte la descripción de la columna NULLABLE.)|  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [Llamadas de](../../../odbc/reference/develop-app/procedure-calls.md)procedimiento .  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver una lista de procedimientos en un origen de datos|[Función SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
