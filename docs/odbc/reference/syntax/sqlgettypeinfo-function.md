---
title: "Función SQLGetTypeInfo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7411a992bfbcb56a05e8ada5e4849a24ab8d2894
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettypeinfo-function"></a>Función SQLGetTypeInfo
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLGetTypeInfo** devuelve información acerca de los tipos de datos admitidos por el origen de datos. El controlador devuelve la información en forma de un conjunto de resultados SQL. Los tipos de datos están diseñados para su uso en las instrucciones de lenguaje de definición de datos (DDL).  
  
> [!IMPORTANT]  
>  Las aplicaciones deben utilizar los nombres de tipo devueltos en la columna TYPE_NAME de la **SQLGetTypeInfo** del conjunto de resultados **ALTER TABLE** y **CREATE TABLE** instrucciones. **SQLGetTypeInfo** puede devolver más de una fila con el mismo valor en la columna DATA_TYPE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción para el conjunto de resultados.  
  
 *Tipo de datos*  
 [Entrada] El tipo de datos SQL. Debe ser uno de los valores en el [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) sección del apéndice D: tipos de datos o un tipo de datos SQL específico del controlador. SQL_ALL_TYPES especifica que se debe devolver información acerca de todos los tipos de datos.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetTypeInfo** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL _HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetTypeInfo** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02 DE SQLSTATE|Ha cambiado el valor de opción|Un atributo de instrucción especificada no era válido debido a las condiciones de trabajo de implementación, por lo que un valor similar se sustituye temporalmente. (Llame a **SQLGetStmtAttr** para determinar el valor sustituido temporalmente.) El valor de reemplazo es válido para la *StatementHandle* hasta que se cierra el cursor. Los atributos de instrucción que se pueden cambiar son: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT y SQL_ATTR_SIMULATE_CURSOR. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle,* y **SQLFetch** o **SQLFetchScroll** si se hubiese llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y se devuelve el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un conjunto de resultados está abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** si no se hubiese llamado.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY004|Tipo de datos SQL no válido|El valor especificado para el argumento *DataType* no era un identificador válido de tipo de datos de ODBC SQL ni un identificador de tipo de datos específico del controlador admitida por el controlador.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*, a continuación, se llama a la función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** era llamar en el *StatementHandle*. A continuación, se llama a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLGetTypeInfo** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta finalizó antes de que el origen de datos devuelve el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetTypeInfo** devuelve los resultados como un conjunto de resultados estándar que se ordenan por DATA_TYPE y, a continuación, por la proximidad de los datos de tipos se asigna a los tipos de datos de ODBC SQL correspondientes. Tipos de datos definidos por el origen de datos tienen prioridad sobre los tipos de datos definidos por el usuario. Por lo tanto, el criterio de ordenación no es necesariamente coherente, pero puede ser generalizado como DATA_TYPE en primer lugar, a continuación, TYPE_NAME, ambos ascendente. Por ejemplo, suponga que un origen de datos define los tipos de datos entero y el contador, donde es el contador de incremento automático, y que también se ha definido un tipo de datos definido por el usuario WHOLENUM. Estos se devolverían en el orden de entero, WHOLENUM y contador, porque WHOLENUM se asigna estrechamente a los datos de ODBC SQL tipo SQL_INTEGER, mientras escribe los datos de incremento automático, aunque admitidos por el origen de datos, no se asignan estrechamente a un tipo de datos SQL de ODBC. Para obtener información acerca de cómo se podría utilizar esta información, consulte [instrucciones DDL](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Si el *DataType* argumento especifica un tipo de datos que es válido para la versión de ODBC compatible con el controlador, pero no es compatible con el controlador, a continuación, devolverá un conjunto de resultados vacío.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Se ha cambiado el nombre de las columnas siguientes para ODBC 3. *x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones enlazar por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3. *x* columna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 Las columnas siguientes se agregaron al conjunto de resultados devuelto por **SQLGetTypeInfo** para ODBC 3. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. Columnas adicionales más allá de la columna 19 (INTERVAL_PRECISION) pueden definirse mediante el controlador. Una aplicación debe tener acceso a columnas específicas del controlador contando hacia abajo desde el final del conjunto de resultados, en lugar de especificar una posición ordinal explícita. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** no puede devolver todos los tipos de datos. Por ejemplo, un controlador no podría devolver tipos de datos definidos por el usuario. Las aplicaciones pueden usar cualquier tipo de datos válido, independientemente de si se devuelve de forma **SQLGetTypeInfo**. Los tipos de datos devueltos por **SQLGetTypeInfo** son las que admite el origen de datos. Están diseñados para su uso en las instrucciones de lenguaje de definición de datos (DDL). Controladores pueden devolver datos de conjunto de resultados con tipos de datos distintos de los tipos devueltos por **SQLGetTypeInfo**. Al crear el conjunto de resultados de una función de catálogo, el controlador podría utilizar un tipo de datos que no es compatible con el origen de datos.  
  
|Nombre de columna|Columna<br /><br /> number|Tipo de datos|Comentarios|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar no NULL|Nombre de tipo de datos depende del origen de datos; Por ejemplo, "CHAR()", "VARCHAR()", "MONEY", "LONG VARBINARY" o "CHAR () para datos de bits". Las aplicaciones deben usar este nombre en **CREATE TABLE** y **ALTER TABLE** instrucciones.|  
|DATA_TYPE (ODBC 2.0)|2|Smallint no NULL|Tipo de datos SQL. Puede tratarse de un tipo de datos SQL de ODBC o un tipo de datos SQL específico del controlador. Para los tipos de datos datetime o intervalo, esta columna devuelve el tipo de datos conciso (por ejemplo, SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Para obtener una lista de tipos de datos de ODBC SQL válidos, consulte [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en tipos de datos de apéndice D:. Para obtener información acerca de los tipos de datos SQL específico del controlador, consulte la documentación del controlador.|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|El tamaño máximo de la columna que admite el servidor para este tipo de datos. Para datos numéricos, esto es la precisión máxima. Para los datos de cadena, se trata de la longitud en caracteres. Para los tipos de datos de fecha y hora, se trata de la longitud en caracteres de la representación de cadena (suponiendo la precisión máxima permitida del componente de fracciones de segundo). Se devuelve NULL para tipos de datos donde el tamaño de la columna no es aplicable. Para los tipos de datos de intervalo, es el número de caracteres en la representación de caracteres del intervalo literal (tal como se define por el intervalo a la precisión; vea [longitud del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md) en tipos de datos de apéndice D:).<br /><br /> Para obtener más información sobre el tamaño de la columna, vea [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en tipos de datos de apéndice D:.|  
|CARACTERES LITERAL_PREFIX (ODBC 2.0)|4|Varchar|Carácter o caracteres utilizados para prefijar un literal; Por ejemplo, una comilla simple (') para tipos de datos de caracteres o 0 x para tipos de datos binarios; Se devuelve NULL para tipos de datos donde un prefijo literal no es aplicable.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|Carácter o caracteres utilizados para terminar un literal; Por ejemplo, una comilla simple (') para tipos de datos de caracteres; Se devuelve NULL para tipos de datos donde un sufijo literal no es aplicable.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|Una lista de palabras clave, separadas por coma, que corresponden a cada parámetro que la aplicación puede especificar entre paréntesis cuando se utiliza el nombre que se devuelve en el campo TYPE_NAME. Las palabras clave en la lista pueden ser cualquiera de las siguientes acciones: longitud, precisión o escala. Aparecen en el orden en que la sintaxis requiere que se utilicen. Por ejemplo, sería CREATE_PARAMS para DECIMAL "precisión, escala"; CREATE_PARAMS para VARCHAR equivaldría a "longitud". Se devuelve NULL si no hay ningún parámetro para la definición de tipo de datos; Por ejemplo, entero.<br /><br /> El controlador proporciona el texto CREATE_PARAMS en el idioma de país o región donde se utiliza.|  
|QUE ACEPTAN VALORES NULL (ODBC 2.0)|7|Smallint no NULL|Si el tipo de datos acepta un valor NULL:<br /><br /> SQL_NO_NULLS si el tipo de datos no acepta valores NULL.<br /><br /> SQL_NULLABLE si el tipo de datos acepta valores NULL.<br /><br /> SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL.|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint no NULL|Si un tipo de datos de carácter distingue mayúsculas de minúsculas en las intercalaciones y comparaciones:<br /><br /> SQL_TRUE si el tipo de datos es un tipo de datos de caracteres y distingue mayúsculas de minúsculas.<br /><br /> SQL_FALSE si el tipo de datos no es un tipo de datos de caracteres o no distingue mayúsculas de minúsculas.|  
|PERMITE REALIZAR BÚSQUEDA (ODBC 2.0)|9|Smallint no NULL|¿Cómo se utiliza el tipo de datos en un **donde** cláusula:<br /><br /> SQL_PRED_NONE si la columna no se puede usar en un **donde** cláusula. (Este es el mismo que el valor SQL_UNSEARCHABLE en ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR si la columna se puede utilizar en una **donde** cláusula, pero solo con el **como** predicado. (Este es el mismo que el valor SQL_LIKE_ONLY en ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC si la columna se puede utilizar en una **donde** cláusula con todos los operadores de comparación excepto **como** (comparación, comparación cuantificada, **BETWEEN**,  **DISTINCT**, **IN**, **coincidencia**, y **UNIQUE**). (Este es el mismo que el valor SQL_ALL_EXCEPT_LIKE en ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE si la columna se puede utilizar en una **donde** cláusula con cualquier operador de comparación.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|Indica si el tipo de datos es sin signo:<br /><br /> SQL_TRUE si el tipo de datos es sin signo.<br /><br /> SQL_FALSE si el tipo de datos es con signo.<br /><br /> Se devuelve NULL si el atributo no es aplicable al tipo de datos o el tipo de datos no es numérico.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint no NULL|Si tiene predefinidos el tipo de datos se ha corregido precisión y escala (que son específicos del origen de datos), como un tipo de datos money:<br /><br /> Precisión y escala fijas SQL_TRUE si tiene predefinidos.<br /><br /> SQL_FALSE si no tiene escala y precisión fija predefinido.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|Indica si el tipo de datos es de incremento automático:<br /><br /> SQL_TRUE si el tipo de datos es de incremento automático.<br /><br /> SQL_FALSE si el tipo de datos no es de incremento automático.<br /><br /> Se devuelve NULL si el atributo no es aplicable al tipo de datos o el tipo de datos no es numérico.<br /><br /> Una aplicación puede insertar valores en una columna con este atributo, pero normalmente no puede actualizar los valores de la columna.<br /><br /> Cuando se realiza una inserción en una columna de incremento automático, se inserta un valor único en la columna en el momento de la inserción. El incremento no está definido, pero es específico del origen de datos. Una aplicación no debe suponer que una columna de incremento automático comienza en cualquier momento determinado o incrementos en cualquier valor determinado.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|Versión localizada del depende del origen de datos del tipo de datos. Se devuelve NULL si el origen de datos no admite un nombre traducido. Este nombre está pensado para mostrar solo, como cuadros de diálogo.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|La escala mínima del tipo de datos del origen de datos. Si un tipo de datos tiene una escala fija, las columnas MINIMUM_SCALE y MAXIMUM_SCALE contienen este valor. Por ejemplo, una columna SQL_TYPE_TIMESTAMP podría tener una escala fija para las fracciones de segundo. Se devuelve NULL cuando no se puede aplicar la escala. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en tipos de datos de apéndice D:.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|La escala máxima del tipo de datos del origen de datos. Se devuelve NULL cuando no se puede aplicar la escala. Si la escala máxima no está definida por separado en el origen de datos, pero en su lugar, se define como el mismo que la precisión máxima, esta columna contiene el mismo valor que la columna COLUMN_SIZE. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en tipos de datos de apéndice D:.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|Smallint no NULL|El valor del tipo de datos SQL tal y como aparece en el campo SQL_DESC_TYPE del descriptor. Esta columna es la misma que la columna DATA_TYPE, salvo los tipos de datos datetime y de intervalo.<br /><br /> Para tipos de datos datetime y de intervalo, el campo SQL_DATA_TYPE en el conjunto de resultados devolverá SQL_INTERVAL o SQL_DATETIME y el campo SQL_DATETIME_SUB devolverá el subcódigo para el tipo de datos específico de intervalo o datetime. (Consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|Cuando el valor de SQL_DATA_TYPE es SQL_DATETIME o SQL_INTERVAL, esta columna contiene el subcódigo/intervalo de fecha y hora. Para los tipos de datos distintos de datetime e interval, este campo es NULL.<br /><br /> Para los tipos de datos de intervalo o datetime, el campo SQL_DATA_TYPE en el conjunto de resultados devolverá SQL_INTERVAL o SQL_DATETIME y el campo SQL_DATETIME_SUB devolverá el subcódigo para el tipo de datos específico de intervalo o datetime. (Consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|Si el tipo de datos es un tipo numérico aproximado, esta columna contiene el valor 2 para indicar que COLUMN_SIZE especifica un número de bits. Para tipos numéricos exactos, esta columna contiene el valor 10 para indicar que COLUMN_SIZE especifica un número de dígitos decimales. De lo contrario, esta columna es NULL.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|Si el tipo de datos es un tipo de datos de intervalo, esta columna contiene el valor de la precisión inicial del intervalo. (Consulte [precisión del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md) en tipos de datos de apéndice D:.) De lo contrario, esta columna es NULL.|  
  
 Información de atributo se puede aplicar a tipos de datos o a columnas específicas en un conjunto de resultados. **SQLGetTypeInfo** devuelve información acerca de los atributos asociados con los tipos de datos; **SQLColAttribute** devuelve información acerca de los atributos asociados a las columnas en un conjunto de resultados.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[Función SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Capturar una sola fila o un bloque de datos en una dirección de solo avance|[SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Devolver información acerca de un controlador o un origen de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

