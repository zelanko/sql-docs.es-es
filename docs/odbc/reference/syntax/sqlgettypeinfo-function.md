---
title: Función SQLGetTypeInfo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aef1e90053eba71db84e1fe89aa90684829a4941
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536534"
---
# <a name="sqlgettypeinfo-function"></a>Función SQLGetTypeInfo
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLGetTypeInfo** devuelve información acerca de los tipos de datos admitidos por el origen de datos. El controlador devuelve la información en forma de un conjunto de resultados SQL. Los tipos de datos están diseñados para su uso en las instrucciones de lenguaje de definición de datos (DDL).  
  
> [!IMPORTANT]  
>  Las aplicaciones deben usar los nombres de tipo devueltos en la columna TYPE_NAME del **SQLGetTypeInfo** del conjunto de resultados **ALTER TABLE** y **CREATE TABLE** instrucciones. **SQLGetTypeInfo** puede devolver más de una fila con el mismo valor en la columna DATA_TYPE.  
  
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
 [Entrada] El tipo de datos SQL. Debe ser uno de los valores de la [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) sección del apéndice D: Tipos de datos o un tipo de datos SQL específicas del controlador. SQL_ALL_TYPES especifica que se debe devolver información acerca de todos los tipos de datos.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetTypeInfo** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL _HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetTypeInfo** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02|Valor de opción cambiado|Un atributo de instrucción especificado no era válido debido a las condiciones de trabajo de implementación, por lo que temporalmente se ha sustituido por un valor similar. (Llame a **SQLGetStmtAttr** para determinar el valor sustituido temporalmente.) El valor de reemplazo es válido para el *StatementHandle* hasta que se cierra el cursor. Los atributos de instrucción que se pueden cambiar son: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT y SQL_ATTR_SIMULATE_CURSOR. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle,* y **SQLFetch** o **SQLFetchScroll** hubiera llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un conjunto de resultados estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY004|Tipo de datos SQL no válido|El valor especificado para el argumento *DataType* no era un identificador de tipo de datos de ODBC SQL válido ni un identificador de tipo de datos específico del controlador admitida por el controlador.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*, a continuación, se llamó a la función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** era se llama en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLGetTypeInfo** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y se ha establecido el atributo de instrucción SQL_ATTR_CURSOR_TYPE a un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente a la *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetTypeInfo** devuelve los resultados como un conjunto de resultados estándar, que se ordenan por DATA_TYPE y, a continuación, por proximidad el tipo de datos se asigna a los tipos de datos ODBC SQL correspondientes. Tipos de datos definidos por el origen de datos tienen prioridad sobre los tipos de datos definido por el usuario. Por lo tanto, el criterio de ordenación no es necesariamente coherente, pero puede ser generalizado como DATA_TYPE en primer lugar, seguido TYPE_NAME, ambos ascendente. Por ejemplo, suponga que un origen de datos define los tipos de datos entero y el contador, donde es el contador de incremento automático, y que también se ha definido un tipo de datos definido por el usuario WHOLENUM. Estos se devolverían en el orden de entero, WHOLENUM y contador, porque WHOLENUM se asigna estrechamente a los datos de ODBC SQL tipo SQL_INTEGER, mientras escribe los datos de incremento automático, aunque compatibles con el origen de datos, no se asignan estrechamente a un tipo de datos SQL de ODBC. Para obtener información acerca de cómo se podría utilizar esta información, consulte [instrucciones DDL](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Si el *DataType* argumento especifica un tipo de datos que es válido para la versión de ODBC compatible con el controlador, pero no es compatible con el controlador y, después, devolverá un conjunto de resultados vacío.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Las columnas siguientes se han cambiado para ODBC 3. *x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque el enlace de aplicaciones por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3. *x* columna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 Se han agregado las siguientes columnas para el conjunto de resultados devuelto por **SQLGetTypeInfo** para ODBC 3. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. Las columnas adicionales más allá de la columna 19 (INTERVAL_PRECISION) pueden definirse mediante el controlador. Una aplicación debe tener acceso a las columnas específicas del controlador mediante la cuenta atrás desde el final del conjunto de resultados, en lugar de especificar una posición ordinal explícita. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** no podría devolver todos los tipos de datos. Por ejemplo, un controlador puede no devolver tipos de datos definido por el usuario. Las aplicaciones pueden utilizar cualquier tipo de datos válido, independientemente de si se devuelve de forma **SQLGetTypeInfo**. Los tipos de datos devueltos por **SQLGetTypeInfo** son las que admite el origen de datos. Están diseñados para su uso en las instrucciones de lenguaje de definición de datos (DDL). Los controladores pueden devolver los datos de conjunto de resultados con los tipos de datos distintos de los tipos devueltos por **SQLGetTypeInfo**. Al crear el conjunto de resultados de una función de catálogo, el controlador podría utilizar un tipo de datos que no se admite el origen de datos.  
  
|Nombre de columna|columna<br /><br /> number|Tipo de datos|Comentarios|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar no es NULL|Nombre de tipo de datos depende del origen de datos; Por ejemplo, "CHAR()", "VARCHAR()", "MONEY", "LONG VARBINARY" o "CHAR () para datos de bits". Las aplicaciones deben usar este nombre en **CREATE TABLE** y **ALTER TABLE** instrucciones.|  
|DATA_TYPE (ODBC 2.0)|2|Smallint no NULL|Tipo de datos SQL. Esto puede ser un tipo de datos SQL de ODBC o un tipo de datos SQL específicas del controlador. Para los tipos de datos datetime o intervalo, esta columna devuelve el tipo de datos conciso (por ejemplo, SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Para obtener una lista de tipos de datos ODBC SQL válidos, vea [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en el apéndice D: Tipos de datos. Para obtener información acerca de los tipos de datos SQL específicas del controlador, consulte la documentación del controlador.|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|El tamaño máximo de columna que admite el servidor para este tipo de datos. Para los datos numéricos, se trata de la precisión máxima. Para los datos de cadena, se trata de la longitud en caracteres. Para los tipos de datos de fecha y hora, se trata de la longitud en caracteres de la representación de cadena (suponiendo la precisión máxima permitida del componente de fracciones de segundo). Se devuelve NULL para los tipos de datos donde el tamaño de la columna no es aplicable. Para los tipos de datos de intervalo, es el número de caracteres en la representación de caracteres del intervalo de literal (tal como se define por el intervalo inicial precisión; vea [longitud del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md) en el apéndice D: Tipos de datos).<br /><br /> Para obtener más información sobre el tamaño de la columna, vea [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos.|  
|CARACTERES LITERAL_PREFIX (ODBC 2.0)|4|Varchar|Carácter o caracteres utilizados para prefijar un literal; Por ejemplo, una comilla simple (') para tipos de datos de caracteres o 0 x para tipos de datos binarios; Se devuelve NULL para los tipos de datos donde un prefijo de literal no es aplicable.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|Carácter o caracteres utilizados para terminar un literal; Por ejemplo, una comilla simple (') para tipos de datos de caracteres; Se devuelve NULL para los tipos de datos donde un sufijo literal no es aplicable.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|Una lista de palabras clave, separadas por comas, correspondiente a cada parámetro que la aplicación puede especificar entre paréntesis al usar el nombre que se devuelve en el campo TYPE_NAME. Las palabras clave en la lista pueden ser cualquiera de las siguientes acciones: longitud, precisión o escala. Aparecen en el orden en que la sintaxis requiere que se utilicen. Por ejemplo, sería CREATE_PARAMS para separar los decimales "precisión, escala"; CREATE_PARAMS para VARCHAR equivaldría al "longitud". Se devuelve NULL si no hay ningún parámetro para la definición de tipo de datos; Por ejemplo, entero.<br /><br /> El controlador proporciona el texto CREATE_PARAMS en el idioma de país o región donde se utiliza.|  
|QUE ACEPTA VALORES NULL (ODBC 2.0)|7|Smallint no NULL|Si el tipo de datos acepta un valor NULL:<br /><br /> SQL_NO_NULLS si el tipo de datos no acepta valores NULL.<br /><br /> SQL_NULLABLE si el tipo de datos acepta valores NULL.<br /><br /> SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL.|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint no NULL|Si un tipo de datos de carácter distingue mayúsculas de minúsculas en las intercalaciones y comparaciones:<br /><br /> SQL_TRUE si el tipo de datos es un tipo de datos de caracteres y distingue mayúsculas de minúsculas.<br /><br /> SQL_FALSE si el tipo de datos no es un tipo de datos de caracteres o no distingue mayúsculas de minúsculas.|  
|BÚSQUEDA (ODBC 2.0)|9|Smallint no NULL|Cómo se usa el tipo de datos en un **donde** cláusula:<br /><br /> SQL_PRED_NONE si la columna no se puede usar en un **donde** cláusula. (Esto es el mismo que el valor SQL_UNSEARCHABLE de ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR si la columna se puede usar en un **donde** cláusula, pero solo con el **como** predicado. (Esto es el mismo que el valor SQL_LIKE_ONLY de ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC si la columna se puede usar en un **donde** cláusula con todos los operadores de comparación excepto **como** (comparación, comparación cuantificada, **BETWEEN**,  **DISTINCT**, **IN**, **coincidencia**, y **UNIQUE**). (Esto es el mismo que el valor SQL_ALL_EXCEPT_LIKE de ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE si la columna se puede usar en un **donde** cláusula con cualquier operador de comparación.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|Indica si el tipo de datos es sin signo:<br /><br /> SQL_TRUE si el tipo de datos es sin signo.<br /><br /> SQL_FALSE si el tipo de datos está firmado.<br /><br /> Se devuelve NULL si el atributo no es aplicable al tipo de datos o el tipo de datos no es numérico.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint no NULL|Si ha predefinido el tipo de datos fija la precisión y escala (que son específicas del origen de datos), como un tipo de datos money:<br /><br /> Precisión y escala fijas SQL_TRUE si predefinidos.<br /><br /> SQL_FALSE si no dispone de la escala y precisión fija predefinido.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|Indica si el tipo de datos es de incremento automático:<br /><br /> SQL_TRUE si el tipo de datos es de incremento automático.<br /><br /> SQL_FALSE si el tipo de datos no es de incremento automático.<br /><br /> Se devuelve NULL si el atributo no es aplicable al tipo de datos o el tipo de datos no es numérico.<br /><br /> Una aplicación puede insertar valores en una columna de este atributo, pero normalmente no puede actualizar los valores de la columna.<br /><br /> Cuando se realiza una inserción en una columna de incremento automático, se inserta un valor único en la columna en el momento de la inserción. El incremento no está definido, pero es específica del origen de datos. Una aplicación no debe suponer que una columna de incremento automático comienza en cualquier momento determinado o incrementos por cualquier valor concreto.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|Versión traducida del nombre del tipo de datos, dependiente del origen de datos. Se devuelve NULL si el origen de datos no admite un nombre traducido. Este nombre está diseñado para mostrar solo, como en los cuadros de diálogo.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|La escala mínima del tipo de datos del origen de datos. Si un tipo de datos tiene una escala fija, las columnas MINIMUM_SCALE y MAXIMUM_SCALE contienen este valor. Por ejemplo, una columna SQL_TYPE_TIMESTAMP podría tener una escala fija para las fracciones. Se devuelve NULL cuando no se puede aplicar la escala. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|La escala máxima del tipo de datos del origen de datos. Se devuelve NULL cuando no se puede aplicar la escala. Si la escala máxima no está definida por separado en el origen de datos, pero en su lugar, se define como el mismo que la precisión máxima, esta columna contiene el mismo valor que la columna COLUMN_SIZE. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|smallint no NULL|El valor del tipo de datos SQL tal y como aparece en el campo SQL_DESC_TYPE del descriptor. Esta columna es igual que la columna DATA_TYPE, salvo los tipos de datos de intervalo y la fecha y hora.<br /><br /> Para los tipos de datos de intervalo y la fecha y hora, el campo SQL_DATA_TYPE del conjunto de resultados devolverá SQL_INTERVAL o SQL_DATETIME y el campo SQL_DATETIME_SUB devolverá el subcódigo para el tipo de datos específico de intervalo o datetime. (Consulte [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|Cuando el valor de SQL_DATA_TYPE es SQL_DATETIME o SQL_INTERVAL, esta columna contiene el subcódigo de datetime o intervalo. Para los tipos de datos distintos de datetime e interval, este campo es NULL.<br /><br /> Para los tipos de datos datetime o intervalo, el campo SQL_DATA_TYPE del conjunto de resultados devolverá SQL_INTERVAL o SQL_DATETIME y el campo SQL_DATETIME_SUB devolverá el subcódigo para el tipo de datos específico de intervalo o datetime. (Consulte [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|Si el tipo de datos es un tipo numérico aproximado, esta columna contiene el valor 2 para indicar que COLUMN_SIZE especifica un número de bits. Para tipos numéricos exactos, esta columna contiene el valor 10 para indicar que COLUMN_SIZE especifica el número de dígitos decimales. De lo contrario, esta columna es NULL.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|Si el tipo de datos es un tipo de datos de intervalo, esta columna contiene el valor de la precisión inicial del intervalo. (Consulte [precisión del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md) en el apéndice D: Tipos de datos). De lo contrario, esta columna es NULL.|  
  
 Información de atributos puede aplicar a tipos de datos o a columnas específicas en un conjunto de resultados. **SQLGetTypeInfo** devuelve información acerca de los atributos asociados con los tipos de datos; **SQLColAttribute** devuelve información acerca de los atributos asociados a las columnas en un conjunto de resultados.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[Función SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Devolver información acerca de un controlador o un origen de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
