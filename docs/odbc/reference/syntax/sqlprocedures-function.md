---
title: Función SQLProcedures (Función) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4c8b8a9f22f6005d1af811e56485299bad3a425
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306846"
---
# <a name="sqlprocedures-function"></a>Función SQLProcedures
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: ODBC  
  
 **Resumen**  
 **SQLProcedures** devuelve la lista de nombres de procedimiento almacenados en un origen de datos específico. *Procedure* es un término genérico que se utiliza para describir un *objeto ejecutable*o una entidad con nombre que se puede invocar mediante parámetros de entrada y salida. Para obtener más información sobre los procedimientos, consulte [Procedimientos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *CatalogName*  
 [Entrada] Catálogo de procedimientos. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadenas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente, y su caso es significativo. Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de esquema de procedimiento. Si un controlador admite esquemas para algunos procedimientos pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica los procedimientos que no tienen esquemas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *ProcName*  
 [Entrada] Patrón de búsqueda de cadenas para nombres de procedimiento.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *ProcName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *ProcName* es un argumento de valor de patrón; se trata literalmente, y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **ProcName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLProcedures** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLProcedures** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
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
|HY009|Uso no válido de puntero nulo|El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y el SQL_CATALOG_NAME *InfoType* devuelve que se admiten los nombres de catálogo.<br /><br /> (DM) el atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE y el *SchemaName* o *ProcName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El valor de uno de los argumentos de longitud de nombre era menor que 0 pero no igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud de nombre superó el valor de longitud máxima para el nombre correspondiente.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo de procedimientos y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema de procedimiento y el controlador o el origen de datos no admite esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el esquema de procedimiento o el nombre del procedimiento y el origen de datos no admite patrones de búsqueda para uno o varios de esos argumentos.<br /><br /> El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados solicitado. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite esta función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLProcedures** enumera todos los procedimientos del intervalo solicitado. Un usuario puede o no tener permiso para ejecutar cualquiera de estos procedimientos. Para comprobar la accesibilidad, una aplicación puede llamar a **SQLGetInfo** y comprobar el valor de información de SQL_ACCESSIBLE_PROCEDURES. De lo contrario, la aplicación debe ser capaz de controlar una situación en la que el usuario selecciona un procedimiento que no puede ejecutar. Para obtener información sobre cómo se puede utilizar esta información, consulte [Procedimientos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de las funciones de catálogo ODBC, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
 **SQLProcedures** devuelve los resultados como un conjunto de resultados estándar, ordenado por PROCEDURE_CAT, PROCEDURE_SCHEMA y PROCEDURE_NAME.  
  
> [!NOTE]  
>  **SQLProcedures** podría no devolver todos los procedimientos. Las aplicaciones pueden usar cualquier procedimiento válido, independientemente de si **SQLProcedures**lo devuelve.  
  
 Se ha cambiado el nombre de las columnas siguientes para ODBC 3 *.x*. Los cambios en el nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones se enlazan por número de columna.  
  
|Columna ODBC 2.0|Columna ODBC 3 *.x*|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMIENTO _OWNER|PROCEDIMIENTO _SCHEM|  
  
 Para determinar las longitudes reales de las columnas PROCEDURE_CAT, PROCEDURE_SCHEM y PROCEDURE_NAME, una aplicación puede llamar a **SQLGetInfo** con las opciones SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN y SQL_MAX_PROCEDURE_NAME_LEN.  
  
 En la tabla siguiente se enumeran las columnas del conjunto de resultados. El controlador puede definir columnas adicionales más allá de la columna 8 (PROCEDURE_TYPE). Una aplicación debe obtener acceso a columnas específicas del controlador mediante la cuenta regresiva desde el final del conjunto de resultados en lugar de especificar una posición ordinal explícita. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
|Nombre de la columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Identificador de catálogo de procedimientos; NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunos procedimientos, pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellos procedimientos que no tienen catálogos.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Identificador de esquema de procedimiento; NULL si no es aplicable al origen de datos. Si un controlador admite esquemas para algunos procedimientos pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellos procedimientos que no tienen esquemas.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar no NULL|Identificador de procedimiento.|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|N/D|Reservado para uso futuro. Las aplicaciones no deben confiar en los datos devueltos en estas columnas de resultados.|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|N/D|Reservado para uso futuro. Las aplicaciones no deben confiar en los datos devueltos en estas columnas de resultados.|  
|NUM_RESULT_SETS (ODBC 2.0)|6|N/D|Reservado para uso futuro. Las aplicaciones no deben confiar en los datos devueltos en estas columnas de resultados.|  
|MARCAS (ODBC 2.0)|7|Varchar|Una descripción del procedimiento.|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|Define el tipo de procedimiento:<br /><br /> SQL_PT_UNKNOWN: No se puede determinar si el procedimiento devuelve un valor.<br /><br /> SQL_PT_PROCEDURE: el objeto devuelto es un procedimiento; es decir, no tiene un valor devuelto.<br /><br /> SQL_PT_FUNCTION: el objeto devuelto es una función; es decir, tiene un valor devuelto.|  
  
 Los argumentos *SchemaName* y *ProcName* aceptan patrones de búsqueda. Para obtener más información acerca de los patrones de búsqueda válidos, vea Argumentos de valor de [patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [Llamadas de](../../../odbc/reference/develop-app/procedure-calls.md)procedimiento .  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver información sobre un controlador o una fuente de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Devolver los parámetros y las columnas del conjunto de resultados de un procedimiento|[Función SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|Sintaxis para invocar procedimientos almacenados|[Ejecutar instrucciones](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
