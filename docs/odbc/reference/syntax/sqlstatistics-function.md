---
title: "Función SQLStatistics | Documentos de Microsoft"
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
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 664c3c439eacc7bfa5b5b1d59b8421f8067c3376
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlstatistics-function"></a>Función SQLStatistics
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLStatistics** recupera una lista de las estadísticas sobre una sola tabla y los índices asociados a la tabla. El controlador devuelve la información como un conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Nombre del catálogo. Si un controlador admite catálogos para algunas tablas pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nombre del esquema. Si un controlador es compatible con esquemas para algunas tablas pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tengan esquemas. *SchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *SchemaName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *Nombre de tabla*  
 [Entrada] Nombre de la tabla. Este argumento no puede ser un puntero nulo. *SchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *TableName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *Único*  
 [Entrada] Tipo de índice: SQL_INDEX_UNIQUE o SQL_INDEX_ALL.  
  
 *Reservado*  
 [Entrada] Indica la importancia de las columnas de CARDINALIDAD y las páginas del conjunto de resultados. Las opciones siguientes afectan a la devolución de las columnas de la CARDINALIDAD y páginas únicamente; incluso si no se devuelven la CARDINALIDAD y las páginas, se devuelve información de índice.  
  
 SQL_ENSURE solicita que el controlador incondicionalmente recuperar las estadísticas. (Los controladores que solo cumplen el estándar Open Group y no admiten extensiones de ODBC no será capaces de admitir SQL_ENSURE.)  
  
 SQL_QUICK solicita que el controlador de recuperar la CARDINALIDAD y las páginas solo si están siempre disponibles desde el servidor. En este caso, el controlador no garantiza que los valores sean actuales. (Las aplicaciones que se escriben en el estándar Open Group siempre obtendrá un comportamiento SQL_QUICK de ODBC 3*.x*-controladores compatibles.)  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLStatistics** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLStatistics** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** si se hubiese llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** si no se hubiese llamado.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*, y, a continuación, se llama a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero null|El *TableName* argumento era un puntero nulo.<br /><br /> El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *tipo de información* devuelve que los nombres de catálogo se admite.<br /><br /> (DM) se estableció el atributo de instrucción de SQL_ATTR_METADATA_ID en SQL_TRUE y el *SchemaName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLStatistics** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud de nombre era menor que 0 pero no es igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud de nombre supera el valor de longitud máxima para el nombre correspondiente.|  
