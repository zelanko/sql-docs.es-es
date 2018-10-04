---
title: Función SQLSpecialColumns | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52ad6bc3fc84b0d50675b4e0a4e7bb44a6ded1c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849363"
---
# <a name="sqlspecialcolumns-function"></a>Función SQLSpecialColumns
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: Abrir grupo  
  
 **Resumen**  
 **SQLSpecialColumns** recupera la información siguiente acerca de las columnas dentro de una tabla especificada:  
  
-   El conjunto óptimo de columnas que identifica de forma única una fila en la tabla.  
  
-   Columnas que se actualizan automáticamente cuando una transacción actualiza cualquier valor de la fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
  
 SQL_BEST_ROWID: Devuelve la columna óptima o el conjunto de columnas, al recuperar valores de la columna o columnas, que permite que cualquier fila de la tabla especificada pueda identificarse de forma única. Una columna puede ser cualquier una pseudocolumna diseñada específicamente para este propósito (como en Oracle ROWID o TID Ingres) o la columna o columnas de cualquier índice único para la tabla.  
  
 SQL_ROWVER: Devuelve la columna o columnas de la tabla especificada, si procede, que se actualizan automáticamente por el origen de datos cuando se actualiza algún valor en la fila de una transacción (como en SQLBase ROWID o Sybase TIMESTAMP).  
  
 *CatalogName*  
 [Entrada] Nombre del catálogo de la tabla. Si un controlador es compatible con los catálogos para algunas tablas pero no para otros factores, como cuando el controlador recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tengan los catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos en funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nombre de esquema para la tabla. Si un controlador es compatible con los esquemas para algunas tablas pero no para otros factores, como cuando el controlador recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene esquemas. *SchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *SchemaName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Nombre de tabla. Este argumento no puede ser un puntero nulo. *TableName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *TableName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *Ámbito*  
 [Entrada] Ámbito mínimo necesario del rowid. Rowid devuelto puede ser un ámbito mayor. Debe ser una de las siguientes:  
  
 SQL_SCOPE_CURROW: Se garantiza que el rowid sea válido solo mientras se coloca en esa fila. Una nueva selección posterior mediante rowid no puede devolver una fila si la fila actualizada o eliminada por otra transacción.  
  
 SQL_SCOPE_TRANSACTION: Se garantiza que el rowid sea válido para la duración de la transacción actual.  
  
 SQL_SCOPE_SESSION: Se garantiza que el rowid sea válido para la duración de la sesión (a través de los límites de transacción).  
  
 *Admisión de valores NULL*  
 [Entrada] Determina si se deben devolver columnas especiales que pueden tener un valor NULL. Debe ser una de las siguientes:  
  
 SQL_NO_NULLS: Excluir columnas especiales que pueden tener valores NULL. Algunos controladores no admiten SQL_NO_NULLS y estos controladores devolverá un conjunto si se especificó SQL_NO_NULLS de resultados vacío. Las aplicaciones deben estar preparadas para este caso y solicitud SQL_NO_NULLS solo si es absolutamente necesario.  
  
 SQL_NULLABLE: Devolver columnas especiales incluso si tienen valores NULL.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLSpecialColumns** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSpecialColumns** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** hubiera llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero nulo|El *TableName* argumento era un puntero nulo.<br /><br /> El atributo de instrucción SQL_ATTR_METADATA_ID estuviera establecido en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *InfoType* devuelve que los nombres de catálogo es compatibles.<br /><br /> (DM) se estableció el atributo de instrucción SQL_ATTR_METADATA_ID en SQL_TRUE y el *SchemaName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función aún estaba ejecutando cuando **SQLSpecialColumns** llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud era menor que 0 pero no es igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud supera el valor de longitud máxima para el nombre correspondiente. La longitud máxima de cada nombre se puede obtener mediante una llamada a **SQLGetInfo** con el *InfoType* valores: SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN o SQL_MAX_TABLE_NAME_LEN.|  
