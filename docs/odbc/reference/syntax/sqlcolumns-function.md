---
title: Función SQLColumns (SQLColumns) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36293c1f2393e9a57351fc8cd19dcc6e3338f5cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301261"
---
# <a name="sqlcolumns-function"></a>Función SQLColumns
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: Grupo abierto  
  
 **Resumen**  
 **SQLColumns** devuelve la lista de nombres de columna en tablas especificadas. El controlador devuelve esta información como un conjunto de resultados en el *StatementHandle*especificado .  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *CatalogName*  
 [Entrada] Nombre del catálogo. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadenas.  
  
> [!NOTE]  
>  Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente, y su caso es significativo. Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de esquema. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen esquemas.  
  
> [!NOTE]  
>  Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de tabla.  
  
> [!NOTE]  
>  Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *TableName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *ColumnName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de columna.  
  
> [!NOTE]  
>  Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *ColumnName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *ColumnName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength4*  
 [Entrada] Longitud en caracteres de **ColumnName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLColumns** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLColumns** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** se había llamado. El Administrador de controladores devuelve este error si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y lo devuelve el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle* pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y el SQL_CATALOG_NAME *InfoType* devuelve que se admiten los nombres de catálogo.<br /><br /> (DM) el atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE y el argumento *SchemaName*, *TableName*o *ColumnName* era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLColumns.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El valor de uno de los argumentos de longitud de nombre era menor que 0 pero no igual a SQL_NTS.|  
