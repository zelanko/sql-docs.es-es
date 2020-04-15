---
title: Función SQLTables (SQLTables) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae52e6431679ed0f260e6885090ac38363b4ef3d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287135"
---
# <a name="sqltables-function"></a>Función SQLTables
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: Grupo abierto  
  
 **Resumen**  
 **SQLTables** devuelve la lista de nombres de tabla, catálogo o esquema y tipos de tabla, almacenados en un origen de datos específico. El controlador devuelve la información como un conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLTables(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      TableType,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción para los resultados recuperados.  
  
 *CatalogName*  
 [Entrada] Nombre del catálogo. El *Argumento CatalogName* acepta patrones de búsqueda si se SQL_OV_ODBC3 el atributo de entorno SQL_ODBC_VERSION; no acepta patrones de búsqueda si se establece SQL_OV_ODBC2. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando un controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen catálogos.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *CatalogName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo. Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de esquema. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen esquemas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de tabla.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *TableName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *TableType*  
 [Entrada] Lista de tipos de tabla que se quieren hacer coincidir.  
  
 Observe que el atributo de instrucción SQL_ATTR_METADATA_ID no tiene ningún efecto en el *TableType* argumento. *TableType* es un argumento de lista de valores, independientemente de la configuración de SQL_ATTR_METADATA_ID.  
  
 *NameLength4*  
 [Entrada] Longitud en caracteres de **TableType*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLTables** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLTables** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
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
|HY009|Uso no válido de puntero nulo|El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y el SQL_CATALOG_NAME *InfoType* devuelve que se admiten los nombres de catálogo.<br /><br /> (DM) el atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE y el *SchemaName* o *TableName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando sqlTables se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El valor de uno de los argumentos de longitud era menor que 0 pero no igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud de nombre superó el valor de longitud máxima para el nombre correspondiente.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema y el controlador o el origen de datos no admite esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el nombre del catálogo, el esquema de tabla o el nombre de tabla, y el origen de datos no admite patrones de búsqueda para uno o varios de esos argumentos.<br /><br /> El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados solicitado. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLTables** enumera todas las tablas del intervalo solicitado. Un usuario puede o no tener privilegios SELECT para cualquiera de estas tablas. Para comprobar la accesibilidad, una aplicación puede:  
  
-   Llame a **SQLGetInfo** y compruebe el tipo de información SQL_ACCESSIBLE_TABLES.  
  
-   Llame a **SQLTablePrivileges** para comprobar los privilegios de cada tabla.  
  
 De lo contrario, la aplicación debe poder controlar una situación en la que el usuario selecciona una tabla para la que no se conceden privilegios **SELECT.**  
  
 Los argumentos *SchemaName* y *TableName* aceptan patrones de búsqueda. El *Argumento CatalogName* acepta patrones de búsqueda si se SQL_OV_ODBC3 el atributo de entorno SQL_ODBC_VERSION; no acepta patrones de búsqueda si se establece SQL_OV_ODBC2. Si se establece SQL_OV_ODBC3, un controlador ODBC 3 *.x* requerirá que los caracteres comodín del argumento *CatalogName* se traten literalmente. Para obtener más información acerca de los patrones de búsqueda válidos, vea Argumentos de valor de [patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de las funciones de catálogo ODBC, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
 Para admitir la enumeración de catálogos, esquemas y tipos de tabla, se definen las siguientes semánticas especiales para los argumentos *CatalogName*, *SchemaName*, *TableName*y *TableType* de **SQLTables:**  
  
-   Si *CatalogName* es SQL_ALL_CATALOGS y *SchemaName* y *TableName* son cadenas vacías, el conjunto de resultados contiene una lista de catálogos válidos para el origen de datos. (Todas las columnas excepto la columna TABLE_CAT contienen NUL.)  
  
-   Si *SchemaName* es SQL_ALL_SCHEMAS y *CatalogName* y *TableName* son cadenas vacías, el conjunto de resultados contiene una lista de esquemas válidos para el origen de datos. (Todas las columnas excepto la columna TABLE_SCHEM contienen NUL.)  
  
-   Si *TableType* es SQL_ALL_TABLE_TYPES y *CatalogName*, *SchemaName*y *TableName* son cadenas vacías, el conjunto de resultados contiene una lista de tipos de tabla válidos para el origen de datos. (Todas las columnas excepto la columna TABLE_TYPE contienen NUL.)  
  
 Si *TableType* no es una cadena vacía, debe contener una lista de valores separados por comas para los tipos de interés; cada valor puede incluirse entre comillas simples (') o sin comillas, por ejemplo, 'TABLE', 'VIEW' o TABLE, VIEW. Una aplicación siempre debe especificar el tipo de tabla en mayúsculas; el controlador debe convertir el tipo de tabla en cualquier caso que necesite el origen de datos. Si el origen de datos no admite un tipo de tabla especificado, **SQLTables** no devuelve ningún resultado para ese tipo.  
  
 **SQLTables** devuelve los resultados como un conjunto de resultados estándar, ordenado por TABLE_TYPE, TABLE_CAT, TABLE_SCHEM y TABLE_NAME. Para obtener información sobre cómo se puede usar esta información, vea [Usos de datos de catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar las longitudes reales de las columnas TABLE_CAT, TABLE_SCHEM y TABLE_NAME, una aplicación puede llamar a **SQLGetInfo** con los tipos de información SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN y SQL_MAX_TABLE_NAME_LEN.  
  
 Se ha cambiado el nombre de las columnas siguientes para ODBC 3 *.x*. Los cambios en el nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones se enlazan por número de columna.  
  
|Columna ODBC 2.0|Columna ODBC 3 *.x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 En la tabla siguiente se enumeran las columnas del conjunto de resultados. El controlador puede definir columnas adicionales más allá de la columna 5 (REMARKS). Una aplicación debe obtener acceso a columnas específicas del controlador mediante la cuenta regresiva desde el final del conjunto de resultados en lugar de especificar una posición ordinal explícita. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
|Nombre de la columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nombre del catálogo; NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellas tablas que no tienen catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema; NULL si no es aplicable al origen de datos. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tienen esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|Nombre de la tabla.|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|Nombre de tipo de tabla; uno de los siguientes: "TABLE", "VIEW", "SYSTEM TABLE", "GLOBAL TEMPORARY", "LOCAL TEMPORARY", "ALIAS", "SYNONYM" o un nombre de tipo específico del origen de datos.<br /><br /> Los significados de "ALIAS" y "SYNONYM" son específicos del controlador.|  
|MARCAS (ODBC 1.0)|5|Varchar|Una descripción de la tabla.|  
  
## <a name="example"></a>Ejemplo  
 El siguiente código de ejemplo no libera identificadores y conexiones. Vea [SQLFreeHandle (función)](../../../odbc/reference/syntax/sqlfreehandle-function.md) y [SQLFreeStmt Function (Función)](../../../odbc/reference/syntax/sqlfreestmt-function.md) para obtener ejemplos de código en identificadores e instrucciones libres.  
  
```cpp  
// SQLTables.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
// simple helper functions  
int MySQLSuccess(SQLRETURN rc) {  
   return (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO);  
}  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printCatalog(const struct DataBinding* catalogResult) {  
   if (catalogResult[0].StrLen_or_Ind != SQL_NULL_DATA)   
      printf("Catalog Name = %s\n", (char *)catalogResult[0].TargetValuePtr);  
}  
  
// remember to disconnect and free memory, and free statements and handles  
int main() {  
   int bufferSize = 1024, i, numCols = 5;  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   wchar_t* dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   wchar_t* userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR*)"Driver={SQL Server}", SQL_NTS, (SQLCHAR*)connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
  
   bufferSize = 1024;  
  
   // allocate memory for the binding  
   // free this memory when done  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // setup the binding (can be used even if the statement is closed by closeStatementHandle)  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   // all catalogs query  
   printf( "A list of names of all catalogs\n" );  
   retCode = SQLTables( hstmt, (SQLCHAR*)SQL_ALL_CATALOGS, SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS );  
   for ( retCode = SQLFetch(hstmt) ;  MySQLSuccess(retCode) ; retCode = SQLFetch(hstmt) )  
      printCatalog( catalogResult );  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver privilegios para una columna o columnas|[Función SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Devolver las columnas en una tabla o tablas|[Función SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver estadísticas e índices de tablas|[Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Devolver privilegios para una tabla o tablas|[Función SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