|HY097|Tipo de columna fuera del intervalo|(DM) no es válido *IdentifierType* se especificó un valor.|  
|HY098|Tipo de ámbito fuera del intervalo|(DM) no es válido *ámbito* se especificó un valor.|  
|HY099|Tipo que acepta valores NULL fuera del intervalo|(DM) no es válido *Nullable* se especificó un valor.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo, y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema y el controlador o el origen de datos no admite esquemas.<br /><br /> La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y se ha establecido el atributo de instrucción SQL_ATTR_CURSOR_TYPE a un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes del origen de datos devuelve el conjunto de resultados solicitada. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Cuando el *IdentifierType* argumento es SQL_BEST_ROWID, **SQLSpecialColumns** devuelve la columna o columnas que identifican de forma única cada fila de la tabla. Estas columnas siempre se pueden usar en un *lista de selección* o **donde** cláusula. **SQLColumns**, que se usa para devolver una gran variedad de información en las columnas de una tabla, no necesariamente devolver las columnas que identifican de forma única cada fila o las columnas que se actualizan automáticamente cuando cualquier valor de la fila se actualiza mediante un transacción. Por ejemplo, **SQLColumns** podrían no devolverse con Oracle pseudocolumna ROWID. Por ello **SQLSpecialColumns** se usa para devolver estas columnas. Para obtener más información, consulte [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Si no hay columnas que identifican de forma única cada fila de la tabla, **SQLSpecialColumns** devuelve un conjunto de filas con ninguna fila; una llamada subsiguiente a **SQLFetch** o **SQLFetchScroll**en la instrucción devuelve SQL_NO_DATA.  
  
 Si el *IdentifierType*, *ámbito*, o *Nullable* argumentos especifican las características que no son compatibles con el origen de datos, **SQLSpecialColumns**  devuelve un conjunto de resultados vacío.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, el *CatalogName*, *SchemaName*, y *TableName* argumentos se tratan como identificadores, por lo que se no se puede establecer en un puntero nulo en determinadas situaciones. (Para obtener más información, consulte [argumentos en funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).)  
  
 **SQLSpecialColumns** devuelve los resultados como un conjunto de resultados estándar, ordenado por ámbito.  
  
 Las columnas siguientes se han cambiado para ODBC 3 *.x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque el enlace de aplicaciones por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3 *.x* columna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Para determinar la longitud real de la columna COLUMN_NAME, una aplicación puede llamar a **SQLGetInfo** con la opción SQL_MAX_COLUMN_NAME_LEN.  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. Las columnas adicionales más allá de la columna 8 (PSEUDO_COLUMN) pueden definirse mediante el controlador. Una aplicación debe tener acceso a las columnas específicas del controlador mediante la cuenta atrás desde el final del conjunto de resultados, en lugar de especificar una posición ordinal explícita. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|ÁMBITO (ODBC 1.0)|1|Smallint|Ámbito real del rowid. Contiene uno de los siguientes valores:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> Se devuelve NULL si *IdentifierType* es SQL_ROWVER. Para obtener una descripción de cada valor, vea la descripción de *ámbito* en "Sintaxis", anteriormente en esta sección.|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar no es NULL|Nombre de columna. El controlador devuelve una cadena vacía para una columna que no tiene un nombre.|  
|DATA_TYPE (ODBC 1.0)|3|Smallint no NULL|Tipo de datos SQL. Esto puede ser un tipo de datos SQL de ODBC o un tipo de datos SQL específicas del controlador. Para obtener una lista de tipos de datos ODBC SQL válidos, vea [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md). Para obtener información acerca de los tipos de datos SQL específicas del controlador, consulte la documentación del controlador.|  
|TYPE_NAME (ODBC 1.0)|4|Varchar no es NULL|Nombre de tipo de datos depende del origen de datos; "Por ejemplo,"CHAR", VARCHAR", "MONEY", "LONG VARBINARY" o "CHAR () para datos de bits".|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|El tamaño de la columna del origen de datos. Para obtener más información sobre el tamaño de la columna, vea [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|La longitud en bytes de datos transferidos en un **SQLGetData** o **SQLFetch** operación si se especifica SQL_C_DEFAULT. Para los datos numéricos, este tamaño puede ser diferente que el tamaño de los datos almacenados en el origen de datos. Este valor es igual que la columna COLUMN_SIZE para caracteres o datos binarios. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|Los dígitos decimales de la columna del origen de datos. Se devuelve NULL para los tipos de datos que no son aplicables los dígitos decimales. Para obtener más información relativa a los dígitos decimales, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|Indica si la columna es una pseudocolumna, como Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Nota:** para obtener la máxima interoperatividad, pseudocolumnas no deben ir entrecomillados con el carácter de comilla de identificador devuelto por **SQLGetInfo**.|  
  
 Una vez que la aplicación recupera los valores para SQL_BEST_ROWID, la aplicación puede utilizar estos valores para volver a seleccionar esa fila dentro del ámbito definido. El **seleccione** instrucción se garantiza para devolver ninguna fila o una fila.  
  
 Si una aplicación selecciona una fila basándose en la columna rowid o columnas y no se encuentra la fila, la aplicación puede suponer que la fila se eliminó o se han modificado las columnas rowid. Lo contrario no es cierto: incluso si no ha cambiado el rowid, es posible que han cambiado las demás columnas de la fila.  
  
 Columnas devueltas para el tipo de columna SQL_BEST_ROWID son útiles para las aplicaciones que tenga que desplazarse hacia delante y atrás dentro de un conjunto de resultados para recuperar los datos más recientes de un conjunto de filas. La columna o columnas del rowid se garantiza que no cambie mientras se coloca en esa fila.  
  
 La columna o columnas del rowid es posible que siguen siendo válidas aunque no está situado el cursor en la fila; la aplicación puede determinarlo mediante la comprobación de la columna de ámbito en el conjunto de resultados.  
  
 Columnas devueltas para el tipo de columna son útiles para las aplicaciones que necesitan la capacidad de comprobar si se han actualizado las columnas en una fila determinada mientras se desactivan las filas usando rowid SQL_ROWVER. Por ejemplo, después de volver a seleccionar una fila usando rowid, la aplicación puede comparar los valores anteriores en las columnas SQL_ROWVER a los que simplemente capturados. Si el valor de una columna SQL_ROWVER es diferente del valor anterior, la aplicación puede alertar al usuario que ha cambiado los datos en la pantalla.  
  
## <a name="code-example"></a>Ejemplo de código  
 Para obtener un ejemplo de código de una función similar, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver las columnas de una o varias tablas|[Función SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver las columnas de una clave principal|[Función SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