|||El valor de uno de los argumentos de longitud de nombre superó el valor de longitud máxima para el catálogo o nombre correspondiente. La longitud máxima de cada catálogo o nombre se puede obtener llamando a **SQLGetInfo** con el *InfoType* valores. (Véase "Comentarios.")|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|Se especificó un nombre de catálogo y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un nombre de esquema y el controlador o el origen de datos no admite esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el nombre de esquema, el nombre de tabla o el nombre de columna, y el origen de datos no admite patrones de búsqueda para uno o varios de esos argumentos.<br /><br /> El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Esta función se utiliza normalmente antes de la ejecución de instrucciones para recuperar información sobre las columnas de una tabla o tablas del catálogo del origen de datos. **SQLColumns** se puede utilizar para recuperar datos para todos los tipos de elementos devueltos por **SQLTables**. Además de las tablas base, esto puede incluir (pero no se limita a) vistas, sinónimos, tablas del sistema, etc. Por el contrario, las funciones **SQLColAttribute** y **SQLDescribeCol** describen las columnas de un conjunto de resultados y la función **SQLNumResultCols** devuelve el número de columnas de un conjunto de resultados. Para obtener más información, consulte [Usos de datos de catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de las funciones de catálogo ODBC, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
 **SQLColumns** devuelve los resultados como un conjunto de resultados estándar, ordenados por TABLE_CAT, TABLE_SCHEM, TABLE_NAME y ORDINAL_POSITION.  
  
> [!NOTE]  
>  Cuando una aplicación funciona con un ODBC 2. *x* driver, no se devuelve ninguna columna ORDINAL_POSITION en el conjunto de resultados. Como resultado, cuando se trabaja con ODBC 2. *x* controladores, el orden de las columnas de la lista de columnas devuelta por **SQLColumns** no es necesariamente el mismo que el orden de las columnas devueltas cuando la aplicación realiza una instrucción SELECT en todas las columnas de esa tabla.  
  
> [!NOTE]  
>  **SQLColumns** podría no devolver todas las columnas. Por ejemplo, es posible que un controlador no devuelva información sobre pseudocolumnas, como Oracle ROWID. Las aplicaciones pueden usar cualquier columna válida, ya sea que **SQLColumns**la devuelva.  
>   
>  **SQLColumns**no devuelve algunas columnas que **SQLStatistics** puede devolver. Por ejemplo, **SQLColumns** no devuelve las columnas de un índice creado sobre una expresión o filtro, como SALARY + BENEFITS o DEPT a 0012.  
  
 Las longitudes de las columnas VARCHAR no se muestran en la tabla; las longitudes reales dependen del origen de datos. Para determinar las longitudes reales de las columnas TABLE_CAT, TABLE_SCHEM, TABLE_NAME y COLUMN_NAME, una aplicación puede llamar a **SQLGetInfo** con las opciones SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN y SQL_MAX_COLUMN_NAME_LEN.  
  
 Se ha cambiado el nombre de las siguientes columnas para ODBC 3. *x*. Los cambios en el nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones se enlazan por número de columna.  
  
|Columna ODBC 2.0|ODBC 3. *x* columna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Las siguientes columnas se han agregado al conjunto de resultados devuelto por **SQLColumns** para ODBC 3. *x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 En la tabla siguiente se enumeran las columnas del conjunto de resultados. El controlador puede definir columnas adicionales más allá de la columna 18 (IS_NULLABLE). Una aplicación debe obtener acceso a columnas específicas del controlador mediante la cuenta regresiva desde el final del conjunto de resultados en lugar de especificar una posición ordinal explícita. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
|Nombre de la columna|Columna<br /><br /> number|Tipo de datos|Comentarios|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nombre del catálogo; NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellas tablas que no tienen catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema; NULL si no es aplicable al origen de datos. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tienen esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar no NULL|Nombre de la tabla.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar no NULL|Nombre de la columna. El controlador devuelve una cadena vacía para una columna que no tiene un nombre.|  
|DATA_TYPE (ODBC 1.0)|5|Smallint no NULL|Tipo de datos SQL. Puede ser un tipo de datos SQL ODBC o un tipo de datos SQL específico del controlador. Para los tipos de datos datetime e interval, esta columna devuelve el tipo de datos conciso (como SQL_TYPE_DATE o SQL_INTERVAL_YEAR_TO_MONTH, en lugar del tipo de datos no conciso como SQL_DATETIME o SQL_INTERVAL). Para obtener una lista de tipos de datos SQL ODBC válidos, vea Tipos de [datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en apéndice D: tipos de datos. Para obtener información acerca de los tipos de datos SQL específicos del controlador, consulte la documentación del controlador.<br /><br /> Los tipos de datos devueltos para ODBC 3. *x* y ODBC 2. *x* aplicaciones pueden ser diferentes. Para obtener más información, consulte [Compatibilidad con versiones anteriores y Cumplimiento](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)de normas .|  
|TYPE_NAME (ODBC 1.0)|6|Varchar no NULL|Nombre de tipo de datos dependiente del origen de datos; por ejemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINAR" o "CHAR ( ) FOR BIT DATA".|  
|COLUMN_SIZE (ODBC 1.0)|7|Entero|Si DATA_TYPE es SQL_CHAR o SQL_VARCHAR, esta columna contiene la longitud máxima en caracteres de la columna. Para los tipos de datos datetime, este es el número total de caracteres necesarios para mostrar el valor cuando se convierte en caracteres. Para los tipos de datos numéricos, se trata del número total de dígitos o el número total de bits permitidos en la columna, según la columna NUM_PREC_RADIX. Para los tipos de datos de intervalo, este es el número de caracteres en la representación de caracteres del literal de intervalo (según lo definido por la precisión inicial del intervalo, vea Longitud del [tipo](../../../odbc/reference/appendixes/interval-data-type-length.md) de datos de intervalo en apéndice D: tipos de datos). Para obtener más información, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en Apéndice D: Tipos de datos.|  
|BUFFER_LENGTH (ODBC 1.0)|8|Entero|La longitud en bytes de datos transferidos en una operación SQLGetData, SQLFetch o SQLFetchScroll si se especifica SQL_C_DEFAULT. Para los datos numéricos, este tamaño puede diferir del tamaño de los datos almacenados en el origen de datos. Este valor puede diferir de COLUMN_SIZE columna para los datos de caracteres. Para obtener más información acerca de la longitud, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|El número total de dígitos significativos a la derecha del punto decimal. Para SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP, esta columna contiene el número de dígitos en el componente de fracciones de segundo. Para los otros tipos de datos, estos son los dígitos decimales de la columna en el origen de datos. Para los tipos de datos de intervalo que contienen un componente de tiempo, esta columna contiene el número de dígitos a la derecha del punto decimal (segundos fraccionarios). Para los tipos de datos de intervalo que no contienen un componente de tiempo, esta columna es 0. Para obtener más información acerca de los dígitos decimales, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos. NULL se devuelve para los tipos de datos donde DECIMAL_DIGITS no es aplicable.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|Para los tipos de datos numéricos, 10 o 2. Si es 10, los valores de COLUMN_SIZE y DECIMAL_DIGITS dan el número de dígitos decimales permitidos para la columna. Por ejemplo, una columna DECIMAL(12,5) devolvería un NUM_PREC_RADIX de 10, un COLUMN_SIZE de 12 y un DECIMAL_DIGITS de 5; una columna FLOAT podría devolver un NUM_PREC_RADIX de 10, un COLUMN_SIZE de 15 y un DECIMAL_DIGITS de NULL.<br /><br /> Si es 2, los valores de COLUMN_SIZE y DECIMAL_DIGITS dan el número de bits permitidos en la columna. Por ejemplo, una columna FLOAT podría devolver un RADIX de 2, un COLUMN_SIZE de 53 y un DECIMAL_DIGITS de NULL.<br /><br /> NULL se devuelve para los tipos de datos donde NUM_PREC_RADIX no es aplicable.|  
|NULLABLE (ODBC 1.0)|11|Smallint no NULL|SQL_NO_NULLS si la columna no pudo incluir valores NULL.<br /><br /> SQL_NULLABLE si la columna acepta valores NULL.<br /><br /> SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL.<br /><br /> El valor devuelto para esta columna difiere del valor devuelto para la columna IS_NULLABLE. La columna NULLABLE indica con certeza que una columna puede aceptar valores NULL, pero no puede indicar con certeza que una columna no acepta NULL. La columna IS_NULLABLE indica con certeza que una columna no puede aceptar valores VALORES nulo, pero no puede indicar con certeza que una columna acepta valores NORMALes.|  
|MARCAS (ODBC 1.0)|12|Varchar|Una descripción de la columna.|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|Valor predeterminado de la columna. El valor de esta columna debe interpretarse como una cadena si está entre comillas.<br /><br /> Si se especificó NULL como valor predeterminado, esta columna es la palabra NULL, no entre comillas. Si el valor predeterminado no se puede representar sin truncamiento, esta columna contiene TRUNCATED, sin entrecomillaslas simples. Si no se especificó ningún valor predeterminado, esta columna es NULL.<br /><br /> El valor de COLUMN_DEF se puede utilizar para generar una nueva definición de columna, excepto cuando contiene el valor TRUNCATED.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint no NULL|Tipo de datos SQL, tal como aparece en el campo de registro SQL_DESC_TYPE del IRD. Puede ser un tipo de datos SQL ODBC o un tipo de datos SQL específico del controlador. Esta columna es la misma que la columna DATA_TYPE, excepto para los tipos de datos datetime e interval. Esta columna devuelve el tipo de datos no conciso (como SQL_DATETIME o SQL_INTERVAL), en lugar del tipo de datos conciso (como SQL_TYPE_DATE o SQL_INTERVAL_YEAR_TO_MONTH) para los tipos de datos datetime e interval. Si esta columna devuelve SQL_DATETIME o SQL_INTERVAL, el tipo de datos específico se puede determinar desde la columna SQL_DATETIME_SUB. Para obtener una lista de tipos de datos SQL ODBC válidos, vea Tipos de [datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en apéndice D: tipos de datos. Para obtener información acerca de los tipos de datos SQL específicos del controlador, consulte la documentación del controlador.<br /><br /> Los tipos de datos devueltos para ODBC 3. *x* y ODBC 2. *x* aplicaciones pueden ser diferentes. Para obtener más información, consulte [Compatibilidad con versiones anteriores y Cumplimiento](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)de normas .|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|El código de subtipo para los tipos de datos datetime e interval. Para otros tipos de datos, esta columna devuelve un VALOR NULL. Para obtener más información acerca de los subcódigos datetime e interval, vea "SQL_DESC_DATETIME_INTERVAL_CODE" en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Entero|La longitud máxima en bytes de una columna de tipo de carácter o de tipo de datos binarios. Para todos los demás tipos de datos, esta columna devuelve NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer no NULL|La posición ordinal de la columna en la tabla. La primera columna de la tabla es el número 1.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|"NO" si la columna no incluye los archivos NULL.<br /><br /> "SI" si la columna podría incluir NUL.<br /><br /> Esta columna devuelve una cadena de longitud cero si no se conoce la nulabilidad.<br /><br /> Se siguen las normas ISO para determinar la nulabilidad. Un DBMS que cumpla la norma ISO SQL no puede devolver una cadena vacía.<br /><br /> El valor devuelto para esta columna difiere del valor devuelto para la columna NULLABLE. (Consulte la descripción de la columna NULLABLE.)|  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación declara búferes para el conjunto de resultados devuelto por **SQLColumns**. Llama a **SQLColumns** para devolver un conjunto de resultados que describe cada columna de la tabla EMPLOYEE. A continuación, llama a **SQLBindCol** para enlazar las columnas del conjunto de resultados a los búferes. Por último, la aplicación recupera cada fila de datos con **SQLFetch** y la procesa.  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver privilegios para una columna o columnas|[Función SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Devolver columnas que identifican de forma única una fila o columnas actualizadas automáticamente mediante una transacción|[Función SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|Devolver estadísticas e índices de tablas|[Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Devolver una lista de tablas en un origen de datos|[Función SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
|Devolver privilegios para una tabla o tablas|[Función SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
