---
title: FUNción SQLGetTypeInfo ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47273c75a005f11b33e9929977b57607b36898de
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303266"
---
# <a name="sqlgettypeinfo-function"></a>Función SQLGetTypeInfo
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLGetTypeInfo** devuelve información sobre los tipos de datos admitidos por el origen de datos. El controlador devuelve la información en forma de un conjunto de resultados SQL. Los tipos de datos están diseñados para su uso en instrucciones de lenguaje de definición de datos (DDL).  
  
> [!IMPORTANT]  
>  Las aplicaciones deben usar los nombres de tipo devueltos en la columna TYPE_NAME del conjunto de resultados **SQLGetTypeInfo** en las instrucciones **ALTER TABLE** y **CREATE TABLE.** **SQLGetTypeInfo** puede devolver más de una fila con el mismo valor en la columna DATA_TYPE.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción para el conjunto de resultados.  
  
 *DataType*  
 [Entrada] El tipo de datos SQL. Debe ser uno de los valores de la sección Tipos de [datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) del Apéndice D: Tipos de datos o un tipo de datos SQL específico del controlador. SQL_ALL_TYPES especifica que se debe devolver información sobre todos los tipos de datos.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetTypeInfo** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLGetTypeInfo** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opción cambiado|Un atributo de instrucción especificado no era válido debido a las condiciones de trabajo de implementación, por lo que se sustituyó temporalmente un valor similar. (Llame a **SQLGetStmtAttr** para determinar el valor sustituido temporalmente.) El valor sustituto es válido para el *StatementHandle* hasta que se cierra el cursor. Los atributos de instrucción que se pueden cambiar son: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT y SQL_ATTR_SIMULATE_CURSOR. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle,* y **SQLFetch** o **SQLFetchScroll** se había llamado. El Administrador de controladores devuelve este error si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y lo devuelve el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.<br /><br /> Un conjunto de resultados estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY004|Tipo de datos SQL no válido|El valor especificado para el argumento *DataType* no era un identificador de tipo de datos ODBC SQL válido ni un identificador de tipo de datos específico del controlador admitido por el controlador.|  
