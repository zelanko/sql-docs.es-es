---
title: Función SQLColumns | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51b14014853e0ccb91293097fd3aa81c1edcb2ae
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207744"
---
# <a name="sqlcolumns-function"></a>Función SQLColumns
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: Abrir grupo  
  
 **Resumen**  
 **SQLColumns** devuelve la lista de nombres de columna en las tablas especificadas. El controlador devuelve esta información como un conjunto de resultados en el objeto *StatementHandle*.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Nombre del catálogo. Si un controlador es compatible con los catálogos para algunas tablas pero no para otros factores, como cuando el controlador recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tengan los catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadena.  
  
> [!NOTE]  
>  Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos en funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de esquema. Si un controlador es compatible con los esquemas para algunas tablas pero no para otros factores, como cuando el controlador recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene esquemas.  
  
> [!NOTE]  
>  Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de tabla.  
  
> [!NOTE]  
>  Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *TableName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *ColumnName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de columna.  
  
> [!NOTE]  
>  Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *ColumnName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *ColumnName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength4*  
 [Entrada] Longitud en caracteres de **ColumnName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLColumns** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLColumns** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** hubiera llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle* pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero nulo|El atributo de instrucción SQL_ATTR_METADATA_ID estuviera establecido en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *InfoType* devuelve que los nombres de catálogo es compatibles.<br /><br /> (DM) se estableció el atributo de instrucción SQL_ATTR_METADATA_ID en SQL_TRUE y el *SchemaName*, *TableName*, o *ColumnName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLColumns** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud de nombre era menor que 0 pero no es igual a SQL_NTS.|  
