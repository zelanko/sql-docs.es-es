---
title: Función SQLStatistics ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2a5ef0b0e54e17a2dc091a98efc972fa608ef15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302949"
---
# <a name="sqlstatistics-function"></a>Función SQLStatistics
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLStatistics** recupera una lista de estadísticas sobre una sola tabla y los índices asociados a la tabla. El controlador devuelve la información como un conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *CatalogName*  
 [Entrada] Nombre del catálogo. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadenas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente, y su caso es significativo. Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nombre del esquema. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen esquemas. *SchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *SchemaName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Nombre de la tabla. Este argumento no puede ser un puntero nulo. *SchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *TableName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *Único*  
 [Entrada] Tipo de índice: SQL_INDEX_UNIQUE o SQL_INDEX_ALL.  
  
 *Reserved*  
 [Entrada] Indica la importancia de las columnas CARDINALITY y PAGES en el conjunto de resultados. Las siguientes opciones solo afectan a la devolución de las columnas CARDINALITY y PAGES; la información de índice se devuelve incluso si no se devuelvecardinalidad y páginas.  
  
 SQL_ENSURE solicita que el controlador recupere incondicionalmente las estadísticas. (Los controladores que solo se ajustan al estándar Open Group y no admiten extensiones ODBC no podrán admitir SQL_ENSURE.)  
  
 SQL_QUICK solicita que el controlador recupere CARDINALITY y PAGES solo si están disponibles desde el servidor. En este caso, el controlador no garantiza que los valores sean actuales. (Las aplicaciones que se escriben en el estándar de grupo abierto siempre obtendrán SQL_QUICK comportamiento de los controladores compatibles con ODBC *3.x.)*  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLStatistics** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLStatistics** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** se había llamado. El Administrador de controladores devuelve este error si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y lo devuelve el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*, y, a continuación, se llamó a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|El *TableName* argumento era un puntero nulo.<br /><br /> El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y el SQL_CATALOG_NAME *InfoType* devuelve que se admiten los nombres de catálogo.<br /><br /> (DM) el atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE y el *SchemaName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLStatistics.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El valor de uno de los argumentos de longitud de nombre era menor que 0 pero no igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud de nombre superó el valor de longitud máxima para el nombre correspondiente.|  
