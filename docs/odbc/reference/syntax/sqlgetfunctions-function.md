---
title: Función SQLGetFunctions ? Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15537b28ff2bae8a4fcd3e7be82426eb53aa83a8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285335"
---
# <a name="sqlgetfunctions-function"></a>Función SQLGetFunctions
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLGetFunctions** devuelve información sobre si un controlador admite una función ODBC específica. Esta función se implementa en el Administrador de controladores; también se puede implementar en controladores. Si un controlador implementa **SQLGetFunctions**, el Administrador de controladores llama a la función en el controlador. De lo contrario, ejecuta la propia función.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
 *Functionid*  
 [Entrada] Un **valor #define** que identifica la función ODBC de interés; **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**. **SQL_API_ODBC3_ALL_FUNCTIONS** es utilizado por una aplicación ODBC 3 *.x* para determinar la compatibilidad de ODBC 3 *.x* y funciones anteriores. **SQL_API_ALL_FUNCTIONS** es utilizado por una aplicación ODBC 2 *.x* para determinar la compatibilidad de ODBC 2 *.x* y funciones anteriores.  
  
 Para obtener una lista de **#define** valores que identifican funciones ODBC, vea las tablas en "Comentarios."  
  
 *SupportedPtr*  
 [Salida]  Si *FunctionId* identifica una sola función ODBC, *SupportedPtr* apunta a un único valor SQLUSMALLINT que se SQL_TRUE si el controlador admite la función especificada y SQL_FALSE si no se admite.  
  
 Si *FunctionId* es SQL_API_ODBC3_ALL_FUNCTIONS, *SupportedPtr* apunta a una matriz SQLSMALLINT con un número de elementos igual a SQL_API_ODBC3_ALL_FUNCTIONS_SIZE. El Administrador de controladores trata esta matriz como un mapa de bits de 4.000 bits que se puede utilizar para determinar si se admite una función ODBC 3 *.x* o anterior. Se llama a la macro SQL_FUNC_EXISTS para determinar la compatibilidad con funciones. (Véase "Comentarios.") Una aplicación ODBC 3 *.x* puede llamar a **SQLGetFunctions** con SQL_API_ODBC3_ALL_FUNCTIONS en un controlador ODBC 3 *.x* u ODBC 2 *.x.*  
  
 Si *FunctionId* es SQL_API_ALL_FUNCTIONS, *SupportedPtr* apunta a una matriz SQLUSMALLINT de 100 elementos. La matriz se indiza mediante **#define** valores utilizados por *FunctionId* para identificar cada función ODBC; algunos elementos de la matriz no se utilizan y se reservan para su uso futuro. Un elemento se SQL_TRUE si identifica una función ODBC 2 *.x* o anterior admitida por el controlador. Es SQL_FALSE si identifica una función ODBC no admitida por el controlador o no identifica una función ODBC.  
  
 Las matrices devueltas en **SupportedPtr* usan la indización de base cero.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetFunctions** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *control* de *ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLGetFunctions** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------|-----|-----------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) **SQLGetFunctions** se llamó antes de **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect**.<br /><br /> (DM) **SQLBrowseConnect** se llamó para el *ConnectionHandle* y devuelto SQL_NEED_DATA. Esta función se llamó antes de **SQLBrowseConnect** devuelto SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *ConnectionHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY095|Tipo de función fuera del rango|(DM) se especificó un valor *FunctionId* no válido.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetFunctions** siempre devuelve que **SQLGetFunctions**, **SQLDataSources**y **SQLDrivers** son compatibles. Lo hace porque estas funciones se implementan en el Administrador de controladores. El Administrador de controladores asignará una función ANSI a la función Unicode correspondiente si existe la función Unicode y asignará una función Unicode a la función ANSI correspondiente si existe la función ANSI. Para obtener información sobre cómo las aplicaciones usan **SQLGetFunctions**, vea Niveles de conformidad de [interfaz](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 A continuación se muestra una lista de valores válidos para *FunctionId* para funciones que se ajustan al nivel de cumplimiento de normas ISO 92:  
  
|Valor FunctionId|Valor FunctionId|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETENVATTR|  
|SQL_API_SQLCONNECT|SQL_API_SQLGETFUNCTIONS|  
|SQL_API_SQLCOPYDESC|SQL_API_SQLGETINFO|  
|SQL_API_SQLDATASOURCES|SQL_API_SQLGETSTMTATTR|  
|SQL_API_SQLDESCRIBECOL|SQL_API_SQLGETTYPEINFO|  
|SQL_API_SQLDISCONNECT|SQL_API_SQLNUMRESULTCOLS|  
|SQL_API_SQLDRIVERS|SQL_API_SQLPARAMDATA|  
|SQL_API_SQLENDTRAN|SQL_API_SQLPREPARE|  
|SQL_API_SQLEXECDIRECT|SQL_API_SQLPUTDATA|  
|SQL_API_SQLEXECUTE|SQL_API_SQLROWCOUNT|  
|SQL_API_SQLFETCH|SQL_API_SQLSETCONNECTATTR|  
|SQL_API_SQLFETCHSCROLL|SQL_API_SQLSETCURSORNAME|  
|SQL_API_SQLFREEHANDLE|SQL_API_SQLSETDESCFIELD|  
|SQL_API_SQLFREESTMT|SQL_API_SQLSETDESCREC|  
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETENVATTR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 A continuación se muestra una lista de valores válidos para *FunctionId* para funciones que cumplen con el nivel de cumplimiento de estándares de grupo abierto:  
  
|Valor FunctionId|Valor FunctionId|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 A continuación se muestra una lista de valores válidos para *FunctionId* para las funciones que se ajustan al nivel de cumplimiento de estándares ODBC.  
  
|Valor FunctionId|Valor FunctionId|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] Cuando se trabaja con un controlador ODBC 2 *.x,* **SQLBulkOperations** se devolverá como admitido solo si se cumplen las dos opciones siguientes: el controlador ODBC 2 *.x* admite **SQLSetPos**y el tipo de información SQL_POS_OPERATIONS devuelve el bit SQL_POS_ADD como establecido.  
  
 A continuación se muestra una lista de valores válidos para *FunctionId* para las funciones introducidas en ODBC 3.8 o posterior:  
  