|||El valor de uno de los argumentos de longitud del nombre supera el valor de longitud máxima para el catálogo correspondiente o el nombre. La longitud máxima de cada nombre del catálogo o se puede obtener mediante una llamada a **SQLGetInfo** con el *InfoType* valores. (Vea "Comentarios".)|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un nombre de catálogo y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un nombre de esquema y el controlador o el origen de datos no admite esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el nombre de esquema, nombre de tabla o nombre de columna y el origen de datos no admite patrones de búsqueda para uno o varios de estos argumentos.<br /><br /> La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y se ha establecido el atributo de instrucción SQL_ATTR_CURSOR_TYPE a un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Esta función normalmente se usa antes de ejecutar la instrucción para recuperar información acerca de las columnas de una o varias tablas de catálogo del origen de datos. **SQLColumns** puede usarse para recuperar datos para todos los tipos de elementos devueltos por **SQLTables**. Además de las tablas bases, esto puede incluir (pero no está limitado a) las vistas, sinónimos, las tablas del sistema y así sucesivamente. Por el contrario, las funciones **SQLColAttribute** y **SQLDescribeCol** describen las columnas de un conjunto de resultados y la función **SQLNumResultCols** devuelve el número de columnas de un conjunto de resultados. Para obtener más información, consulte [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLColumns** devuelve los resultados como un conjunto de resultados estándar, ordenado por TABLE_CAT, según TABLE_SCHEM, TABLE_NAME y ORDINAL_POSITION.  
  
> [!NOTE]  
>  Cuando una aplicación funciona con un ODBC 2. *x* ninguna columna ORDINAL_POSITION de controlador, se devuelve en el conjunto de resultados. Como resultado, cuando se trabaja con ODBC 2. *x* controladores, el orden de las columnas de la lista de columnas devueltas por **SQLColumns** no es necesariamente el mismo que el orden de las columnas devuelto cuando la aplicación realiza una instrucción SELECT en todas las columnas de esa tabla.  
  
> [!NOTE]  
>  **SQLColumns** no puede devolver todas las columnas. Por ejemplo, un controlador no podría devolver información acerca de las pseudocolumnas, como Oracle ROWID. Las aplicaciones pueden utilizar cualquier columna válida, si se devuelve de forma **SQLColumns**.  
>   
>  Algunas columnas que pueden ser devueltos por **SQLStatistics** no se devuelven por **SQLColumns**. Por ejemplo, **SQLColumns** no devuelve las columnas en un índice creado a través de una expresión o filtro, como el salario + beneficios o DEPT = 0012.  
  
 Las longitudes de las columnas VARCHAR no se muestran en la tabla. las longitudes reales dependen del origen de datos. Para determinar las longitudes de las columnas TABLE_CAT, según TABLE_SCHEM, TABLE_NAME y COLUMN_NAME reales, una aplicación puede llamar a **SQLGetInfo** con el SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, y las opciones de SQL_MAX_COLUMN_NAME_LEN.  
  
 Las columnas siguientes se han cambiado para ODBC 3. *x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque el enlace de aplicaciones por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3. *x* columna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Las columnas siguientes se han agregado al conjunto de resultados devuelto por **SQLColumns** para ODBC 3. *x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. Las columnas adicionales más allá de la columna 18 (IS_NULLABLE) pueden definirse mediante el controlador. Una aplicación debe tener acceso a columnas específicas del controlador mediante la cuenta atrás desde el final del conjunto en lugar de especificar una posición ordinal explícita de resultados. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|columna<br /><br /> number|Tipo de datos|Comentarios|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nombre del catálogo; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con los catálogos para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tengan los catálogos.|  
|SEGÚN TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con los esquemas para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tiene esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar no es NULL|Nombre de la tabla.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar no es NULL|Nombre de columna. El controlador devuelve una cadena vacía para una columna que no tiene un nombre.|  
|DATA_TYPE (ODBC 1.0)|5|Smallint no NULL|Tipo de datos SQL. Esto puede ser un tipo de datos SQL de ODBC o un tipo de datos SQL específicas del controlador. Para los tipos de datos datetime e interval, esta columna devuelve el tipo de datos conciso (por ejemplo, SQL_TYPE_DATE o SQL_INTERVAL_YEAR_TO_MONTH, en lugar del tipo de datos nonconcise como SQL_DATETIME o SQL_INTERVAL). Para obtener una lista de tipos de datos ODBC SQL válidos, vea [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en el apéndice D: Tipos de datos. Para obtener información acerca de los tipos de datos SQL específicas del controlador, consulte la documentación del controlador.<br /><br /> Los tipos de datos devueltos para ODBC 3. *x* y ODBC 2. *x* las aplicaciones pueden ser diferentes. Para obtener más información, consulte [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|TYPE_NAME (ODBC 1.0)|6|Varchar no es NULL|Nombre de tipo de datos dependiente del origen de datos; "Por ejemplo,"CHAR", VARCHAR", "MONEY", "Largo VARBINAR" o "CHAR () para datos de bits".|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|Si DATA_TYPE es SQL_CHAR o SQL_VARCHAR, esta columna contiene la longitud máxima en caracteres de la columna. Para los tipos de datos de fecha y hora, este es el número total de caracteres necesarios para mostrar el valor cuando se convierte en caracteres. Para los tipos de datos numéricos, este es el número total de dígitos o el número total de bits que se permiten en la columna, según la columna NUM_PREC_RADIX. Para los tipos de datos de intervalo, es el número de caracteres en la representación de caracteres del intervalo de literal (tal como se define por el intervalo de precisión inicial, vea [longitud del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md) en el apéndice D: Tipos de datos). Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos.|  
|BUFFER_LENGTH (ODBC 1.0)|8|Integer|La longitud en bytes de datos se transfiere en una operación SQLGetData, SQLFetch o SQLFetchScroll si se especifica SQL_C_DEFAULT. Para los datos numéricos, este tamaño puede diferir el tamaño de los datos almacenados en el origen de datos. Este valor puede diferir de la columna COLUMN_SIZE para datos de caracteres. Para obtener más información acerca de la longitud, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|El número total de dígitos significativos a la derecha del separador decimal. SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP, esta columna contiene el número de dígitos en el componente de fracciones de segundo. Para otros tipos de datos, se trata de los dígitos decimales de la columna del origen de datos. Tipos de datos de intervalo que contienen un componente de tiempo, esta columna contiene el número de dígitos a la derecha del separador decimal (fracciones de segundo). Para los tipos de datos de intervalo que no contienen un componente de tiempo, esta columna es 0. Para obtener más información acerca de dígitos decimales, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos. Se devuelve NULL para los tipos de datos donde DECIMAL_DIGITS no es aplicable.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|Para los tipos de datos numéricos, 10 ó 2. Si es 10, los valores COLUMN_SIZE y DECIMAL_DIGITS proporcionan el número de dígitos decimales que se permiten para la columna. Por ejemplo, una columna DECIMAL(12,5) devolvería un NUM_PREC_RADIX de 10, un valor de COLUMN_SIZE de 12 y un DECIMAL_DIGITS de 5; una columna de tipo FLOAT podría devolver un NUM_PREC_RADIX de 10, un valor de COLUMN_SIZE de 15 y DECIMAL_DIGITS NULL.<br /><br /> Si es 2, los valores COLUMN_SIZE y DECIMAL_DIGITS proporcionan el número de bits que se permiten en la columna. Por ejemplo, una columna de tipo FLOAT podría devolver una base de 2, un valor de COLUMN_SIZE 53 y DECIMAL_DIGITS NULL.<br /><br /> Se devuelve NULL para los tipos de datos donde NUM_PREC_RADIX no es aplicable.|  
|QUE ACEPTA VALORES NULL (ODBC 1.0)|11|Smallint no NULL|SQL_NO_NULLS si la columna no puede incluir valores NULL.<br /><br /> SQL_NULLABLE si la columna acepta valores NULL.<br /><br /> SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL.<br /><br /> El valor devuelto para esta columna es diferente del valor devuelto para la columna IS_NULLABLE. Indica la columna que acepta valores NULL con certeza que una columna puede aceptar valores NULL, pero no se indica con certeza que una columna no acepta valores NULL. Indica la columna IS_NULLABLE con certeza que una columna no puede aceptar valores NULL, pero no se indica con certeza que una columna acepta valores NULL.|  
|COMENTARIOS (ODBC 1.0)|12|Varchar|Descripción de la columna.|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|Valor predeterminado de la columna. El valor de esta columna debe interpretarse como una cadena si se incluye entre comillas.<br /><br /> Si se especifica NULL como valor predeterminado, esta columna es la palabra NULL, que no se incluyen entre comillas. Si el valor predeterminado no se puede representar sin truncamiento, esta columna contiene TRUNCADO, sin incluir las comillas simples. Si se ha especificado ningún valor predeterminado, esta columna es NULL.<br /><br /> El valor de COLUMN_DEF puede utilizarse para generar una nueva definición de columna, excepto cuando no contiene el valor TRUNCADO.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint no NULL|Tipo de datos SQL, tal como aparece en el campo SQL_DESC_TYPE registro IRD. Esto puede ser un tipo de datos SQL de ODBC o un tipo de datos SQL específicas del controlador. Esta columna es igual que la columna DATA_TYPE, salvo los tipos de datos datetime e interval. Esta columna devuelve el tipo de datos nonconcise (por ejemplo, SQL_DATETIME o SQL_INTERVAL), en lugar de concisa tipo de datos (por ejemplo, SQL_TYPE_DATE o SQL_INTERVAL_YEAR_TO_MONTH) para datetime y tipos de datos interval. Si esta columna devuelve SQL_DATETIME o SQL_INTERVAL, se puede determinar el tipo de datos específico de la columna SQL_DATETIME_SUB. Para obtener una lista de tipos de datos ODBC SQL válidos, vea [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en el apéndice D: Tipos de datos. Para obtener información acerca de los tipos de datos SQL específicas del controlador, consulte la documentación del controlador.<br /><br /> Los tipos de datos devueltos para ODBC 3. *x* y ODBC 2. *x* las aplicaciones pueden ser diferentes. Para obtener más información, consulte [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|El código de subtipo para los tipos de datos datetime e interval. Para otros tipos de datos, esta columna devuelve un valor NULL. Para obtener más información sobre subcódigos datetime e interval, vea "SQL_DESC_DATETIME_INTERVAL_CODE" en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|Columna de tipo de la longitud máxima en bytes de un carácter o datos binarios. Para todos los demás tipos de datos, esta columna devuelve NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer no NULL|La posición ordinal de la columna en la tabla. La primera columna de la tabla es el número 1.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|"NO" si la columna no incluye los valores NULL.<br /><br /> "Sí" si la columna puede incluir valores NULL.<br /><br /> Esta columna devuelve una cadena de longitud cero si no se conoce la nulabilidad.<br /><br /> Se siguen las normas ISO para determinar la nulabilidad. Un DBMS que cumpla la norma ISO SQL no puede devolver una cadena vacía.<br /><br /> El valor devuelto para esta columna es diferente del valor devuelto para la columna que acepta valores NULL. (Vea la descripción de la columna que acepta valores NULL).|  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación declara los búferes del conjunto de resultados devuelto por **SQLColumns**. Llama a **SQLColumns** para devolver un conjunto de resultados que se describe cada columna en la tabla EMPLOYEE. A continuación, llama **SQLBindCol** para enlazar las columnas en el conjunto de resultados a los búferes. Por último, la aplicación recopila cada fila de datos con **SQLFetch** y lo procesa.  
  
```  
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
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devuelve los privilegios para una o varias columnas|[Función SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recopilación de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Devolver las columnas que identifican de forma única una fila o una transacción actualiza automáticamente|[Función SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|Devolver estadísticas de tablas e índices|[Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Devuelve una lista de tablas en un origen de datos|[Función SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
|Devuelve los privilegios para una o varias tablas|[Función SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
