---
title: Función SQLSpecialColumns (SQLSpecialColumns) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 826630e1d344322268a2f2638310b3a1e182de6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287175"
---
# <a name="sqlspecialcolumns-function"></a>Función SQLSpecialColumns
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: Grupo abierto  
  
 **Resumen**  
 **SQLSpecialColumns** recupera la siguiente información sobre las columnas dentro de una tabla especificada:  
  
-   Conjunto óptimo de columnas que identifica de forma única una fila de la tabla.  
  
-   Columnas que se actualizan automáticamente cuando una transacción actualiza cualquier valor de la fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *IdentifierType*  
 [Entrada] Tipo de columna que se va a devolver. Debe ser uno de los siguientes valores:   
  
 SQL_BEST_ROWID: devuelve la columna o conjunto óptimo de columnas que, al recuperar valores de la columna o columnas, permite identificar de forma única cualquier fila de la tabla especificada. Una columna puede ser una pseudocolumna diseñada específicamente para este propósito (como en Oracle ROWID o Ingres TID) o la columna o columnas de cualquier índice único de la tabla.  
  
 SQL_ROWVER: devuelve la columna o columnas de la tabla especificada, si existe, que el origen de datos actualiza automáticamente cuando cualquier transacción actualiza cualquier valor de la fila (como en SQLBase ROWID o Sybase TIMESTAMP).  
  
 *CatalogName*  
 [Entrada] Nombre del catálogo de la tabla. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadenas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente, y su caso es significativo. Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nombre de esquema de la tabla. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") denota las tablas que no tienen esquemas. *SchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *SchemaName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Nombre de la tabla. Este argumento no puede ser un puntero nulo. *TableName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *TableName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *Ámbito*  
 [Entrada] Alcance mínimo requerido del rowid. El rowid devuelto puede tener un ámbito mayor. Debe ser una de las siguientes:  
  
 SQL_SCOPE_CURROW: se garantiza que el rowid solo es válido mientras se coloca en esa fila. Una reselección posterior mediante rowid puede no devolver una fila si la fila se actualizó o eliminó por otra transacción.  
  
 SQL_SCOPE_TRANSACTION: se garantiza que el rowid es válido durante la transacción actual.  
  
 SQL_SCOPE_SESSION: se garantiza que el rowid es válido durante la sesión (a través de los límites de la transacción).  
  
 *Admisión de valores NULL*  
 [Entrada] Determina si se deben devolver columnas especiales que pueden tener un valor NULL. Debe ser una de las siguientes:  
  
 SQL_NO_NULLS: excluya las columnas especiales que pueden tener valores NULL. Algunos controladores no pueden admitir SQL_NO_NULLS y estos controladores devolverán un conjunto de resultados vacío si se especificó SQL_NO_NULLS. Las solicitudes deben estar preparadas para este caso y solicitar SQL_NO_NULLS sólo si es absolutamente necesario.  
  
 SQL_NULLABLE: devuelve columnas especiales incluso si pueden tener valores NULL.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSpecialColumns** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLSpecialColumns** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** se había llamado. El Administrador de controladores devuelve este error si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y lo devuelve el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|El *TableName* argumento era un puntero nulo.<br /><br /> El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y el SQL_CATALOG_NAME *InfoType* devuelve que se admiten los nombres de catálogo.<br /><br /> (DM) el atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE y el *SchemaName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función todavía se estaba ejecutando cuando **SQLSpecialColumns** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El valor de uno de los argumentos de longitud era menor que 0 pero no igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos length superó el valor de longitud máxima para el nombre correspondiente. La longitud máxima de cada nombre se puede obtener llamando a **SQLGetInfo** con los valores *InfoType:* SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN o SQL_MAX_TABLE_NAME_LEN.|  