|HY100|Tipo de opción de unicidad fuera de rango|(DM) Se especificó un valor *único* no válido.|  
|HY101|Tipo de opción de precisión fuera del rango|(DM) Se especificó un valor *Reservado* no válido.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema y el controlador o el origen de datos no admite esquemas.<br /><br /> El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados solicitado. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLStatistics** devuelve información sobre una sola tabla como un conjunto de resultados estándar, ordenado por NON_UNIQUE, TYPE, INDEX_QUALIFIER, INDEX_NAME y ORDINAL_POSITION. El conjunto de resultados combina información estadística (en las columnas CARDINALITY y PAGES del conjunto de resultados) de la tabla con información sobre cada índice. Para obtener información sobre cómo se puede usar esta información, vea [Usos de datos de catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar las longitudes reales de las columnas TABLE_CAT, TABLE_SCHEM, TABLE_NAME y COLUMN_NAME, una aplicación puede llamar a **SQLGetInfo** con las opciones SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN y SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de las funciones de catálogo ODBC, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
 Se ha cambiado el nombre de las columnas siguientes para ODBC *3.x*. Los cambios en el nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones se enlazan por número de columna.  
  
|Columna ODBC 2.0|Columna ODBC *3.x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 En la tabla siguiente se enumeran las columnas del conjunto de resultados. El controlador puede definir columnas adicionales más allá de la columna 13 (FILTER_CONDITION). Una aplicación debe obtener acceso a columnas específicas del controlador mediante la cuenta regresiva desde el final del conjunto de resultados en lugar de especificar una posición ordinal explícita. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
|Nombre de la columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nombre de catálogo de la tabla a la que se aplica la estadística o el índice; NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellas tablas que no tienen catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre de esquema de la tabla a la que se aplica la estadística o el índice; NULL si no es aplicable al origen de datos. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tienen esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar no NULL|Nombre de tabla de la tabla a la que se aplica la estadística o el índice.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Indica si el índice no permite valores duplicados:<br /><br /> SQL_TRUE si los valores de índice pueden ser no únicos.<br /><br /> SQL_FALSE si los valores de índice deben ser únicos.<br /><br /> NULL se devuelve si TYPE se SQL_TABLE_STAT.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|Identificador que se utiliza para calificar el nombre del índice mediante DROP **INDEX**; NULL se devuelve si el origen de datos no admite un calificador de índice o si TYPE está SQL_TABLE_STAT. Si se devuelve un valor distinto de null en esta columna, debe usarse para calificar el nombre del índice en una instrucción **DROP INDEX;** de lo contrario, el TABLE_SCHEM debe utilizarse para calificar el nombre del índice.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Nombre del índice; NULL se devuelve si TYPE se SQL_TABLE_STAT.|  
|TIPO (ODBC 1.0)|7|Smallint no NULL|Tipo de información que se devuelve:<br /><br /> SQL_TABLE_STAT indica una estadística para la tabla (en la columna CARDINALITY o PAGES).<br /><br /> SQL_INDEX_BTREE indica un índice de árbol B.<br /><br /> SQL_INDEX_CLUSTERED indica un índice clúster.<br /><br /> SQL_INDEX_CONTENT indica un índice de contenido.<br /><br /> SQL_INDEX_HASHED indica un índice hash.<br /><br /> SQL_INDEX_OTHER indica otro tipo de índice.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Número de secuencia de columnas en el índice (a partir de 1); NULL se devuelve si TYPE se SQL_TABLE_STAT.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Nombre de la columna. Si la columna se basa en una expresión, como SALARY + BENEFITS, se devuelve la expresión; si no se puede determinar la expresión, se devuelve una cadena vacía. NULL se devuelve si TYPE se SQL_TABLE_STAT.|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|Ordenar secuencia para la columna: "A" para ascendente; "D" para descender; NULL se devuelve si el origen de datos no admite la secuencia de ordenación de columnas o si TYPE es SQL_TABLE_STAT.|  
|CARDINALIDAD (ODBC 1.0)|11|Entero|Cardenalidad de la tabla o índice; número de filas en la tabla si TYPE es SQL_TABLE_STAT; número de valores únicos en el índice si TYPE no se SQL_TABLE_STAT; NULL se devuelve si el valor no está disponible desde el origen de datos.|  
|PÁGINAS (ODBC 1.0)|12|Entero|Número de páginas utilizadas para almacenar el índice o la tabla; número de páginas de la tabla si TYPE es SQL_TABLE_STAT; número de páginas para el índice si TYPE no está SQL_TABLE_STAT; NULL se devuelve si el valor no está disponible desde el origen de datos o si no es aplicable al origen de datos.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Si el índice es un índice filtrado, esta es la condición de filtro, como SALARY > 30000; si no se puede determinar la condición de filtro, se trata de una cadena vacía.<br /><br /> NULL si el índice no es un índice filtrado, no se puede determinar si el índice es un índice filtrado o TYPE es SQL_TABLE_STAT.|  
  
 Si la fila del conjunto de resultados corresponde a una tabla, el controlador establece TYPE en SQL_TABLE_STAT y establece NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME y ASC_OR_DESC en NULL. Si CARDINALITY o PAGES no están disponibles desde el origen de datos, el controlador los establece en NULL.  
  
## <a name="code-example"></a>Ejemplo de código  
 Para obtener un ejemplo de código de una función similar, vea [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance.|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver las columnas de claves externas|[Función SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Devolver las columnas de una clave principal|[Función SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
