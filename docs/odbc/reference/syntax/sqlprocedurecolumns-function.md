---
title: Función SQLProcedureColumns | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 903d291c68cf61935294ed5fd983b6789c6407a3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlprocedurecolumns-function"></a>Función SQLProcedureColumns
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLProcedureColumns** devuelve la lista de parámetros de entrada y salida, así como las columnas que componen el conjunto de resultados de los procedimientos especificados. El controlador devuelve la información como un conjunto de resultados en la instrucción especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Nombre de catálogo del procedimiento. Si un controlador admite catálogos para algunos procedimientos, pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica los procedimientos que no tiene catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *schemaName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de esquema de procedimiento. Si un controlador es compatible con esquemas para algunos procedimientos, pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica los procedimientos que no tengan esquemas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *ProcName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de procedimiento.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *ProcName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *ProcName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **ProcName*.  
  
 *ColumnName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de columna.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *ColumnName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *ColumnName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength4*  
 [Entrada] Longitud en caracteres de **ColumnName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLProcedureColumns** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLProcedureColumns** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el controlador Administrador. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** si se hubiese llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y se devuelve el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** si no se hubiese llamado.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLError** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*. A continuación, se llama a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero null|El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *tipo de información* devuelve que los nombres de catálogo se admite.<br /><br /> (DM) se estableció el atributo de instrucción de SQL_ATTR_METADATA_ID en SQL_TRUE y el *SchemaName*, *ProcName*, o *ColumnName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función aynschronous aún se estaba ejecutando cuando se llamó a la función SQLProcedureColumns.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud de nombre era menor que 0 pero no es igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud de nombre supera el valor de longitud máxima para el catálogo correspondiente, el esquema, el procedimiento o el nombre de la columna.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo de procedimiento y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema de procedimiento y el controlador o el origen de datos no admite los esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el esquema de procedimiento, el nombre del procedimiento o el nombre de columna y el origen de datos no admite patrones de búsqueda para uno o varios de esos argumentos.<br /><br /> La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera expirado antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Esta función normalmente se utiliza antes de la ejecución de la instrucción para recuperar información sobre los parámetros de procedimiento y las columnas que componen el conjunto de resultados o conjuntos devueltos por el procedimiento, si lo hay. Para obtener más información, consulte [procedimientos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  **SQLProcedureColumns** no puede devolver todas las columnas utilizadas por un procedimiento. Por ejemplo, un controlador podría devolver solo información sobre los parámetros utilizados por un procedimiento y no las columnas de un conjunto de resultados que genera.  
  
 El *SchemaName*, *ProcName*, y *ColumnName* argumentos aceptan patrones de búsqueda. Para obtener más información sobre los patrones de búsqueda válidos, consulte [argumentos de valor de patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedureColumns** devuelve los resultados como un conjunto de resultados estándar, ordenado por PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME y COLUMN_TYPE. Se devuelven los nombres de columna para cada procedimiento en el siguiente orden: el nombre del valor devuelto, los nombres de cada parámetro en la invocación del procedimiento (en orden de llamada) y, a continuación, los nombres de cada columna del conjunto de resultados devuelto por el procedimiento (en orden de las columnas).  
  
 Las aplicaciones deben enlazar columnas específicas del controlador en relación con el final del conjunto de resultados. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
 Para determinar la longitud real de las columnas PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME y COLUMN_NAME, una aplicación puede llamar a **SQLGetInfo** con el SQL_MAX_ SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, PROCEDURE_NAME_LEN y las opciones de SQL_MAX_COLUMN_NAME_LEN.  
  
 Se ha cambiado el nombre de las columnas siguientes para ODBC 3. *x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones enlazar por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3. *x* columna|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMIENTO _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Las columnas siguientes se agregaron al conjunto de resultados devuelto por **SQLProcedureColumns** para ODBC 3. *x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. Columnas adicionales más allá de la columna 19 (IS_NULLABLE) pueden definirse mediante el controlador. Una aplicación debe tener acceso a columnas específicas del controlador contando hacia abajo desde el final del conjunto de resultados, en lugar de especificar una posición ordinal explícita. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Nombre de catálogo del procedimiento; Es NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunos procedimientos, pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para los procedimientos que no tiene catálogos.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Nombre de esquema de procedimiento; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con esquemas para algunos procedimientos, pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para los procedimientos que no tengan esquemas.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar no NULL|Nombre del procedimiento. Se devuelve una cadena vacía para un procedimiento que no tiene un nombre.|  
|COLUMN_NAME (ODBC 2.0)|4|Varchar no NULL|Nombre de la columna de procedimiento. El controlador devuelve una cadena vacía para una columna de procedimiento que no tiene un nombre.|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint no NULL|Define la columna de procedimiento como un parámetro o una columna de conjunto de resultados:<br /><br /> SQL_PARAM_TYPE_UNKNOWN: La columna de procedimiento es un parámetro cuyo tipo es desconocido. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT: La columna de procedimiento es un parámetro de entrada. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: La columna de procedimiento es un parámetro de entrada/salida. ODBC (1.0)<br /><br /> SQL_PARAM_OUTPUT: La columna de procedimiento es un parámetro de salida. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: La columna de procedimiento es el valor devuelto del procedimiento. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: La columna de procedimiento es una columna de conjunto de resultados. ODBC (1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint no NULL|Tipo de datos SQL. Puede tratarse de un tipo de datos SQL de ODBC o un tipo de datos SQL específico del controlador. Para los tipos de datos datetime e interval, esta columna devuelve los tipos de datos conciso (por ejemplo, SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Para obtener una lista de tipos de datos de ODBC SQL válidos, consulte [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en tipos de datos de apéndice D:. Para obtener información acerca de los tipos de datos SQL específico del controlador, consulte la documentación del controlador.|  
|TYPE_NAME (ODBC 2.0)|7|Varchar no NULL|Nombre de tipo de datos depende del origen de datos; "Por ejemplo,"CHAR", VARCHAR", "MONEY", "LONG VARBINARY" o "CHAR () para datos de bits".|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|El tamaño de la columna de la columna de procedimiento en el origen de datos. Se devuelve NULL para tipos de datos donde el tamaño de la columna no es aplicable. Para obtener más información sobre la precisión, vea [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en tipos de datos de apéndice D:.|  
|BUFFER_LENGTH (ODBC 2.0)|9|Integer|La longitud en bytes de datos transferidos en una **SQLGetData** o **SQLFetch** operación si se especifica SQL_C_DEFAULT. Para datos numéricos, este tamaño puede ser diferente que el tamaño de los datos almacenados en el origen de datos. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), en el apéndice D: tipos de datos.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|Los dígitos decimales de la columna de procedimiento en el origen de datos. Se devuelve NULL para tipos de datos que no es aplicables a los dígitos decimales. Para obtener más información relativa a los dígitos decimales, vea [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), en el apéndice D: tipos de datos.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|Para los tipos de datos numéricos, 10 ó 2.<br /><br /> Si es 10, los valores COLUMN_SIZE y DECIMAL_DIGITS proporcionan el número de dígitos decimales que se permiten para la columna. Por ejemplo, una columna DECIMAL(12,5) devolvería un NUM_PREC_RADIX de 10, un valor de COLUMN_SIZE de 12 y un DECIMAL_DIGITS de 5; una columna de tipo FLOAT podría devolver un NUM_PREC_RADIX de 10, un valor de COLUMN_SIZE de 15 y DECIMAL_DIGITS NULL.<br /><br /> Si es 2, los valores COLUMN_SIZE y DECIMAL_DIGITS proporcionan el número de bits que se permiten en la columna. Por ejemplo, una columna de tipo FLOAT podría devolver un NUM_PREC_RADIX de 2, un valor de COLUMN_SIZE de 53 y DECIMAL_DIGITS NULL.<br /><br /> Se devuelve NULL para tipos de datos donde NUM_PREC_RADIX no es aplicable.|  
|QUE ACEPTAN VALORES NULL (ODBC 2.0)|12|Smallint no NULL|Si la columna de procedimiento acepta un valor NULL:<br /><br /> SQL_NO_NULLS: La columna de procedimiento no acepta valores NULL.<br /><br /> SQL_NULLABLE: La columna de procedimiento acepta valores NULL.<br /><br /> SQL_NULLABLE_UNKNOWN: Se desconoce si la columna de procedimiento acepta valores NULL.|  
|COMENTARIOS (ODBC 2.0)|13|Varchar|Una descripción de la columna de procedimiento.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|El valor predeterminado de la columna.<br /><br /> Si se especifica NULL como valor predeterminado, esta columna es la palabra NULL, no entre comillas. Si el valor predeterminado no se puede representar sin truncamiento, esta columna contiene TRUNCA, ninguna inclusión entre comillas simples. Si se ha especificado ningún valor predeterminado, esta columna es NULL.<br /><br /> El valor de COLUMN_DEF puede utilizarse para generar una nueva definición de columna, excepto cuando contiene el valor TRUNCA.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint no NULL|El valor del tipo de datos SQL tal y como aparece en el campo SQL_DESC_TYPE del descriptor. Esta columna es la misma que la columna DATA_TYPE, salvo los tipos de datos datetime e interval.<br /><br /> Para los tipos de datos datetime e interval, el campo SQL_DATA_TYPE en el conjunto de resultados devolverá SQL_INTERVAL o SQL_DATETIME y el campo SQL_DATETIME_SUB devolverá el subcódigo para el tipo de datos específico de intervalo o datetime. (Consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|El código de subtipo para los tipos de datos datetime e interval. Para otros tipos de datos, esta columna devuelve un valor NULL.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|Columna de tipo de la longitud máxima en bytes de un carácter o datos binarios. Para todos los demás tipos de datos, esta columna devuelve NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer no NULL|Para los parámetros entradas y salidas, la posición ordinal del parámetro en la definición de procedimiento (en orden creciente de parámetro, empezando por 1). Un valor devuelto (si existe), se devuelve 0. Para las columnas del conjunto de resultados, se establece la posición ordinal de la columna en el resultado, con la primera columna del conjunto de resultados que se va a número 1. Si hay varios conjuntos de resultados, las posiciones ordinales de columna se devuelven en una manera específica del controlador.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"NO" si la columna no incluye valores NULL.<br /><br /> "Sí" si la columna puede incluir valores NULL.<br /><br /> Esta columna devuelve una cadena de longitud cero si no se conoce la nulabilidad.<br /><br /> Se siguen las normas ISO para determinar la nulabilidad. Un DBMS compatible con ISO SQL no puede devolver una cadena vacía.<br /><br /> El valor devuelto para esta columna es diferente del valor devuelto para la columna NULLABLE. (Vea la descripción de la columna admite valores NULL).|  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [las llamadas a procedimiento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Capturar una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver una lista de procedimientos en un origen de datos|[Función SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