|HY097|Tipo de columna fuera del rango|(DM) se especificó un valor *IdentifierType* no válido.|  
|HY098|Tipo de alcance fuera del rango|(DM) Se especificó un valor *de ámbito* no válido.|  
|HY099|Tipo que acepta valores NULL fuera del rango|(DM) Se especificó un valor *nullable* no válido.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema y el controlador o el origen de datos no admite esquemas.<br /><br /> El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados solicitado. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Cuando el *IdentifierType* argumento se SQL_BEST_ROWID, **SQLSpecialColumns** devuelve la columna o columnas que identifican de forma única cada fila de la tabla. Estas columnas siempre se pueden utilizar en una cláusula *select-list* o **WHERE.** **SQLColumns**, que se usa para devolver una variedad de información sobre las columnas de una tabla, no devuelve necesariamente las columnas que identifican de forma única cada fila o columnas que se actualizan automáticamente cuando una transacción actualiza cualquier valor de la fila. Por ejemplo, **SQLColumns** podría no devolver la pseudocolumna ROWID de Oracle. Esta es la razón por **SQLSpecialColumns** se utiliza para devolver estas columnas. Para obtener más información, consulte [Usos de datos de catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de las funciones de catálogo ODBC, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
 Si no hay columnas que identifiquen de forma única cada fila de la tabla, **SQLSpecialColumns** devuelve un conjunto de filas sin filas; una llamada posterior a **SQLFetch** o **SQLFetchScroll** en la instrucción devuelve SQL_NO_DATA.  
  
 Si los argumentos *IdentifierType*, *Scope*o *Nullable* especifican características que no son compatibles con el origen de datos, **SQLSpecialColumns** devuelve un conjunto de resultados vacío.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, los argumentos *CatalogName*, *SchemaName*y *TableName* se tratan como identificadores, por lo que no se pueden establecer en un puntero nulo en determinadas situaciones. (Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .)  
  
 **SQLSpecialColumns** devuelve los resultados como un conjunto de resultados estándar, ordenado por SCOPE.  
  
 Se ha cambiado el nombre de las columnas siguientes para ODBC *3.x*. Los cambios en el nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones se enlazan por número de columna.  
  
|Columna ODBC 2.0|Columna ODBC *3.x*|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Para determinar la longitud real de la columna COLUMN_NAME, una aplicación puede llamar a **SQLGetInfo** con la opción SQL_MAX_COLUMN_NAME_LEN.  
  
 En la tabla siguiente se enumeran las columnas del conjunto de resultados. El controlador puede definir columnas adicionales más allá de la columna 8 (PSEUDO_COLUMN). Una aplicación debe obtener acceso a columnas específicas del controlador mediante la cuenta regresiva desde el final del conjunto de resultados en lugar de especificar una posición ordinal explícita. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
|Nombre de la columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|SCOPE (ODBC 1.0)|1|Smallint|Alcance real del rowid. Contiene uno de los siguientes valores:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL se devuelve cuando *IdentifierType* se SQL_ROWVER. Para obtener una descripción de cada valor, consulte la descripción de *Scope* en "Syntax", anteriormente en esta sección.|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar no NULL|Nombre de la columna. El controlador devuelve una cadena vacía para una columna que no tiene un nombre.|  
|DATA_TYPE (ODBC 1.0)|3|Smallint no NULL|Tipo de datos SQL. Puede ser un tipo de datos SQL ODBC o un tipo de datos SQL específico del controlador. Para obtener una lista de tipos de datos SQL ODBC válidos, vea [Tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md). Para obtener información acerca de los tipos de datos SQL específicos del controlador, consulte la documentación del controlador.|  
|TYPE_NAME (ODBC 1.0)|4|Varchar no NULL|Nombre de tipo de datos dependiente del origen de datos; por ejemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" o "CHAR ( ) FOR BIT DATA".|  
|COLUMN_SIZE (ODBC 1.0)|5|Entero|El tamaño de la columna en el origen de datos. Para obtener más información sobre el tamaño de columna, vea Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)de visualización .|  
|BUFFER_LENGTH (ODBC 1.0)|6|Entero|La longitud en bytes de datos transferidos en una operación **SQLGetData** o **SQLFetch** si se especifica SQL_C_DEFAULT. Para los datos numéricos, este tamaño puede ser diferente del tamaño de los datos almacenados en el origen de datos. Este valor es el mismo que la columna COLUMN_SIZE para datos binarios o de caracteres. Para obtener más información, consulte [Tamaño de columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)de visualización .|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|Los dígitos decimales de la columna en el origen de datos. NULL se devuelve para los tipos de datos donde los dígitos decimales no son aplicables. Para obtener más información sobre los dígitos decimales, consulte [Tamaño de columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)de visualización .|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|Indica si la columna es una pseudocolumna, como Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Nota:** Para una interoperabilidad máxima, no se deben citar pseudocolumnas con el carácter de comillas de identificador devuelto por **SQLGetInfo**.|  
  
 Después de que la aplicación recupere valores para SQL_BEST_ROWID, la aplicación puede usar estos valores para volver a seleccionar esa fila dentro del ámbito definido. Se garantiza que la instrucción **SELECT** no devolverá filas ni una fila.  
  
 Si una aplicación vuelve a seleccionar una fila basada en la columna o columnas rowid y no se encuentra la fila, la aplicación puede suponer que se eliminó la fila o se modificaron las columnas rowid. Lo contrario no es cierto: incluso si el rowid no ha cambiado, las otras columnas de la fila pueden haber cambiado.  
  
 Las columnas devueltas para el tipo de columna SQL_BEST_ROWID son útiles para las aplicaciones que necesitan desplazarse hacia delante y hacia atrás dentro de un conjunto de resultados para recuperar los datos más recientes de un conjunto de filas. Se garantiza que la columna o columnas del rowid no cambiará mientras se coloca en esa fila.  
  
 La columna o columnas del rowid pueden seguir siendo válidas incluso cuando el cursor no se coloca en la fila; la aplicación puede determinar esto comprobando la columna SCOPE en el conjunto de resultados.  
  
 Las columnas devueltas para el tipo de columna SQL_ROWVER son útiles para las aplicaciones que necesitan la capacidad de comprobar si las columnas de una fila determinada se han actualizado mientras se ha vuelto a seleccionar la fila mediante el rowid. Por ejemplo, después de volver a seleccionar una fila mediante rowid, la aplicación puede comparar los valores anteriores de las columnas SQL_ROWVER con los que acaba de capturar. Si el valor de una columna SQL_ROWVER difiere del valor anterior, la aplicación puede alertar al usuario de que los datos de la pantalla han cambiado.  
  
## <a name="code-example"></a>Ejemplo de código  
 Para obtener un ejemplo de código de una función similar, vea [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver las columnas en una tabla o tablas|[Función SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver las columnas de una clave principal|[Función SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
