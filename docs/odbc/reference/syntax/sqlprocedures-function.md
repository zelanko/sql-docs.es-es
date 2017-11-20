---
title: "Función SQLProcedures | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2790087b4a8ea0518a81f540da6b3887933a4ef6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlprocedures-function"></a>Función SQLProcedures
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLProcedures** devuelve la lista de nombres de procedimientos almacenados en un origen de datos específico. *Procedimiento* es un término genérico que se utiliza para describir un *objeto ejecutable*, o una entidad con nombre que se puede invocar mediante parámetros de entrada y salida. Para obtener más información sobre procedimientos, consulte el [procedimientos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Catálogo de procedimiento. Si un controlador admite catálogos para algunas tablas pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de esquema de procedimiento. Si un controlador es compatible con esquemas para algunos procedimientos, pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica los procedimientos que no tengan esquemas.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *ProcName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de procedimiento.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *ProcName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *ProcName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **ProcName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLProcedures** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLProcedures** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** si se hubiese llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y se devuelve el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** si no se hubiese llamado.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*. A continuación, se llama a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero null|El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *tipo de información* devuelve que los nombres de catálogo se admite.<br /><br /> (DM) se estableció el atributo de instrucción de SQL_ATTR_METADATA_ID en SQL_TRUE y el *SchemaName* o *ProcName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica estaba aún se estaba ejecutando cuando se llama a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud de nombre era menor que 0 pero no es igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud de nombre supera el valor de longitud máxima para el nombre correspondiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo de procedimiento y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema de procedimiento y el controlador o el origen de datos no admite los esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el esquema de procedimiento o el nombre del procedimiento y el origen de datos no admite patrones de búsqueda para uno o varios de esos argumentos.<br /><br /> La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta expirado antes el origen de datos que devuelve el conjunto de resultados solicitada. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite esta función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLProcedures** enumera todos los procedimientos en el intervalo solicitado. Un usuario puede o no tenga permiso para ejecutar cualquiera de estos procedimientos. Para comprobar la accesibilidad, una aplicación puede llamar a **SQLGetInfo** y compruebe el valor de la información de SQL_ACCESSIBLE_PROCEDURES. En caso contrario, la aplicación debe ser capaz de controlar una situación donde el usuario selecciona un procedimiento que puede o no ejecutarse. Para obtener información acerca de cómo se podría utilizar esta información, consulte [procedimientos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedures** devuelve los resultados como un conjunto de resultados estándar, ordenado por PROCEDURE_CAT, PROCEDURE_SCHEMA y PROCEDURE_NAME.  
  
> [!NOTE]  
>  **SQLProcedures** no puede devolver todos los procedimientos. Las aplicaciones pueden usar cualquier procedimiento válido, independientemente de si se devuelve de forma **SQLProcedures**.  
  
 Las columnas siguientes se cambió para ODBC 3*.x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones enlazar por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3*.x* columna|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMIENTO _OWNER|PROCEDIMIENTO _SCHEM|  
  
 Para determinar la longitud real de las columnas PROCEDURE_CAT y PROCEDURE_SCHEM, PROCEDURE_NAME, una aplicación puede llamar a **SQLGetInfo** con SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN y SQL_MAX_PROCEDURE_ Opciones de NAME_LEN.  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. Columnas adicionales más allá de la columna 8 (PROCEDURE_TYPE) pueden definirse mediante el controlador. Una aplicación debe tener acceso a columnas específicas del controlador contando hacia abajo desde el final del conjunto de resultados, en lugar de especificar una posición ordinal explícita. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Identificador de catálogo del procedimiento; Es NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunos procedimientos, pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para los procedimientos que no tiene catálogos.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Identificador de esquema de procedimiento; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con esquemas para algunos procedimientos, pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para los procedimientos que no tengan esquemas.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar no NULL|Identificador de procedimiento.|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|N/D|Reservado para uso futuro. Las aplicaciones no deben depender de los datos devueltos en estas columnas de resultados.|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|N/D|Reservado para uso futuro. Las aplicaciones no deben depender de los datos devueltos en estas columnas de resultados.|  
|NUM_RESULT_SETS (ODBC 2.0)|6|N/D|Reservado para uso futuro. Las aplicaciones no deben depender de los datos devueltos en estas columnas de resultados.|  
|COMENTARIOS (ODBC 2.0)|7|Varchar|Una descripción del procedimiento.|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|Define el tipo de procedimiento:<br /><br /> SQL_PT_UNKNOWN: No se puede determinar si el procedimiento devuelve un valor.<br /><br /> SQL_PT_PROCEDURE: El objeto devuelto es un procedimiento; es decir, no tiene un valor devuelto.<br /><br /> A SQL_PT_FUNCTION: El objeto devuelto es una función; es decir, tiene un valor devuelto.|  
  
 El *SchemaName* y *ProcName* argumentos aceptan patrones de búsqueda. Para obtener más información sobre los patrones de búsqueda válidos, consulte [argumentos de valor de patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [las llamadas a procedimiento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Capturar una sola fila o un bloque de datos en una dirección de solo avance|[SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver información acerca de un controlador o un origen de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Devuelva los parámetros y el resultado se debe establecer las columnas de un procedimiento|[SQLProcedureColumns, función](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|Sintaxis para llamar a procedimientos almacenados|[Ejecución de instrucciones](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