|Valor FunctionId|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** se devolverá como compatible solo si el controlador admite **SQLCancel** y **SQLCancelHandle**. Si se admite **SQLCancel** pero **SQLCancelHandle** no lo es, la aplicación todavía puede llamar a **SQLCancelHandle** en un identificador de instrucción, porque se asignará a **SQLCancel**.  
  
## <a name="sql_func_exists-macro"></a>SQL_FUNC_EXISTS Macro  
 La macro SQL_FUNC_EXISTS(*SupportedPtr*, *FunctionID*) se utiliza para determinar la compatibilidad de ODBC 3 *.x* o funciones anteriores después de **SQLGetFunctions** se ha llamado con un *FunctionId* argumento de SQL_API_ODBC3_ALL_FUNCTIONS. La aplicación llama a SQL_FUNC_EXISTS con el *SupportedPtr* argumento establecido en el *SupportedPtr* pasado en *SQLGetFunctions*y con el *FunctionID* argumento establecido en el **#define** para la función. SQL_FUNC_EXISTS devuelve SQL_TRUE si se admite la función y SQL_FALSE lo contrario.  
  
> [!NOTE]
>  Cuando se trabaja con un controlador ODBC 2 *.x,* el Administrador de controladores ODBC 3 *.x* devolverá SQL_TRUE para **SQLAllocHandle** y **SQLFreeHandle** porque **SQLAllocHandle** está asignado a **SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt**, y porque **SQLFreeHandle** está asignado a **SQLFreeEnv**, **SQLFreeConnect**o **SQLFreeStmt**. **SQLAllocHandle** o **SQLFreeHandle** con un *HandleType* argumento de SQL_HANDLE_DESC no se admite, sin embargo, aunque se devuelve SQL_TRUE para las funciones, porque no hay ninguna función ODBC 2 *.x* para asignar en este caso.  
  
## <a name="code-example"></a>Ejemplo de código  
 En los tres ejemplos siguientes se muestra cómo una aplicación utiliza **SQLGetFunctions** para determinar si un controlador admite **SQLTables**, **SQLColumns**y **SQLStatistics**. Si el controlador no admite estas funciones, la aplicación se desconecta del controlador. El primer ejemplo llama a **SQLGetFunctions** una vez para cada función.  
  
```cpp  
SQLUSMALLINT TablesExists, ColumnsExists, StatisticsExists;  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
  
retcodeTables = SQLGetFunctions(hdbc, SQL_API_SQLTABLES, &TablesExists);  
retcodeColumns = SQLGetFunctions(hdbc, SQL_API_SQLCOLUMNS, &ColumnsExists);  
retcodeStatistics = SQLGetFunctions(hdbc, SQL_API_SQLSTATISTICS, &StatisticsExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (retcodeTables == SQL_SUCCESS && TablesExists == SQL_TRUE &&   
retcodeColumns == SQL_SUCCESS && ColumnsExists == SQL_TRUE &&   
retcodeStatistics == SQL_SUCCESS && StatisticsExists == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 En el segundo ejemplo, una aplicación ODBC 3.x llama a **SQLGetFunctions** y le pasa una matriz en la que **SQLGetFunctions** devuelve información sobre todas las funciones ODBC 3.x y anteriores.  
  
```cpp  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[SQL_API_ODBC3_ALL_FUNCTIONS_SIZE];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ODBC3_ALL_FUNCTIONS, fExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (reccode == SQL_SUCCESS &&   
SQL_FUNC_EXISTS(fExists, SQL_API_SQLTABLES) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLCOLUMNS) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLSTATISTICS) == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 El tercer ejemplo es una aplicación ODBC 2.x llama a **SQLGetFunctions** y le pasa una matriz de 100 elementos en la que **SQLGetFunctions** devuelve información sobre todas las funciones ODBC 2.x y anteriores.  
  
```cpp  
#define FUNCTIONS 100  
  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[FUNCTIONS];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ALL_FUNCTIONS, fExists);  
  
/* SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver. */  
if (retcode == SQL_SUCCESS &&   
fExists[SQL_API_SQLTABLES] == SQL_TRUE &&  
   fExists[SQL_API_SQLCOLUMNS] == SQL_TRUE &&  
   fExists[SQL_API_SQLSTATISTICS] == SQL_TRUE)   
{  
  
   /* Continue with application */  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Devolver la configuración de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Devolver información sobre un controlador o una fuente de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Devolver la configuración de un atributo de instrucción|[Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