|HY008|Operación cancelada|El procesamiento asincrónico se habilitó para *StatementHandle*, a continuación, se llamó a la función y, antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y, antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLGetTypeInfo** .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador correspondiente a *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetTypeInfo** devuelve los resultados como un conjunto de resultados estándar, ordenado por DATA_TYPE y, a continuación, por la proximidad con la que se asigna el tipo de datos al tipo de datos SQL ODBC correspondiente. Los tipos de datos definidos por el origen de datos tienen prioridad sobre los tipos de datos definidos por el usuario. Por lo tanto, el criterio de ordenación no es necesariamente coherente, pero se puede generalizar como DATA_TYPE primero, seguido de TYPE_NAME, ambos ascendentes. Por ejemplo, supongamos que un origen de datos definió los tipos de datos INTEGER y COUNTER, donde COUNTER es el incremento automático, y que también se ha definido un tipo de datos definido por el usuario WHOLENUM. Estos se devolverían en el orden INTEGER, WHOLENUM y COUNTER, porque WHOLENUM se asigna estrechamente al tipo de datos SQL ODBC SQL_INTEGER, mientras que el tipo de datos de incremento automático, aunque sea compatible con el origen de datos, no se asigna estrechamente a un tipo de datos SQL ODBC. Para obtener información sobre cómo se puede utilizar esta información, vea [Instrucciones DDL](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Si el *DataType* argumento especifica un tipo de datos que es válido para la versión de ODBC compatible con el controlador, pero no es compatible con el controlador, a continuación, devolverá un conjunto de resultados vacío.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de las funciones de catálogo ODBC, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
 Se ha cambiado el nombre de las siguientes columnas para ODBC 3. *x*. Los cambios en el nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones se enlazan por número de columna.  
  
|Columna ODBC 2.0|ODBC 3. *x* columna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 Las siguientes columnas se han agregado al conjunto de resultados devuelto por **SQLGetTypeInfo** para ODBC 3. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 En la tabla siguiente se enumeran las columnas del conjunto de resultados. El controlador puede definir columnas adicionales más allá de la columna 19 (INTERVAL_PRECISION). Una aplicación debe obtener acceso a columnas específicas del controlador mediante la cuenta regresiva desde el final del conjunto de resultados en lugar de especificar una posición ordinal explícita. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
> [!NOTE]  
>  **SQLGetTypeInfo** podría no devolver todos los tipos de datos. Por ejemplo, es posible que un controlador no devuelva tipos de datos definidos por el usuario. Las aplicaciones pueden usar cualquier tipo de datos válido, independientemente de si **SQLGetTypeInfo**lo devuelve. Los tipos de datos devueltos por **SQLGetTypeInfo** son los admitidos por el origen de datos. Están diseñados para su uso en instrucciones de lenguaje de definición de datos (DDL). Los controladores pueden devolver datos de conjunto de resultados mediante tipos de datos distintos de los tipos devueltos por **SQLGetTypeInfo**. Al crear el conjunto de resultados para una función de catálogo, el controlador puede usar un tipo de datos que no es compatible con el origen de datos.  
  
|Nombre de la columna|Columna<br /><br /> number|Tipo de datos|Comentarios|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar no NULL|Nombre de tipo de datos dependiente del origen de datos; por ejemplo, "CHAR()", "VARCHAR()", "MONEY", "LONG VARBINARY" o "CHAR ( ) FOR BIT DATA". Las aplicaciones deben utilizar este nombre en las instrucciones **CREATE TABLE** y **ALTER TABLE.**|  
|DATA_TYPE (ODBC 2.0)|2|Smallint no NULL|Tipo de datos SQL. Puede ser un tipo de datos SQL ODBC o un tipo de datos SQL específico del controlador. Para los tipos de datos datetime o interval, esta columna devuelve el tipo de datos conciso (como SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Para obtener una lista de tipos de datos SQL ODBC válidos, vea Tipos de [datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en apéndice D: tipos de datos. Para obtener información acerca de los tipos de datos SQL específicos del controlador, consulte la documentación del controlador.|  
|COLUMN_SIZE (ODBC 2.0)|3|Entero|El tamaño máximo de columna que admite el servidor para este tipo de datos. Para los datos numéricos, esta es la precisión máxima. Para los datos de cadena, esta es la longitud en caracteres. Para los tipos de datos datetime, esta es la longitud en caracteres de la representación de cadena (suponiendo la precisión máxima permitida del componente de fracciones de segundo). NULL se devuelve para los tipos de datos donde el tamaño de columna no es aplicable. Para los tipos de datos de intervalo, este es el número de caracteres en la representación de caracteres del literal de intervalo (según lo definido por la precisión inicial del intervalo; vea Longitud del [tipo](../../../odbc/reference/appendixes/interval-data-type-length.md) de datos de intervalo en apéndice D: tipos de datos).<br /><br /> Para obtener más información sobre el tamaño de columna, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos.|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|Carácter o caracteres utilizados para prefijar un literal; por ejemplo, una comilla simple (') para tipos de datos de caracteres o 0x para tipos de datos binarios; NULL se devuelve para los tipos de datos donde un prefijo literal no es aplicable.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|Carácter o caracteres utilizados para terminar un literal; por ejemplo, una comilla simple (') para los tipos de datos de caracteres; NULL se devuelve para los tipos de datos donde un sufijo literal no es aplicable.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|Una lista de palabras clave, separadas por comas, correspondientes a cada parámetro que la aplicación puede especificar entre paréntesis al usar el nombre que se devuelve en el campo TYPE_NAME. Las palabras clave de la lista pueden ser cualquiera de las siguientes: longitud, precisión o escala. Aparecen en el orden en que la sintaxis requiere que se utilicen. Por ejemplo, CREATE_PARAMS para DECIMAL sería "precisión, escala"; CREATE_PARAMS para VARCHAR sería igual a "longitud." NULL se devuelve si no hay parámetros para la definición de tipo de datos; por ejemplo, INTEGER.<br /><br /> El controlador proporciona el texto CREATE_PARAMS en el idioma del país o región donde se utiliza.|  
|NULLABLE (ODBC 2.0)|7|Smallint no NULL|Si el tipo de datos acepta un valor NULL:<br /><br /> SQL_NO_NULLS si el tipo de datos no acepta valores NULL.<br /><br /> SQL_NULLABLE si el tipo de datos acepta valores NULL.<br /><br /> SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL.|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint no NULL|Si un tipo de datos de caracteres distingue mayúsculas de minúsculas en intercalaciones y comparaciones:<br /><br /> SQL_TRUE si el tipo de datos es un tipo de datos de carácter y distingue mayúsculas de minúsculas.<br /><br /> SQL_FALSE si el tipo de datos no es un tipo de datos de carácter o no distingue mayúsculas de minúsculas.|  
|BUSQUEBLE (ODBC 2.0)|9|Smallint no NULL|Cómo se utiliza el tipo de datos en una cláusula **WHERE:**<br /><br /> SQL_PRED_NONE si la columna no se puede utilizar en una cláusula **WHERE.** (Esto es lo mismo que el valor de SQL_UNSEARCHABLE en ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR si la columna se puede utilizar en una cláusula **WHERE,** pero solo con el predicado **LIKE.** (Esto es lo mismo que el valor de SQL_LIKE_ONLY en ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC si la columna se puede utilizar en una cláusula **WHERE** con todos los operadores de comparación excepto **LIKE** (comparación, comparación cuantificada, **BETWEEN**, **DISTINCT**, **IN**, **MATCH**y **UNIQUE**). (Esto es lo mismo que el valor de SQL_ALL_EXCEPT_LIKE en ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE si la columna se puede utilizar en una cláusula **WHERE** con cualquier operador de comparación.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|Si el tipo de datos no está firmado:<br /><br /> SQL_TRUE si el tipo de datos no está firmado.<br /><br /> SQL_FALSE si el tipo de datos está firmado.<br /><br /> NULL se devuelve si el atributo no es aplicable al tipo de datos o el tipo de datos no es numérico.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint no NULL|Si el tipo de datos tiene una precisión y una escala fijas predefinidas (que son específicas del origen de datos), como un tipo de datos money:<br /><br /> SQL_TRUE si tiene precisión y escala fijas predefinidas.<br /><br /> SQL_FALSE si no tiene precisión y escala fijas predefinidas.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|Si el tipo de datos se está incrementando automáticamente:<br /><br /> SQL_TRUE si el tipo de datos se incrementa automáticamente.<br /><br /> SQL_FALSE si el tipo de datos no se incrementa automáticamente.<br /><br /> NULL se devuelve si el atributo no es aplicable al tipo de datos o el tipo de datos no es numérico.<br /><br /> Una aplicación puede insertar valores en una columna que tenga este atributo, pero normalmente no puede actualizar los valores de la columna.<br /><br /> Cuando se realiza una inserción en una columna de incremento automático, se inserta un valor único en la columna en el momento de la inserción. El incremento no está definido, pero es específico del origen de datos. Una aplicación no debe suponer que una columna de incremento automático comienza en un punto determinado o incrementos por cualquier valor determinado.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|Versión traducida del nombre del tipo de datos, dependiente del origen de datos. Se devuelve NULL si el origen de datos no admite un nombre traducido. Este nombre está pensado para mostrarse únicamente, como en los cuadros de diálogo.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|La escala mínima del tipo de datos en el origen de datos. Si un tipo de datos tiene una escala fija, las columnas MINIMUM_SCALE y MAXIMUM_SCALE contienen este valor. Por ejemplo, una columna SQL_TYPE_TIMESTAMP puede tener una escala fija durante fracciones de segundo. Se devuelve NULL cuando no se puede aplicar la escala. Para obtener más información, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en Apéndice D: Tipos de datos.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|La escala máxima del tipo de datos en el origen de datos. Se devuelve NULL cuando no se puede aplicar la escala. Si la escala máxima no se define por separado en el origen de datos, sino que se define como la misma que la precisión máxima, esta columna contiene el mismo valor que la columna COLUMN_SIZE. Para obtener más información, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en Apéndice D: Tipos de datos.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|Smallint NO NULL|El valor del tipo de datos SQL tal como aparece en el campo SQL_DESC_TYPE del descriptor. Esta columna es la misma que la columna DATA_TYPE, excepto para los tipos de datos interval y datetime.<br /><br /> Para los tipos de datos interval y datetime, el campo SQL_DATA_TYPE del conjunto de resultados devolverá SQL_INTERVAL o SQL_DATETIME y el campo SQL_DATETIME_SUB devolverá el subcódigo para el tipo de datos de intervalo o fecha y hora específico. (Véase [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|Cuando el valor de SQL_DATA_TYPE es SQL_DATETIME o SQL_INTERVAL, esta columna contiene el subcódigo datetime/interval. Para los tipos de datos distintos de datetime e interval, este campo es NULL.<br /><br /> Para los tipos de datos interval o datetime, el campo SQL_DATA_TYPE del conjunto de resultados devolverá SQL_INTERVAL o SQL_DATETIME y el campo SQL_DATETIME_SUB de datos devolverá el subcódigo para el tipo de datos de intervalo o fecha y hora específico. (Véase [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Entero|Si el tipo de datos es un tipo numérico aproximado, esta columna contiene el valor 2 para indicar que COLUMN_SIZE especifica un número de bits. Para los tipos numéricos exactos, esta columna contiene el valor 10 para indicar que COLUMN_SIZE especifica un número de dígitos decimales. De lo contrario, esta columna es NULL.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|Si el tipo de datos es un tipo de datos de intervalo, esta columna contiene el valor de la precisión inicial del intervalo. (Consulte Precisión del tipo de datos de [intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md) en el Apéndice D: Tipos de datos.) De lo contrario, esta columna es NULL.|  
  
 La información de atributos se puede aplicar a tipos de datos o a columnas específicas de un conjunto de resultados. **SQLGetTypeInfo** devuelve información sobre los atributos asociados a los tipos de datos; **SQLColAttribute** devuelve información sobre los atributos asociados a las columnas de un conjunto de resultados.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información sobre una columna en un conjunto de resultados|[Función SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Devolver información sobre un controlador o una fuente de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
