---
title: Función SQLTables | Documentos de Microsoft
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
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca0e5379079c735b7dd0f5b6770818e5f930f51d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqltables-function"></a>Función SQLTables
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: Abrir grupo  
  
 **Resumen**  
 **SQLTables** devuelve la lista de nombres de esquema, catálogo o tabla y tipos de tabla, almacenados en un origen de datos específico. El controlador devuelve la información como un conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Identificador de instrucción para recupera resultados.  
  
 *CatalogName*  
 [Entrada] Nombre del catálogo. El *CatalogName* argumento acepta patrones de búsqueda si el atributo de entorno de SQL_ODBC_VERSION es SQL_OV_ODBC3; no acepta patrones de búsqueda, si se establece SQL_OV_ODBC2. Si un controlador admite catálogos para algunas tablas pero no para otros, como cuando un controlador recupera los datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene catálogos.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *CatalogName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *schemaName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de esquema. Si un controlador es compatible con esquemas para algunas tablas pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tengan esquemas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de tabla.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *TableName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *TableType*  
 [Entrada] Lista de tipos de tabla para que coincida con.  
  
 Tenga en cuenta que el atributo de instrucción de SQL_ATTR_METADATA_ID no tiene ningún efecto sobre la *TableType* argumento. *TableType* es un argumento de la lista de valor, independientemente de la configuración de SQL_ATTR_METADATA_ID.  
  
 *NameLength4*  
 [Entrada] Longitud en caracteres de **TableType*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLTables** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLTables** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** si se hubiese llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** si no se hubiese llamado.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*. A continuación, se llama a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero null|El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *tipo de información* devuelve que los nombres de catálogo se admite.<br /><br /> (DM) se estableció el atributo de instrucción de SQL_ATTR_METADATA_ID en SQL_TRUE y el *SchemaName* o *TableName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún se estaba ejecutando cuando se llamó a SQLTables.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud era menor que 0 pero no es igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud de nombre supera el valor de longitud máxima para el nombre correspondiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo y del origen de datos o el controlador no admite catálogos.<br /><br /> Se especificó un esquema y el controlador o el origen de datos no admite los esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el nombre del catálogo, esquema de tabla o nombre de la tabla y el origen de datos no admite patrones de búsqueda para uno o varios de esos argumentos.<br /><br /> La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta expirado antes el origen de datos que devuelve el conjunto de resultados solicitada. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLTables** enumera todas las tablas en el intervalo solicitado. Un usuario puede o no puede tener determinados privilegios a cualquiera de estas tablas. Para comprobar la accesibilidad, una aplicación hacer lo siguiente:  
  
-   Llame a **SQLGetInfo** y comprobar el tipo de información de SQL_ACCESSIBLE_TABLES.  
  
-   Llame a **SQLTablePrivileges** para comprobar los privilegios para cada tabla.  
  
 En caso contrario, la aplicación debe ser capaz de controlar una situación donde el usuario selecciona una tabla para la que **seleccione** no se conceden los privilegios.  
  
 El *SchemaName* y *TableName* argumentos aceptan patrones de búsqueda. El *CatalogName* argumento acepta patrones de búsqueda si el atributo de entorno de SQL_ODBC_VERSION es SQL_OV_ODBC3; no acepta patrones de búsqueda, si se establece SQL_OV_ODBC2. Si se establece SQL_OV_ODBC3, una aplicación ODBC 3 *.x* controlador requerirá que comodín los caracteres de la *CatalogName* argumento convertirse para ser tratados literalmente. Para obtener más información sobre los patrones de búsqueda válidos, consulte [argumentos de valor de patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Para permitir la enumeración de catálogos, esquemas y tipos de tabla, la semántica especial siguiente se define para la *CatalogName*, *SchemaName*, *TableName*y  *TableType* argumentos de **SQLTables**:  
  
-   Si *CatalogName* es SQL_ALL_CATALOGS y *SchemaName* y *TableName* son cadenas vacías, el conjunto de resultados contiene una lista de catálogos válidos para el origen de datos. (Todas las columnas excepto la columna TABLE_CAT contienen valores NULL).  
  
-   Si *SchemaName* es SQL_ALL_SCHEMAS y *CatalogName* y *TableName* son cadenas vacías, el conjunto de resultados contiene una lista de esquemas válidos para el origen de datos. (Todas las columnas excepto la columna según TABLE_SCHEM contienen valores NULL).  
  
-   Si *TableType* es SQL_ALL_TABLE_TYPES y *CatalogName*, *SchemaName*, y *TableName* son cadenas vacías, el conjunto de resultados contiene una lista de tipos de tablas válido para el origen de datos. (Todas las columnas excepto la columna TABLE_TYPE contienen valores NULL).  
  
 Si *TableType* no es una cadena vacía, debe contener una lista de valores separados por comas para los tipos de interés; cada valor puede ir entre comillas simples (') o sin comillas, por ejemplo, 'TABLE', 'Ver' o tabla, ver. Una aplicación siempre debe especificar el tipo de tabla en mayúsculas; el controlador debe convertir el tipo de tabla en cualquier caso es necesario para el origen de datos. Si el origen de datos no admite un tipo de tabla especificado, **SQLTables** no devuelve ningún resultado para ese tipo.  
  
 **SQLTables** devuelve los resultados como un conjunto de resultados estándar, ordenado por TABLE_TYPE, TABLE_CAT, según TABLE_SCHEM y TABLE_NAME. Para obtener información acerca de cómo se podría utilizar esta información, consulte [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar la longitud real de las columnas TABLE_CAT, según TABLE_SCHEM y TABLE_NAME, una aplicación puede llamar a **SQLGetInfo** con la información de SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN y SQL_MAX_TABLE_NAME_LEN tipos.  
  
 Las columnas siguientes se cambió para ODBC 3 *.x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones enlazar por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3 *.x* columna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. El controlador, se pueden definir columnas adicionales más allá de la columna 5 (comentarios). Una aplicación debe tener acceso a columnas específicas del controlador contando hacia abajo desde el final del conjunto en lugar de especificar una posición ordinal explícitos de resultados. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nombre del catálogo; Es NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tiene catálogos.|  
|SEGÚN TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con esquemas para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tengan esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|Nombre de la tabla.|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|Nombre de tipo de tabla; uno de los siguientes: "TABLE", "Vista", "Tabla del sistema", "GLOBAL TEMPORARY", "LOCAL TEMPORARY", "ALIAS", "Sinónimo" o un nombre de tipo específico del origen de datos.<br /><br /> El significado de "ALIAS" y "Sinónimo" es específicos del controlador.|  
|COMENTARIOS (ODBC 1.0)|5|Varchar|Una descripción de la tabla.|  
  
## <a name="example"></a>Ejemplo  
 El siguiente código de ejemplo no libera identificadores y conexiones. Vea [SQLFreeHandle, función](../../../odbc/reference/syntax/sqlfreehandle-function.md) y [SQLFreeStmt, función](../../../odbc/reference/syntax/sqlfreestmt-function.md) para obtener ejemplos de código liberar los identificadores y las instrucciones.  
  
```  
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
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devuelve privilegios para una o varias columnas|[Función SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Devolver las columnas de una o varias tablas|[Función SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Capturar una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver estadísticas de las tablas e índices|[Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Devuelve privilegios para una o varias tablas|[Función SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