|HY100|Tipo de opción de unicidad fuera del intervalo|(DM) no válido *Unique* se especificó un valor.|  
|HY101|Tipo de opción de precisión fuera del intervalo|(DM) no válido *reservado* se especificó un valor.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo y del origen de datos o el controlador no admite catálogos.<br /><br /> Se especificó un esquema y el controlador o el origen de datos no admite los esquemas.<br /><br /> La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta expirado antes el origen de datos que devuelve el conjunto de resultados solicitada. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLStatistics** devuelve información acerca de una sola tabla como un conjunto de resultados estándar que se ordenan por NON_UNIQUE, tipo, INDEX_QUALIFIER, INDEX_NAME y ORDINAL_POSITION. El conjunto de resultados combina información de estadísticas (en las columnas de CARDINALIDAD y las páginas del conjunto de resultados) para la tabla con información acerca de cada índice. Para obtener información acerca de cómo se podría utilizar esta información, consulte [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar la longitud real de las columnas TABLE_CAT, según TABLE_SCHEM, TABLE_NAME y COLUMN_NAME, una aplicación puede llamar a **SQLGetInfo** con el SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, y las opciones de SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Las columnas siguientes se cambió para ODBC 3*.x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones enlazar por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3*.x* columna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. El controlador, se pueden definir columnas adicionales más allá de 13 (FILTER_CONDITION) de la columna. Una aplicación debe tener acceso a columnas específicas del controlador contando hacia abajo desde el final del conjunto en lugar de especificar una posición ordinal explícitos de resultados. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nombre del catálogo de la tabla a la que se aplica la estadística o índice; Es NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tiene catálogos.|  
|SEGÚN TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema de la tabla a la que se aplica la estadística o índice; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con esquemas para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tengan esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar no NULL|Nombre de tabla de la tabla a la que se aplica la estadística o índice.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Indica si el índice no permite valores duplicados:<br /><br /> SQL_TRUE si los valores de índice pueden ser no únicos.<br /><br /> SQL_FALSE si los valores de índice deben ser únicos.<br /><br /> Se devuelve NULL si el tipo es SQL_TABLE_STAT.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|El identificador que se utiliza para calificar el índice nombre al hacerlo un **DROP INDEX**; Si un calificador de índice no es compatible con el origen de datos o si el tipo es SQL_TABLE_STAT, se devuelve NULL. Si se devuelve un valor distinto de null en esta columna, se debe usar para calificar el nombre del índice en un **DROP INDEX** instrucción; en caso contrario, debe usarse la según TABLE_SCHEM para calificar el nombre del índice.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Nombre del índice; Se devuelve NULL si el tipo es SQL_TABLE_STAT.|  
|TIPO DE (ODBC 1.0)|7|Smallint no NULL|Tipo de información que se devuelve:<br /><br /> SQL_TABLE_STAT indica una estadística para la tabla (en la columna de CARDINALIDAD o páginas).<br /><br /> SQL_INDEX_BTREE indica un índice de árbol B.<br /><br /> SQL_INDEX_CLUSTERED indica un índice agrupado.<br /><br /> SQL_INDEX_CONTENT indica un índice de contenido.<br /><br /> SQL_INDEX_HASHED indica un índice hash.<br /><br /> SQL_INDEX_OTHER indica que otro tipo de índice.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Número de secuencia de la columna de índice (empezando por 1); Se devuelve NULL si el tipo es SQL_TABLE_STAT.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Nombre de columna. Si la columna se basa en una expresión, por ejemplo, salario + beneficios, se devuelve la expresión; Si la expresión no se puede determinar, se devuelve una cadena vacía. Se devuelve NULL si el tipo es SQL_TABLE_STAT.|  
|ASC_OR_DESC (ODBC 1.0)|10|Char (1)|Ordenar la secuencia para la columna: "A" para ascendente; "D" para descendente; Se devuelve NULL si la secuencia de ordenación de columna no es compatible con el origen de datos o si el tipo es SQL_TABLE_STAT.|  
|CARDINALIDAD (ODBC 1.0)|11|Integer|Cardinalidad de tabla o índice; número de filas de tabla si el tipo es SQL_TABLE_STAT; número de valores únicos del índice si el tipo no es SQL_TABLE_STAT; Se devuelve NULL si el valor no está disponible desde el origen de datos.|  
|PÁGINAS DE (ODBC 1.0)|12|Integer|Número de páginas utilizadas para almacenar el índice o tabla. número de páginas de la tabla si el tipo es SQL_TABLE_STAT; número de páginas de índice si el tipo no es SQL_TABLE_STAT; Se devuelve NULL si el valor no está disponible desde el origen de datos o si no es aplicable al origen de datos.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Si el índice es un índice filtrado, se trata de la condición de filtro, por ejemplo, salario > 30000; Si no se puede determinar la condición de filtro, esto es una cadena vacía.<br /><br /> Es NULL si el índice no es un índice filtrado, no se puede determinar si el índice es un índice filtrado o el tipo es SQL_TABLE_STAT.|  
  
 Si la fila del conjunto de resultados corresponde a una tabla, el controlador establece el tipo para SQL_TABLE_STAT y NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME y ASC_OR_DESC establece en NULL. Si la CARDINALIDAD o las páginas no están disponibles desde el origen de datos, el controlador los establece en NULL.  
  
## <a name="code-example"></a>Ejemplo de código  
 Para obtener un ejemplo de código de una función similar, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Capturar una sola fila o un bloque de datos en una dirección de solo avance.|[SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devuelve las columnas de claves externas|[SQLForeignKeys, función](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Devuelve las columnas de una clave principal|[SQLPrimaryKeys, función](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

