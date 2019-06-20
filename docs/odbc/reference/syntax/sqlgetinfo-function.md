---
title: Función SQLGetInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInfo
helpviewer_keywords:
- SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af4b2b5546e8b084afbdd769fb93c416964b0c13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537987"
---
# <a name="sqlgetinfo-function"></a>Función SQLGetInfo
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLGetInfo** proporciona información general sobre el origen de datos y controladores asociado con una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
 *InfoType*  
 [Entrada] Tipo de información.  
  
 *InfoValuePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver la información. En función de la *InfoType* solicitada, la información devuelta será uno de los siguientes: una cadena de caracteres terminada en null, un valor SQLUSMALLINT, una máscara de bits SQLUINTEGER que incluya, un indicador SQLUINTEGER que incluya, un valor binario SQLUINTEGER que incluya, o un Valor SQLULEN.  
  
 Si el *InfoType* argumento es SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT, el *InfoValuePtr* argumento es tanto de entrada y salido. (Vea los descriptores de SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT más adelante en esta descripción de la función para obtener más información).  
  
 Si *InfoValuePtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (excluido el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por *InfoValuePtr*.  
  
 *BufferLength*  
 [Entrada] Longitud de la \* *InfoValuePtr* búfer. Si el valor de  *\*InfoValuePtr* no es una cadena de caracteres o si *InfoValuePtr* es un puntero nulo, el *BufferLength* argumento se omite. El controlador se da por supuesto que el tamaño de  *\*InfoValuePtr* es SQLUSMALLINT o SQLUINTEGER, según la *InfoType*. Si  *\*InfoValuePtr* es una cadena Unicode (al llamar a **SQLGetInfoW**), el *BufferLength* argumento debe ser un número par; si no, SQLSTATE HY090 () Se devuelve la longitud de búfer o cadena no válida).  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de bytes (excluido el carácter de terminación null para los datos de caracteres) disponibles para devolver en **InfoValuePtr*.  
  
 Datos de caracteres, si el número de bytes disponible para devolver es mayor o igual a *BufferLength*, la información de \* *InfoValuePtr* se trunca a  *BufferLength* bytes menos la longitud de una terminación null de caracteres y termina en null por el controlador.  
  
 Para los demás tipos de datos, el valor de *BufferLength* se omite y el controlador supone que el tamaño de \* *InfoValuePtr* es SQLUSMALLINT o SQLUINTEGER, según la  *Tipo de información*.  
  
## <a name="return-value"></a>Valor devuelto  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetInfo** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *controlar* de *ConnectionHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetInfo** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|El búfer \* *InfoValuePtr* no era lo suficientemente grande como para devolver toda la información solicitada. Por lo tanto, la información se truncó. Se devuelve la longitud de la información solicitada en su forma sin truncar en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|(DM) el tipo de información solicitada en *InfoType* requiere una conexión abierta. Los tipos de información reservados por ODBC, se pueden devolver sólo SQL_ODBC_VER sin una conexión abierta.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY024|Valor de atributo no válido|(DM) el *InfoType* argumento era SQL_DRIVER_HSTMT y el valor señalado por *InfoValuePtr* no era un identificador de instrucción válida.<br /><br /> (DM) el *InfoType* argumento era SQL_DRIVER_HDESC y el valor señalado por *InfoValuePtr* no era un identificador de descriptor válido.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.<br /><br /> (DM) el valor especificado para *BufferLength* era un número impar, y  *\*InfoValuePtr* era del tipo de datos Unicode.|  
|HY096|Tipo de información fuera del intervalo|El valor especificado para el argumento *InfoType* no era válido para la versión de ODBC compatible con el controlador.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Campo opcional no implementada|El valor especificado para el argumento *InfoType* era un valor específico del controlador que no es compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador que se corresponde con el *ConnectionHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Se muestran los tipos de información definidos actualmente en "Tipos de información", más adelante en esta sección. se espera que más se definirá para aprovechar las ventajas de diferentes orígenes de datos. Un intervalo de tipos de información está reservado por ODBC; los desarrolladores de controladores deben reservar los valores para su propio uso específico del controlador de Open Group. **SQLGetInfo** no realiza ninguna conversión de Unicode o *thunk* (consulte [Apéndice A: Códigos de Error ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) de la *referencia del programador de ODBC*) para definidos por el controlador *tipos de información*. Para obtener más información, consulte [los tipos de datos específicos del controlador, Descriptor tipos, tipos de información, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md). El formato de la información devuelta en \* *InfoValuePtr* depende de la *InfoType* solicitado. **SQLGetInfo** devolverá información en uno de los cinco formatos diferentes:  
  
-   Una cadena de caracteres terminada en null  
  
-   Un valor SQLUSMALLINT  
  
-   Una máscara de bits SQLUINTEGER  
  
-   Un valor SQLUINTEGER  
  
-   Un valor binario SQLUINTEGER  
  
 El formato de cada uno de los siguientes tipos de información se indica en la descripción del tipo. La aplicación debe convertir el valor devuelto en **InfoValuePtr* en consecuencia. Para obtener un ejemplo de cómo una aplicación podría recuperar datos de una máscara de bits SQLUINTEGER, vea "Ejemplo de código".  
  
 Un controlador debe devolver un valor para cada tipo de información que se define en las tablas siguientes. Si no se aplica un tipo de información del origen de datos o el controlador, el controlador devuelve uno de los valores enumerados en la tabla siguiente.  
  
 Cadena de caracteres ("Y" o "N")  
 "N"  
  
 Cadena de caracteres (no "Y" o "N")  
 Cadena vacía  
  
 SQLUSMALLINT  
 0  
  
 Máscara de bits SQLUINTEGER o valor binario SQLUINTEGER  
 0L  
  
 Por ejemplo, si un origen de datos no es compatible con los procedimientos, **SQLGetInfo** devuelve los valores enumerados en la tabla siguiente para los valores de *InfoType* que están relacionadas con los procedimientos.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 Cadena vacía  
  
 **SQLGetInfo** devuelve SQLSTATE HY096 (valor de argumento no válido) para los valores de *InfoType* que están en el intervalo de tipos de información reservados para su uso por ODBC, pero no están definidos por la versión de ODBC compatible con el controlador. Para determinar qué versión de ODBC cumple un controlador, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_DRIVER_ODBC_VER. **SQLGetInfo** devuelve SQLSTATE HYC00 (característica opcional no implementada) para los valores de *InfoType* que están en el intervalo de tipos de información de reserva para uso específico del controlador, pero no son compatibles con el controlador.  
  
 Todas las llamadas a **SQLGetInfo** requieren una conexión abierta, excepto cuando la *InfoType* es SQL_ODBC_VER, que devuelve la versión del Administrador de controladores.  
  
## <a name="information-types"></a>Tipos de información  
 Esta sección enumeran los tipos de información compatibles con **SQLGetInfo**. Tipos de información se agrupan de manera categórica y alfabético. Tipos de información que se han agregado o cambiado el nombre de ODBC 3 *.x* también se muestran.  
  
## <a name="driver-information"></a>Información del controlador  
 Los siguientes valores de la *InfoType* argumento devuelven información sobre el controlador ODBC, como el número de instrucciones activas, el nombre del origen de datos y el nivel de cumplimiento de estándares de interfaz:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_FILE_USAGE|  
|SQL_ASYNC_MODE|SQL_GETDATA_EXTENSIONS|  
|SQL_ASYNC_NOTIFICATION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_BATCH_ROW_COUNT|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_BATCH_SUPPORT|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_DATA_SOURCE_NAME|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|SQL_MAX_CONCURRENT_ACTIVITIES|  
|SQL_DRIVER_HDBC|SQL_MAX_DRIVER_CONNECTIONS|  
|SQL_DRIVER_HDESC|SQL_ODBC_INTERFACE_CONFORMANCE|  
|SQL_DRIVER_HENV|SQL_ODBC_STANDARD_CLI_CONFORMANCE|  
|SQL_DRIVER_HLIB|SQL_ODBC_VER|  
|SQL_DRIVER_HSTMT|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_DRIVER_NAME|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DRIVER_ODBC_VER|SQL_ROW_UPDATES|  
|SQL_DRIVER_VER|SQL_SEARCH_PATTERN_ESCAPE|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|SQL_SERVER_NAME|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_STATIC_CURSOR_ATTRIBUTES2|  
  
> [!NOTE]  
>  Al implementar **SQLGetInfo**, un controlador puede mejorar el rendimiento, ya que minimiza el número de veces que se envía o se solicitan del servidor de información.  
  
## <a name="dbms-product-information"></a>Información de producto DBMS  
 Los siguientes valores de la *InfoType* argumento devolver información sobre el producto DBMS, como el nombre DBMS y la versión:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Información de origen de datos  
 Los siguientes valores de la *InfoType* argumento devuelven información sobre el origen de datos, como las características del cursor y las funcionalidades de transacción:  
  
|||  
|-|-|  
|SQL_ACCESSIBLE_PROCEDURES|SQL_MULT_RESULT_SETS|  
|SQL_ACCESSIBLE_TABLES|SQL_MULTIPLE_ACTIVE_TXN|  
|SQL_BOOKMARK_PERSISTENCE|SQL_NEED_LONG_DATA_LEN|  
|SQL_CATALOG_TERM|SQL_NULL_COLLATION|  
|SQL_COLLATION_SEQ|SQL_PROCEDURE_TERM|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_SCHEMA_TERM|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_SCROLL_OPTIONS|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_TABLE_TERM|  
|SQL_CURSOR_SENSITIVITY|SQL_TXN_CAPABLE|  
|SQL_DATA_SOURCE_READ_ONLY|SQL_TXN_ISOLATION_OPTION|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_USER_NAME|  
|SQL_DESCRIBE_PARAMETER||  
  
## <a name="supported-sql"></a>SQL admitidas  
 Los siguientes valores de la *InfoType* argumento devuelven información acerca de las instrucciones SQL admite el origen de datos. La sintaxis SQL de cada característica descrita por estos tipos de información es la sintaxis de SQL-92. Estos tipos de información no se describen exhaustivamente toda la gramática de SQL-92. En su lugar, describen las partes de la gramática para los datos de orígenes normalmente ofrecen diferentes niveles de soporte técnico. En concreto, se trata la mayoría de las instrucciones de DDL de SQL-92.  
  
 Las aplicaciones deben determinar el nivel de gramática compatible desde el tipo de información SQL_SQL_CONFORMANCE general y utilizar los otros tipos de información para determinar las variaciones en el nivel de cumplimiento de estándares establecidos.  
  
|||  
|-|-|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DROP_TABLE|  
|SQL_ALTER_DOMAIN|SQL_DROP_TRANSLATION|  
|SQL_ALTER_SCHEMA|SQL_DROP_VIEW|  
|SQL_ALTER_TABLE|SQL_EXPRESSIONS_IN_ORDERBY|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_GROUP_BY|  
|SQL_CATALOG_LOCATION|SQL_IDENTIFIER_CASE|  
|SQL_CATALOG_NAME|SQL_IDENTIFIER_QUOTE_CHAR|  
|SQL_CATALOG_NAME_SEPARATOR|SQL_INDEX_KEYWORDS|  
|SQL_CATALOG_USAGE|SQL_INSERT_STATEMENT|  
|SQL_COLUMN_ALIAS|SQL_INTEGRITY|  
|SQL_CORRELATION_NAME|SQL_KEYWORDS|  
|SQL_CREATE_ASSERTION|SQL_LIKE_ESCAPE_CLAUSE|  
|SQL_CREATE_CHARACTER_SET|SQL_NON_NULLABLE_COLUMNS|  
|SQL_CREATE_COLLATION|SQL_SQL_CONFORMANCE|  
|SQL_CREATE_DOMAIN|SQL_OJ_CAPABILITIES|  
|SQL_CREATE_SCHEMA|SQL_ORDER_BY_COLUMNS_IN_SELECT|  
|SQL_CREATE_TABLE|SQL_OUTER_JOINS|  
|SQL_CREATE_TRANSLATION|SQL_PROCEDURES|  
|SQL_DDL_INDEX|SQL_QUOTED_IDENTIFIER_CASE|  
|SQL_DROP_ASSERTION|SQL_SCHEMA_USAGE|  
|SQL_DROP_CHARACTER_SET|SQL_SPECIAL_CHARACTERS|  
|SQL_DROP_COLLATION|SQL_SUBQUERIES|  
|SQL_DROP_DOMAIN|SQL_UNION|  
|SQL_DROP_SCHEMA||  
  
## <a name="sql-limits"></a>Límites de SQL  
 Los siguientes valores de la *InfoType* argumento devolver información acerca de los límites que se aplica a los identificadores y las cláusulas en instrucciones SQL, como las longitudes máximas de identificadores y el número máximo de columnas en una lista de selección. El controlador o el origen de datos se pueden imponer limitaciones.  
  
|||  
|-|-|  
|SQL_MAX_BINARY_LITERAL_LEN|SQL_MAX_IDENTIFIER_LEN|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAX_INDEX_SIZE|  
|SQL_MAX_CHAR_LITERAL_LEN|SQL_MAX_PROCEDURE_NAME_LEN|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAX_ROW_SIZE|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAX_ROW_SIZE_INCLUDES_LONG|  
|SQL_MAX_COLUMNS_IN_INDEX|SQL_MAX_SCHEMA_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAX_STATEMENT_LEN|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAX_TABLE_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAX_TABLES_IN_SELECT|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAX_USER_NAME_LEN|  
  
## <a name="scalar-function-information"></a>Información de la función escalar  
 Los siguientes valores de la *InfoType* argumento devuelven información acerca de las funciones escalares que admite el origen de datos y el controlador. Para obtener más información acerca de las funciones escalares, vea [Apéndice E: Funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Información de conversión  
 Los siguientes valores de la *InfoType* argumento devuelve una lista de los tipos de datos SQL a la que el origen de datos puede convertir el tipo de datos SQL especificado con el **convertir** función escalar:  
  
|||  
|-|-|  
|SQL_CONVERT_BIGINT|SQL_CONVERT_LONGVARBINARY|  
|SQL_CONVERT_BINARY|SQL_CONVERT_LONGVARCHAR|  
|SQL_CONVERT_BIT|SQL_CONVERT_NUMERIC|  
|SQL_CONVERT_CHAR|SQL_CONVERT_REAL|  
|SQL_CONVERT_DATE|SQL_CONVERT_SMALLINT|  
|SQL_CONVERT_DECIMAL|SQL_CONVERT_TIME|  
|SQL_CONVERT_DOUBLE|SQL_CONVERT_TIMESTAMP|  
|SQL_CONVERT_FLOAT|SQL_CONVERT_TINYINT|  
|SQL_CONVERT_INTEGER|SQL_CONVERT_VARBINARY|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_CONVERT_VARCHAR|  
|SQL_CONVERT_INTERVAL_DAY_TIME||  
  
## <a name="information-types-added-for-odbc-3x"></a>Agregan tipos de información para ODBC 3.x  
 Los siguientes valores de la *InfoType* argumento se han agregado para ODBC 3 *.x*:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_DRIVER_AWARE_POOLING_SUPPORTED|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DRIVER_HDESC|  
|SQL_ALTER_DOMAIN|SQL_DROP_ASSERTION|  
|SQL_ALTER_SCHEMA|SQL_DROP_CHARACTER_SET|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_DROP_COLLATION|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_DROP_DOMAIN|  
|SQL_ASYNC_MODE|SQL_DROP_SCHEMA|  
|SQL_ASYNC_NOTIFICATION|SQL_DROP_TABLE|  
|SQL_BATCH_ROW_COUNT|SQL_DROP_TRANSLATION|  
|SQL_BATCH_SUPPORT|SQL_DROP_VIEW|  
|SQL_CATALOG_NAME|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|  
|SQL_COLLATION_SEQ|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|  
|SQL_CONVERT_INTERVAL_DAY_TIME|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_ASSERTION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_CREATE_CHARACTER_SET|SQL_INSERT_STATEMENT|  
|SQL_CREATE_COLLATION|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_CREATE_DOMAIN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_SCHEMA|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_CREATE_TABLE|SQL_MAX_IDENTIFIER_LEN|  
|SQL_CREATE_TRANSLATION|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_CURSOR_SENSITIVITY|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DDL_INDEX|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_DESCRIBE_PARAMETER|SQL_STATIC_CURSOR_ATTRIBUTES2|  
|SQL_DM_VER|SQL_XOPEN_CLI_YEAR|  
  
## <a name="information-types-renamed-for-odbc-3x"></a>Tipos de información que cambia el nombre para ODBC 3.x  
 Los siguientes valores de la *InfoType* cambió el argumento para ODBC 3 *.x*.  
  
 SQL_ACTIVE_CONNECTIONS  
 SQL_MAX_DRIVER_CONNECTIONS  
  
 SQL_ACTIVE_STATEMENTS  
 SQL_MAX_CONCURRENT_ACTIVITIES  
  
 SQL_MAX_OWNER_NAME_LEN  
 SQL_MAX_SCHEMA_NAME_LEN  
  
 SQL_MAX_QUALIFIER_NAME_LEN  
 SQL_MAX_CATALOG_NAME_LEN  
  
 SQL_ODBC_SQL_OPT_IEF  
 SQL_INTEGRITY  
  
 SQL_OWNER_TERM  
 SQL_SCHEMA_TERM  
  
 SQL_OWNER_USAGE  
 SQL_SCHEMA_USAGE  
  
 SQL_QUALIFIER_LOCATION  
 SQL_CATALOG_LOCATION  
  
 SQL_QUALIFIER_NAME_SEPARATOR  
 SQL_CATALOG_NAME_SEPARATOR  
  
 SQL_QUALIFIER_TERM  
 SQL_CATALOG_TERM  
  
 SQL_QUALIFIER_USAGE  
 SQL_CATALOG_USAGE  
  
## <a name="information-types-deprecated-in-odbc-3x"></a>Tipos de información en desuso en ODBC 3.x  
 Los siguientes valores de la *InfoType* argumento han quedado obsoletas en ODBC 3 *.x*. ODBC 3 *.x* controladores deben seguir admitir estos tipos de información para mantener la compatibilidad con ODBC 2 *.x* aplicaciones. (Para obtener más información acerca de estos tipos, vea [compatibilidad con SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md) en Apéndice G: Directrices de controlador para compatibilidad con versiones anteriores.)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Descripciones de tipo de información  
 En la tabla siguiente se enumera por orden alfabético cada tipo de información, la versión de ODBC en el que se introdujo y su descripción.  
  
 SQL_ACCESSIBLE_PROCEDURES(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el usuario puede ejecutar todos los procedimientos que devuelve **SQLProcedures**; "N" si puede haber procedimientos devuelto que no se puede ejecutar el usuario.  
  
 SQL_ACCESSIBLE_TABLES(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el usuario tiene la garantía **seleccione** privilegios a todas las tablas devueltas por **SQLTables**; "N" si puede haber tablas devuelto que el usuario no tiene acceso.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de los entornos activos que puede admitir el controlador. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar la compatibilidad con las funciones de agregación:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá todas estas opciones como compatible.  
  
 SQL_ALTER_DOMAIN(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **ALTER dominio** instrucción, tal como se define en SQL-92, admitidos por el origen de datos. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas las máscaras de bits. Un valor devuelto de "0" significa que el **ALTER dominio** no se admite la instrucción.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = agregar una restricción de dominio es compatible (nivel total)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter dominio > \<cláusula predeterminado de set domain > es compatible (nivel total)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<cláusula de definición de restricción name > es compatible con nombres de restricción de dominio (nivel intermedio)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<cláusula de restricción de dominio de destino > es compatible (nivel total)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter dominio > \<cláusula default de colocación dominio > es compatible (nivel total)  
  
 Los bits siguientes especifican admitidos \<atributos restricción > Si \<Agregar restricción de dominio > es compatible (se establece el bit SQL_AD_ADD_DOMAIN_CONSTRAINT):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (nivel completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (nivel completo) (nivel Full) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (nivel completo)  
  
 SQL_ALTER_TABLE(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **ALTER TABLE** instrucción admitida por el origen de datos.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<Agregar columna > se admite la cláusula con facilidad para especificar la intercalación de columna (nivel completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<Agregar columna > se admite la cláusula con facilidad para especificar los valores predeterminados de columna (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<Agregar columna > es compatible (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<Agregar columna > se admite la cláusula con facilidad para especificar restricciones de columna (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<Agregar restricción de tabla > se admite la cláusula (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<definición del nombre de restricción > se admite para asignar nombres a las restricciones de columna y tabla (nivel intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<quitar columnas > se admite en cascada (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alteración de columna > \<cláusula predeterminado de drop column > es compatible (nivel intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<quitar columnas > RESTRICT es compatible (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<quitar columnas > RESTRICT es compatible (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alteración de columna > \<cláusula de conjunto de columnas predeterminado > es compatible (nivel intermedio) (ODBC 3.0)  
  
 Los bits siguientes especifican la compatibilidad con \<atributos restricción > Si se admite la especificación de restricciones de columna o tabla (se establece el bit SQL_AT_ADD_CONSTRAINT):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (nivel completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (nivel completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (nivel completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (nivel completo) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 Un valor SQLUINTEGER que indica si el controlador puede ejecutar las funciones de forma asincrónica en el identificador de conexión.  
  
 SQL_ASYNC_DBC_CAPABLE = el controlador puede ejecutar funciones de conexión de forma asincrónica.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = el controlador no puede ejecutar funciones de conexión asincrónica.  
  
 SQL_ASYNC_MODE(ODBC 3.0)  
 Un valor SQLUINTEGER que indica el nivel de compatibilidad asincrónica en el controlador:  
  
 SQL_AM_CONNECTION = se admite la ejecución asincrónica de nivel de conexión. Todos los identificadores de instrucción asociados con un identificador de conexión determinado están en modo asincrónico o todas están en modo sincrónico. Un identificador de instrucción en una conexión no puede estar en modo asincrónico mientras otro identificador de instrucción en la misma conexión está en modo sincrónico y viceversa.  
  
 SQL_AM_STATEMENT = se admite la ejecución asincrónica de nivel de instrucción. Algunos identificadores de instrucciones asociados con un identificador de conexión pueden estar en modo asincrónico, mientras que otros identificadores de instrucciones en la misma conexión están en modo sincrónico.  
  
 SQL_AM_NONE = asincrónico no se admite el modo.  
  
 SQL_ASYNC_NOTIFICATION  
 Un valor SQLUINTEGER que indica si el controlador admite la notificación asincrónica:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** notificación de ejecución asincrónica es compatible con el controlador.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** notificación de ejecución asincrónica no es compatible con el controlador.  
  
 Existen dos categorías de operaciones asincrónicas de ODBC: operaciones asincrónicas de nivel de conexión y la instrucción de nivel de operaciones asincrónicas.  Si un controlador devuelve SQL_ASYNC_NOTIFICATION_CAPABLE, debe admitir notificaciones para todas las API que puede ejecutar de forma asincrónica.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Recuentos de máscara de bits SQLUINTEGER que enumera el comportamiento del controlador con respecto a la disponibilidad de la fila. Las máscaras de bits siguientes se utilizan junto con el tipo de información:  
  
 SQL_BRC_ROLLED_UP = recuentos de filas para las instrucciones INSERT, DELETE o UPDATE consecutivas se consolidan en uno. Si no se establece este bit, recuentos de filas están disponibles para cada instrucción.  
  
 SQL_BRC_PROCEDURES = recuentos de filas, si existe, están disponibles cuando se ejecuta un lote en un procedimiento almacenado. Si existen recuentos de filas, puede desplegar o disponibles de forma individual, según el bit SQL_BRC_ROLLED_UP.  
  
 SQL_BRC_EXPLICIT = recuentos de filas, si existe, están disponibles cuando se ejecuta un lote directamente mediante una llamada a **SQLExecute** o **SQLExecDirect**. Si existen recuentos de filas, puede desplegar o disponibles de forma individual, según el bit SQL_BRC_ROLLED_UP.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar la compatibilidad del controlador para los lotes. Las máscaras de bits siguientes se utilizan para determinar qué nivel se admite:  
  
 SQL_BS_SELECT_EXPLICIT = el controlador admite explícita los lotes que pueden haber conjunto de resultados generar instrucciones.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = los lotes explícita es compatible con controladores que pueden tener instrucciones de generación de recuento de filas.  
  
 SQL_BS_SELECT_PROC = el controlador admite explícita los procedimientos que pueden dispone de conjunto de resultados de generación de instrucciones.  
  
 SQL_BS_ROW_COUNT_PROC = el controlador admite explícita los procedimientos que pueden tener instrucciones de generación de recuento de filas.  
  
 SQL_BOOKMARK_PERSISTENCE(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las operaciones a través del cual los marcadores son persistentes.  
  
 Las máscaras de bits siguientes se usan junto con la marca para determinar a través del cual se conservan los marcadores de opciones:  
  
 SQL_BP_CLOSE = los marcadores son válidos después de una aplicación llama a **SQLFreeStmt** con la opción de SQL_CLOSE o **SQLCloseCursor** para cerrar el cursor asociado con una instrucción.  
  
 SQL_BP_DELETE = el marcador para una fila es válida después de esa fila se ha eliminado.  
  
 SQL_BP_DROP = los marcadores son válidos después de una aplicación llama a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT para una instrucción drop.  
  
 SQL_BP_TRANSACTION = los marcadores son válidos después de una aplicación se confirma o revierte una transacción.  
  
 SQL_BP_UPDATE = el marcador para una fila es válida después de cualquier columna de esa fila se ha actualizado, incluidas las columnas de clave.  
  
 SQL_BP_OTHER_HSTMT = un marcador asociado a una instrucción puede utilizarse con otra instrucción. A menos que se especifica SQL_BP_CLOSE o SQL_BP_DROP, el cursor en la primera instrucción debe estar abierto.  
  
 SQL_CATALOG_LOCATION(ODBC 2.0)  
 Un valor SQLUSMALLINT que indica la posición del catálogo en un nombre de tabla completo:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Por ejemplo, un controlador de Xbase devuelve SQL_CL_START porque es el nombre del directorio (catálogo) al principio del nombre de tabla, como en \EMPDATA\EMP. DBF. Un controlador de ORACLE Server devuelve SQL_CL_END porque el catálogo está al final del nombre de tabla, como en ADMIN.EMP@EMPDATA.  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá SQL_CL_START. Se devuelve un valor de 0 si el origen de datos no admite catálogos. Para determinar si se admiten los catálogos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_CATALOG_NAME.  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_QUALIFIER_LOCATION.  
  
 SQL_CATALOG_NAME(ODBC 3.0)  
 Una cadena de caracteres: "Y" si el servidor admite los nombres de catálogo o "N" Si no es así.  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá "S".  
  
 SQL_CATALOG_NAME_SEPARATOR(ODBC 1.0)  
 Una cadena de caracteres: el carácter o caracteres que define el origen de datos como el separador entre un nombre de catálogo y el elemento del nombre completo que sigue a o que lo precede.  
  
 Se devuelve una cadena vacía si el origen de datos no admite catálogos. Para determinar si se admiten los catálogos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_CATALOG_NAME. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá ".".  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_QUALIFIER_NAME_SEPARATOR.  
  
 SQL_CATALOG_TERM(ODBC 1.0)  
 Una cadena de caracteres con el nombre del proveedor de origen de datos para un catálogo; Por ejemplo, "database" o "directory". Esta cadena puede ser en caso de la parte superior, inferior o mixto.  
  
 Se devuelve una cadena vacía si el origen de datos no admite catálogos. Para determinar si se admiten los catálogos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_CATALOG_NAME. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá "catálogo".  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_QUALIFIER_TERM.  
  
 SQL_CATALOG_USAGE(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las instrucciones en el que se pueden usar los catálogos.  
  
 Las máscaras de bits siguientes se usan para determinar dónde se pueden utilizar los catálogos:  
  
 SQL_CU_DML_STATEMENTS = los catálogos se admiten en todas las instrucciones de lenguaje de manipulación de datos: **Seleccione**, **insertar**, **actualizar**, **eliminar**y si se admite, **seleccione para actualizar** y posicionadas update y delete instrucciones.  
  
 SQL_CU_PROCEDURE_INVOCATION = se admiten los catálogos en la instrucción de invocación del procedimiento ODBC.  
  
 SQL_CU_TABLE_DEFINITION = los catálogos se admiten en todas las instrucciones de definición de tabla: **CREAR una tabla**, **Crear vista**, **ALTER TABLE**, **DROP TABLE**, y **DROP VIEW**.  
  
 SQL_CU_INDEX_DEFINITION = los catálogos se admiten en todas las instrucciones de definición de índice: **Crear índice** y **DROP INDEX**.  
  
 SQL_CU_PRIVILEGE_DEFINITION = los catálogos se admiten en todas las instrucciones de definición de privilegios: **GRANT** y **REVOCAR**.  
  
 Se devuelve un valor de 0 si el origen de datos no admite catálogos. Para determinar si se admiten los catálogos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_CATALOG_NAME. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá una máscara de bits con todos estos conjuntos de bits.  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_QUALIFIER_USAGE.  
  
 SQL_COLLATION_SEQ(ODBC 3.0)  
 El nombre de la secuencia de intercalación. Se trata de una cadena de caracteres que indica el nombre de la intercalación predeterminada para el carácter predeterminado establecido para este servidor (por ejemplo, ' ISO 8859-1' o EBCDIC). Si es desconocido, se devolverá una cadena vacía. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá una cadena no vacía.  
  
 SQL_COLUMN_ALIAS(ODBC 2.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite los alias de columna; en caso contrario, "N".  
  
 Un alias de columna es un nombre alternativo que se puede especificar para una columna en la lista de selección mediante el uso de una cláusula AS. Un controlador de función de nivel básico de SQL-92 siempre devolverá "S".  
  
 SQL_CONCAT_NULL_BEHAVIOR(ODBC 1.0)  
 Un valor SQLUSMALLINT que indica cómo el origen de datos controla la concatenación de NULL con valores de columnas de tipo de datos de caracteres con columnas de tipo de datos de caracteres con valores distintos de NULL:  
  
 SQL_CB_NULL = resultado es NULL con valores.  
  
 SQL_CB_NON_NULL = resultado es la concatenación de columnas con valores distintos de NULL.  
  
 SQL_CB_NULL siempre devuelve un controlador de función de nivel básico de SQL-92.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_ DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 Una máscara de bits SQLUINTEGER. La máscara de bits indica las conversiones compatibles con el origen de datos con el **convertir** función escalar para los datos del tipo con nombre en el *InfoType*. Si la máscara de bits es igual a cero, el origen de datos no admite las conversiones de datos del tipo con nombre, incluida la conversión en el mismo tipo de datos.  
  
 Por ejemplo, para determinar si un origen de datos admite la conversión de datos SQL_INTEGER al tipo de datos SQL_BIGINT, llama una aplicación **SQLGetInfo** con el *InfoType* de SQL_CONVERT_INTEGER. La aplicación realiza una **AND** operación con la máscara de bits devuelta y SQL_CVT_BIGINT. Si el valor resultante es distinto de cero, se admite la conversión.  
  
 Las máscaras de bits siguientes se usan para determinar qué conversiones se admiten:  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL SQL_CVT_ DE _CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) SQL_CVT_LONGVARBINARY (ODBC 1.0) (ODBC 1.0) SQL_CVT_LONGVARCHAR SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) (ODBC 1.0) SQL_CVT_SMALLINT SQL_CVT_TIME (ODBC 1.0) MARCA DE TIEMPO (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS(ODBC 1.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones de conversión escalares admitidas por el controlador y el origen de datos asociado.  
  
 La siguiente máscara de bits se usa para determinar qué funciones de conversión son compatibles con:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME(ODBC 1.0)  
 Un valor SQLUSMALLINT que indica si se admiten nombres de correlación de tabla:  
  
 SQL_CN_NONE = no se admiten nombres de correlación.  
  
 SQL_CN_DIFFERENT = correlación nombres se admiten, pero deben diferir de los nombres de las tablas que representan.  
  
 SQL_CN_ANY = correlación nombres se admiten y pueden tener cualquier nombre válido definido por el usuario.  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá SQL_CN_ANY.  
  
 SQL_CREATE_ASSERTION(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **crear aserción** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_CA_CREATE_ASSERTION  
  
 Los bits siguientes especifican el atributo de restricción admitido si se admite la capacidad de especificar explícitamente los atributos de las restricciones (vea los tipos de información SQL_ALTER_TABLE y SQL_CREATE_TABLE):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones como compatible. Un valor devuelto de "0" significa que el **crear aserción** no se admite la instrucción.  
  
 SQL_CREATE_CHARACTER_SET(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **crear el juego de caracteres** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones como compatible. Un valor devuelto de "0" significa que el **crear el juego de caracteres** no se admite la instrucción.  
  
 SQL_CREATE_COLLATION(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **crear intercalación** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 La siguiente máscara de bits se usa para determinar qué cláusulas son compatibles con:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como compatible. Un valor devuelto de "0" significa que el **crear intercalación** no se admite la instrucción.  
  
 SQL_CREATE_DOMAIN(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **crear dominio** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_CDO_CREATE_DOMAIN = crear el dominio se admite la instrucción (nivel intermedio).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<definición del nombre de restricción > se admite para asignar nombres a las restricciones de dominio (nivel intermedio).  
  
 Los bits siguientes especifican la capacidad para crear las restricciones de columna: SQL_CDO_DEFAULT = se permite especificar las restricciones de dominio (nivel intermedio) SQL_CDO_CONSTRAINT = se permite especificar valores predeterminados de dominio (nivel intermedio) SQL_CDO_COLLATION = Se admite la especificación de intercalación de dominio (nivel total)  
  
 Los bits siguientes especifican los atributos de restricción compatibles si se admite la especificación de restricciones de dominio (se establece SQL_CDO_DEFAULT):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (nivel completo) SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (nivel completo) (nivel Full) SQL_CDO_CONSTRAINT_DEFERRABLE SQL_CDO_CONSTRAINT_NON_DEFERRABLE (nivel completo)  
  
 Un valor devuelto de "0" significa que el **crear dominio** no se admite la instrucción.  
  
 SQL_CREATE_SCHEMA(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **CREATE SCHEMA** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Un controlador de función de nivel intermedio de SQL-92 siempre devolverá las opciones SQL_CS_CREATE_SCHEMA y SQL_CS_AUTHORIZATION como compatible. Estos también se deben admitir en el nivel de entrada de SQL-92, pero no necesariamente como instrucciones SQL. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones como compatible.  
  
 SQL_CREATE_TABLE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **CREATE TABLE** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_CT_CREATE_TABLE = CREATE TABLE de la instrucción se admite. (Nivel de entrada)  
  
 SQL_CT_TABLE_CONSTRAINT = se admite la especificación de restricciones de tabla (nivel FIPS transitorio)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION = el \<definición del nombre de restricción > se admite la cláusula para asignar nombres a las restricciones de columna y tabla (nivel intermedio)  
  
 Los bits siguientes especifican la capacidad para crear tablas temporales:  
  
 SQL_CT_COMMIT_PRESERVE = eliminados se conservan las filas en la confirmación. (Nivel completo) SQL_CT_COMMIT_DELETE = eliminadas las filas se eliminan en la confirmación. (Nivel completo) SQL_CT_GLOBAL_TEMPORARY = Global se pueden crear tablas temporales. (Nivel completo) SQL_CT_LOCAL_TEMPORARY = Local se pueden crear tablas temporales. (Nivel completo)  
  
 Los bits siguientes especifican la capacidad para crear restricciones de columna:  
  
 SQL_CT_COLUMN_CONSTRAINT = se admite la especificación de restricciones de columna (nivel FIPS transitorio) SQL_CT_COLUMN_DEFAULT = se permite especificar valores predeterminados de columna (nivel FIPS transitorio) SQL_CT_COLUMN_COLLATION = es especificar la intercalación de columnas compatible (nivel completo)  
  
 Los bits siguientes especifican los atributos de restricción compatibles si se admite la especificación de restricciones de columna o tabla:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (nivel completo) SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (nivel completo) (nivel Full) SQL_CT_CONSTRAINT_DEFERRABLE SQL_CT_CONSTRAINT_NON_DEFERRABLE (nivel completo)  
  
 SQL_CREATE_TRANSLATION(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **crear traducción** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 La siguiente máscara de bits se usa para determinar qué cláusulas son compatibles con:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá estas opciones como compatible. Un valor devuelto de "0" significa que el **crear traducción** no se admite la instrucción.  
  
 SQL_CREATE_VIEW(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **CREATE VIEW** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Un valor devuelto de "0" significa que el **CREATE VIEW** no se admite la instrucción.  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá las opciones SQL_CV_CREATE_VIEW y SQL_CV_CHECK_OPTION como compatible.  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones como compatible.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR(ODBC 1.0)  
 Un valor SQLUSMALLINT que indica cómo un **confirmación** operación afecta a los cursores y las instrucciones preparadas en el origen de datos (el comportamiento del origen de datos cuando se confirma una transacción).  
  
 El valor de este atributo refleja el estado actual de la configuración siguiente: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE = cursores cerrados y eliminar las instrucciones preparadas. De nuevo, para usar el cursor de la aplicación debe reprepare y vuelva a ejecutar la instrucción.  
  
 SQL_CB_CLOSE = cerrados cursores. Para instrucciones preparadas, la aplicación puede llamar a **SQLExecute** en la instrucción sin llamar a **SQLPrepare** nuevo. El valor predeterminado para el controlador ODBC de SQL es SQL_CB_CLOSE. Esto significa que el controlador ODBC de SQL cerrará los cursores al confirmar una transacción.  
  
 SQL_CB_PRESERVE = Preserve cursores en la misma posición que antes el **confirmar** operación. La aplicación puede seguir capturar los datos, o puede cerrar el cursor y volver a ejecutar la instrucción sin necesidad de volver a la preparación.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR(ODBC 1.0)  
 Un valor SQLUSMALLINT que indica cómo un **reversión** operación afecta a los cursores y las instrucciones preparadas en el origen de datos:  
  
 SQL_CB_DELETE = cursores cerrados y eliminar las instrucciones preparadas. De nuevo, para usar el cursor de la aplicación debe reprepare y vuelva a ejecutar la instrucción.  
  
 SQL_CB_CLOSE = cerrados cursores. Para instrucciones preparadas, la aplicación puede llamar a **SQLExecute** en la instrucción sin llamar a **SQLPrepare** nuevo.  
  
 SQL_CB_PRESERVE = Preserve cursores en la misma posición que antes el **reversión** operación. La aplicación puede seguir capturar los datos, o puede cerrar el cursor y ejecutar de nuevo la instrucción sin lo repreparing.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 Un valor SQLUINTEGER que indica la compatibilidad de sensibilidad de cursor:  
  
 SQL_INSENSITIVE = todos los cursores de la presentación de identificador de instrucción, el conjunto de resultados sin reflejar los cambios realizados en él por cualquier otro cursor en la misma transacción.  
  
 SQL_UNSPECIFIED = no se especifica si la cursores en el identificador de instrucción hacer visibles los cambios realizados en un conjunto de resultados por otro cursor en la misma transacción. Los cursores en el identificador de instrucción pueden hacer visible ninguno, algunos o todos los cambios.  
  
 SQL_SENSITIVE = cursores son sensibles a los cambios realizados por otros cursores en la misma transacción.  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá la opción SQL_UNSPECIFIED como compatible.  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá la opción SQL_INSENSITIVE como compatible.  
  
 SQL_DATA_SOURCE_NAME(ODBC 1.0)  
 Una cadena de caracteres con el nombre del origen de datos que se usó durante la conexión. Si la aplicación llama a **SQLConnect**, este es el valor de la *szDSN* argumento. Si la aplicación llama a **SQLDriverConnect** o **SQLBrowseConnect**, este es el valor de la palabra clave DSN en la cadena de conexión que se pasan al controlador. Si la cadena de conexión no contiene el **DSN** palabra clave (por ejemplo, cuando no contiene el **controlador** palabra clave), se trata de una cadena vacía.  
  
 SQL_DATA_SOURCE_READ_ONLY(ODBC 1.0)  
 Una cadena de caracteres. "Y" si el origen de datos está establecido en modo de solo lectura de "N" si es lo contrario.  
  
 Esta característica solo incluye el origen de datos; no es una característica del controlador que permite el acceso al origen de datos. Un controlador de lectura/escritura puede utilizarse con un origen de datos es de solo lectura. Si un controlador es de solo lectura, todos sus orígenes de datos deben ser de solo lectura y deben devolver SQL_DATA_SOURCE_READ_ONLY.  
  
 SQL_DATABASE_NAME(ODBC 1.0)  
 Un carácter de cadena con el nombre de la base de datos actual en uso, si el origen de datos define un objeto con nombre denominado "base de datos".  
  
> [!NOTE]
>  En ODBC 3 *.x*, el valor devuelto para este *InfoType* también pueden ser devueltos por una llamada a **SQLGetConnectAttr** con un *atributo* argumento de SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerando los literales de datetime de SQL-92 admitidos por el origen de datos. Tenga en cuenta que estos son los literales de fecha y hora que aparecen en la especificación de SQL-92 y son independientes de las cláusulas de escape literal de fecha y hora definidas por ODBC. Para obtener más información acerca de las cláusulas de escape ODBC literales de fecha y hora, vea [fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Un controlador de función de nivel FIPS transitorias siempre devolverá el valor "1" en la máscara de bits para los bits de la lista siguiente. Un valor de "0" significa que no se admiten los literales de datetime de SQL-92.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué literales son compatibles con:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_ SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME(ODBC 1.0)  
 Con el nombre del producto DBMS, el controlador obtiene acceso a una cadena de caracteres.  
  
 SQL_DBMS_VER(ODBC 1.0)  
 Una cadena de caracteres que indica la versión del producto DBMS acceder el controlador. La versión tiene el formato ##. ##. ###, donde los dos primeros dígitos son la versión principal, los dos dígitos son la versión secundaria y los cuatro últimos dígitos son la versión de lanzamiento. El controlador debe presentar la versión de producto DBMS en este formulario, pero también puede anexar versión del DBMS específicos de cada producto. Por ejemplo, "04.01.0000 Rdb 4.1".  
  
 SQL_DDL_INDEX(ODBC 3.0)  
 Un valor SQLUINTEGER que indica compatibilidad para la creación y eliminación de índices:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION(ODBC 1.0)  
 Un valor SQLUINTEGER que indica que el nivel de aislamiento de transacción predeterminado compatible con el controlador u origen de datos, o cero si el origen de datos no admite transacciones. Los siguientes términos se usan para definir los niveles de aislamiento de transacción:  
  
 **Lectura de datos sucios** 1 transacción cambia una fila. La transacción 2 lee la fila modificada antes de que el cambio confirma la transacción 1. Si la transacción 1 revierte el cambio, la transacción 2 habrá leer una fila que se considera que nunca han existido.  
  
 **Lectura irrepetible** 1 transacción lee una fila. La transacción 2 se actualiza o elimina esa fila y este cambio confirma. Si la transacción 1 intenta volver a leer la fila, recibirán los valores de fila diferente o detectar que se ha eliminado la fila.  
  
 **Filas fantasma** 1 transacción lee un conjunto de filas que cumplen algunos criterios de búsqueda. La transacción 2 genera una o varias filas (a través de inserciones o actualizaciones) que coinciden con los criterios de búsqueda. Si la transacción 1 reexecutes la instrucción que lee las filas, recibe un conjunto diferente de filas.  
  
 Si el origen de datos admite transacciones, el controlador devuelve una de las máscaras de bits siguientes:  
  
 SQL_TXN_READ_UNCOMMITTED = Dirty es posible las lecturas, lecturas no repetibles y fantasma.  
  
 SQL_TXN_READ_COMMITTED = Dirty lecturas no son posibles. Lecturas no repetibles y fantasma es posible.  
  
 SQL_TXN_REPEATABLE_READ = Dirty lecturas no repetibles y lecturas no son posibles. Fantasmas son posibles.  
  
 SQL_TXN_SERIALIZABLE = transacciones son serializables. Las transacciones serializables no permiten lecturas no actualizadas, lecturas no repetibles o fantasmas.  
  
 SQL_DESCRIBE_PARAMETER(ODBC 3.0)  
 Una cadena de caracteres: "Y" si se pueden describir los parámetros; "N", si no lo es.  
  
 Un controlador compatible con el nivel completo de SQL-92 normalmente devolverá "S" porque admitirá la **describen entrada** instrucción. Dado que esto no especifica directamente del soporte de SQL subyacente, sin embargo, con descripciones de parámetros podrían no admitirse, incluso en un controlador compatible con el nivel completo de SQL-92.  
  
 SQL_DM_VER(ODBC 3.0)  
 Una cadena de caracteres con la versión del Administrador de controladores. La versión tiene el formato ##. ##. ###. ###, donde:  
  
 El primer conjunto de dos dígitos es la versión principal de ODBC, como se indica por la constante SQL_SPEC_MAJOR.  
  
 El segundo conjunto de dos dígitos es la versión secundaria de ODBC, como se indica por la constante SQL_SPEC_MINOR.  
  
 El tercer conjunto de cuatro dígitos es el número de compilación de versión principal del Administrador de controladores.  
  
 El último conjunto de cuatro dígitos es el número de compilación secundaria del Administrador de controladores.  
  
 La versión del Administrador de controladores de Windows 7 es 03.80. La versión del Administrador de controladores de Windows 8 es 03.81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 Un valor SQLUINTEGER que indica si el controlador admite la agrupación dependientes del controlador. (Para obtener más información, consulte [Driver-Aware Connection Pooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE indica que el controlador puede admitir el mecanismo de agrupación dependientes del controlador.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE indica que el controlador no admite el mecanismo de agrupación dependientes del controlador.  
  
 No es necesario implementar SQL_DRIVER_AWARE_POOLING_SUPPORTED un controlador y el Administrador de controladores no cumplirá al valor devuelto del controlador.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV(ODBC 1.0)  
 Identificador de entorno o identificador de conexión, determinada por el argumento de un valor SQLULEN, el controlador *InfoType*.  
  
 Estos tipos de información se implementan mediante el Administrador de controladores por sí solo.  
  
 SQL_DRIVER_HDESC(ODBC 3.0)  
 Valor de un SQLULEN, identificador de descriptor del controlador determinado por el identificador de descriptor del Administrador de controladores, que se debe pasar en la entrada en \* *InfoValuePtr* desde la aplicación. En este caso, *InfoValuePtr* es un argumento de entrada y salido. El identificador de descriptor de entrada pasa en \* *InfoValuePtr* debe haberse explícita o implícitamente asignado en el *ConnectionHandle*.  
  
 La aplicación debe realizar una copia del descriptor del Administrador de controladores de controlar antes de llamar a **SQLGetInfo** con este tipo de información para asegurarse de que el identificador no se sobrescribe en la salida.  
  
 Este tipo de información se implementa mediante el Administrador de controladores por sí solo.  
  
 SQL_DRIVER_HLIB(ODBC 2.0)  
 Un valor SQLULEN, el *hinst* desde la biblioteca de carga devuelve el Administrador de controladores cuando cargue la DLL del controlador en un sistema operativo de Microsoft Windows, o su equivalente en otro sistema operativo. El identificador es válido sólo para el identificador de conexión especificado en la llamada a **SQLGetInfo**.  
  
 Este tipo de información se implementa mediante el Administrador de controladores por sí solo.  
  
 SQL_DRIVER_HSTMT(ODBC 1.0)  
 Valor de un SQLULEN, identificador de instrucción del controlador determinado por el identificador de instrucción del Administrador de controladores, que se debe pasar en la entrada en \* *InfoValuePtr* desde la aplicación. En este caso, *InfoValuePtr* es una entrada y un argumento de salida. Pasa el identificador de instrucción entrada \* *InfoValuePtr* debe haberse asignado en el argumento *ConnectionHandle*.  
  
 La aplicación debe realizar una copia de la instrucción del Administrador de controladores controlar antes de llamar a **SQLGetInfo** con este tipo de información para asegurarse de que el identificador no se sobrescribe en la salida.  
  
 Este tipo de información se implementa mediante el Administrador de controladores por sí solo.  
  
 SQL_DRIVER_NAME(ODBC 1.0)  
 Una cadena de caracteres con el nombre de archivo del controlador se utiliza para acceder al origen de datos.  
  
 SQL_DRIVER_ODBC_VER(ODBC 2.0)  
 Una cadena de caracteres con la versión de ODBC que admite el controlador. La versión tiene el formato ##. ##, donde los dos primeros dígitos son la versión principal y los dos dígitos son la versión secundaria. SQL_SPEC_MAJOR y SQL_SPEC_MINOR definen los números de versión principal y secundaria. Para la versión de ODBC que se describe en este manual, estas son 3 y 0, y el controlador debería devolver "03.00".  
  
 El Administrador de controladores ODBC no modificará el valor devuelto de SQLGetInfo(SQL_DRIVER_ODBC_VER) para mantener la compatibilidad con versiones anteriores de las aplicaciones existentes. El controlador especifica qué valor se devolverá. Sin embargo, un controlador que respalda la extensibilidad de tipo de datos C debe devolver 3,8 (o superior) cuando una aplicación llama a **SQLSetEnvAttr** establecer SQL_ATTR_ODBC_VERSION en 3.8. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER(ODBC 1.0)  
 Una cadena de caracteres con la versión del controlador y si lo desea, una descripción del controlador. Como mínimo, la versión tiene el formato ##. ##. ###, donde los dos primeros dígitos son la versión principal, los dos dígitos son la versión secundaria y los cuatro últimos dígitos son la versión de lanzamiento.  
  
 SQL_DROP_ASSERTION(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **DROP aserción** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 La siguiente máscara de bits se usa para determinar qué cláusulas son compatibles con:  
  
 SQL_DA_DROP_ASSERTION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como compatible.  
  
 SQL_DROP_CHARACTER_SET(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **quitar del juego de caracteres** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 La siguiente máscara de bits se usa para determinar qué cláusulas son compatibles con:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como compatible.  
  
 SQL_DROP_COLLATION(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **DROP intercalación** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 La siguiente máscara de bits se usa para determinar qué cláusulas son compatibles con:  
  
 SQL_DC_DROP_COLLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como compatible.  
  
 SQL_DROP_DOMAIN(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **Quitar dominio** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Un controlador de función de nivel intermedio de SQL-92 siempre devolverá todas estas opciones como compatible.  
  
 SQL_DROP_SCHEMA(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **DROP SCHEMA** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Un controlador de función de nivel intermedio de SQL-92 siempre devolverá todas estas opciones como compatible.  
  
 SQL_DROP_TABLE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **DROP TABLE** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Un controlador de nivel compatibles con FIPS transitorio siempre devolverá todas estas opciones como compatible.  
  
 SQL_DROP_TRANSLATION(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **traducción DROP** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 La siguiente máscara de bits se usa para determinar qué cláusulas son compatibles con:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como compatible.  
  
 SQL_DROP_VIEW(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **DROP VIEW** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Un controlador de nivel compatibles con FIPS transitorio siempre devolverá todas estas opciones como compatible.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor dinámico que son compatibles con el controlador. Esta máscara de bits contiene el subconjunto de atributos; primera para el segundo subconjunto, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 Las máscaras de bits siguientes se utilizan para determinar los atributos que son compatibles con:  
  
 SQL_CA1_NEXT = un *FetchOrientation* es compatible con una llamada al argumento de SQL_FETCH_NEXT **SQLFetchScroll** cuando el cursor es dinámico.  
  
 SQL_CA1_ABSOLUTE = *FetchOrientation* argumentos de SQL_FETCH_FIRST, SQL_FETCH_LAST y SQL_FETCH_ABSOLUTE se admiten en una llamada a **SQLFetchScroll** cuando el cursor es dinámico. (El conjunto de filas que se capturarán es independiente de la posición actual del cursor).  
  
 SQL_CA1_RELATIVE = *FetchOrientation* argumentos de SQL_FETCH_PRIOR y SQL_FETCH_RELATIVE se admiten en una llamada a **SQLFetchScroll** cuando el cursor es dinámico. (El conjunto de filas que se capturarán depende de la posición actual del cursor. Tenga en cuenta que esto se separa de SQL_FETCH_NEXT porque en un cursor de avance y solo se admite solo SQL_FETCH_NEXT.)  
  
 SQL_CA1_BOOKMARK = un *FetchOrientation* es compatible con una llamada al argumento de SQL_FETCH_BOOKMARK **SQLFetchScroll** cuando el cursor es dinámico.  
  
 SQL_CA1_LOCK_EXCLUSIVE = un *LockType* es compatible con una llamada al argumento de SQL_LOCK_EXCLUSIVE **SQLSetPos** cuando el cursor es dinámico.  
  
 SQL_CA1_LOCK_NO_CHANGE = un *LockType* es compatible con una llamada al argumento de SQL_LOCK_NO_CHANGE **SQLSetPos** cuando el cursor es dinámico.  
  
 SQL_CA1_LOCK_UNLOCK = un *LockType* es compatible con una llamada al argumento de SQL_LOCK_UNLOCK **SQLSetPos** cuando el cursor es dinámico.  
  
 SQL_CA1_POS_POSITION = un *operación* es compatible con una llamada al argumento de SQL_POSITION **SQLSetPos** cuando el cursor es dinámico.  
  
 SQL_CA1_POS_UPDATE = un *operación* es compatible con una llamada al argumento de SQL_UPDATE **SQLSetPos** cuando el cursor es dinámico.  
  
 SQL_CA1_POS_DELETE = un *operación* es compatible con una llamada al argumento de SQL_DELETE **SQLSetPos** cuando el cursor es dinámico.  
  
 SQL_CA1_POS_REFRESH = un *operación* es compatible con una llamada al argumento de SQL_REFRESH **SQLSetPos** cuando el cursor es dinámico.  
  
 SQL_CA1_POSITIONED_UPDATE = una actualización donde actual de SQL se admite la instrucción cuando el cursor es dinámico. (Un controlador de función de nivel básico de SQL-92 siempre devolverá esta opción como compatible.)  
  
 SQL_CA1_POSITIONED_DELETE = A eliminar donde actual de SQL se admite la instrucción cuando el cursor es dinámico. (Un controlador de función de nivel básico de SQL-92 siempre devolverá esta opción como compatible.)  
  
 SQL_CA1_SELECT_FOR_UPDATE = una instrucción SELECT para la instrucción UPDATE de SQL se admite cuando el cursor es dinámico. (Un controlador de función de nivel básico de SQL-92 siempre devolverá esta opción como compatible.)  
  
 SQL_CA1_BULK_ADD = un *operación* es compatible con una llamada al argumento de SQL_ADD **SQLBulkOperations** cuando el cursor es dinámico.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = un *operación* es compatible con una llamada al argumento de SQL_UPDATE_BY_BOOKMARK **SQLBulkOperations** cuando el cursor es dinámico.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = un *operación* es compatible con una llamada al argumento de SQL_DELETE_BY_BOOKMARK **SQLBulkOperations** cuando el cursor es dinámico.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = un *operación* es compatible con una llamada al argumento de SQL_FETCH_BY_BOOKMARK **SQLBulkOperations** cuando el cursor es dinámico.  
  
 Un controlador de función de nivel intermedio de SQL-92 normalmente devolverá las opciones SQL_CA1_NEXT, SQL_CA1_ABSOLUTE y SQL_CA1_RELATIVE como compatible, ya que admite cursores desplazables a través de la instrucción FETCH SQL incrustada. Ya que esto no determina directamente del soporte de SQL subyacente, sin embargo, los cursores desplazables pueden no ser compatibles, incluso para un controlador de función de nivel intermedio de SQL-92.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor dinámico que son compatibles con el controlador. Esta máscara de bits contiene el subconjunto de segundo de los atributos. para el subconjunto de la primera, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 Las máscaras de bits siguientes se utilizan para determinar los atributos que son compatibles con:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = solo lectura cursor dinámico, en el que no se permiten actualizaciones, se admite. (El atributo de instrucción SQL_ATTR_CONCURRENCY puede ser SQL_CONCUR_READ_ONLY para un cursor dinámico).  
  
 SQL_CA2_LOCK_CONCURRENCY = un cursor dinámico que utiliza el nivel más bajo de bloqueo suficiente para asegurarse de que se admite que se puede actualizar la fila. (El atributo de instrucción SQL_ATTR_CONCURRENCY puede ser SQL_CONCUR_LOCK para un cursor dinámico). Estos bloqueos deben ser coherentes con el nivel de aislamiento de transacción establecido por el atributo de conexión SQL_ATTR_TXN_ISOLATION.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = un cursor dinámico que usa las versiones de fila de comparación de control de simultaneidad optimista es compatible. (El atributo de instrucción SQL_ATTR_CONCURRENCY puede ser SQL_CONCUR_ROWVER para un cursor dinámico).  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = un cursor dinámico que usa los valores de comparación de control de simultaneidad optimista es compatible. (El atributo de instrucción SQL_ATTR_CONCURRENCY puede ser SQL_CONCUR_VALUES para un cursor dinámico).  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = agregado filas son visibles para un cursor dinámico; el cursor puede desplazarse a las filas. (Donde se agregan estas filas hasta el cursor es dependiente del controlador).  
  
 SQL_CA2_SENSITIVITY_DELETIONS = Deleted filas ya no están disponibles para un cursor dinámico y no deje un "agujero" en el conjunto de resultados; una vez que se desplaza el cursor dinámico de una fila eliminada, éste no se puede volver a esa fila.  
  
 SQL_CA2_SENSITIVITY_UPDATES = las actualizaciones a las filas son visibles en un cursor dinámico; Si el cursor dinámico se desplaza desde y se devuelve a la fila actualizada, los datos devueltos por el cursor son los datos actualizados, no los datos originales.  
  
 SQL_CA2_MAX_ROWS_SELECT = afecta al atributo de instrucción The SQL_ATTR_MAX_ROWS **seleccione** instrucciones cuando el cursor es dinámico.  
  
 SQL_CA2_MAX_ROWS_INSERT = afecta al atributo de instrucción The SQL_ATTR_MAX_ROWS **insertar** instrucciones cuando el cursor es dinámico.  
  
 SQL_CA2_MAX_ROWS_DELETE = afecta al atributo de instrucción The SQL_ATTR_MAX_ROWS **eliminar** instrucciones cuando el cursor es dinámico.  
  
 SQL_CA2_MAX_ROWS_UPDATE = afecta al atributo de instrucción The SQL_ATTR_MAX_ROWS **actualización** instrucciones cuando el cursor es dinámico.  
  
 SQL_CA2_MAX_ROWS_CATALOG = afecta al atributo de instrucción The SQL_ATTR_MAX_ROWS **catálogo** conjuntos de resultados cuando el cursor es dinámico.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = afecta al atributo de instrucción The SQL_ATTR_MAX_ROWS **seleccione**, **insertar**, **eliminar**, y **actualización** las instrucciones, y **catálogo** conjuntos, de resultados cuando el cursor es dinámico.  
  
 SQL_CA2_CRC_EXACT = exactamente recuento de filas está disponible en el campo de diagnóstico SQL_DIAG_CURSOR_ROW_COUNT cuando el cursor es dinámico.  
  
 SQL_CA2_CRC_APPROXIMATE = un valor aproximado recuento de filas está disponible en el campo de diagnóstico SQL_DIAG_CURSOR_ROW_COUNT cuando el cursor es dinámico.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = el controlador garantiza que simula actualización por posición o las instrucciones delete afectará solo una fila cuando el cursor es dinámico; es responsabilidad de la aplicación para garantizar esto. (Si una instrucción afecta a más de una fila, **SQLExecute** o **SQLExecDirect** devuelve SQLSTATE 01001 [conflicto de operación de Cursor].) Para establecer este comportamiento, la aplicación llama a **SQLSetStmtAttr** con el SQL_ATTR_SIMULATE_CURSOR atributo SQL_SC_NON_UNIQUE.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = el controlador intenta garantizar que actualización posicionada simulado o las instrucciones delete afectará solo una fila cuando el cursor es dinámico. El controlador siempre ejecuta estas instrucciones, aunque es posible que afectan a más de una fila, por ejemplo, cuando no hay ninguna clave única. (Si una instrucción afecta a más de una fila, **SQLExecute** o **SQLExecDirect** devuelve SQLSTATE 01001 [conflicto de operación de Cursor].) Para establecer este comportamiento, la aplicación llama a **SQLSetStmtAttr** con el SQL_ATTR_SIMULATE_CURSOR atributo SQL_SC_TRY_UNIQUE.  
  
 SQL_CA2_SIMULATE_UNIQUE = el controlador garantiza que simula actualización por posición o las instrucciones delete afectará solo una fila cuando el cursor es dinámico. Si el controlador no puede garantizar en una instrucción determinada, **SQLExecDirect** o **SQLPrepare** devolver SQLSTATE 01001 (conflicto de operación de Cursor). Para establecer este comportamiento, la aplicación llama a **SQLSetStmtAttr** con el SQL_ATTR_SIMULATE_CURSOR atributo SQL_SC_UNIQUE.  
  
 SQL_EXPRESSIONS_IN_ORDERBY(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite expresiones en el **ORDER BY** lista; "N" Si no es así.  
  
 SQL_FILE_USAGE(ODBC 2.0)  
 Un valor SQLUSMALLINT que indica el modo en que un controlador de nivel único trata directamente los archivos en un origen de datos:  
  
 SQL_FILE_NOT_SUPPORTED = el controlador no es un único nivel. Por ejemplo, un controlador ORACLE es un controlador de dos niveles.  
  
 SQL_FILE_TABLE = un nivel único controlador trata los archivos en un origen de datos como tablas. Por ejemplo, un controlador de Xbase trata cada archivo Xbase como una tabla.  
  
 SQL_FILE_CATALOG = un nivel único controlador trata los archivos en un origen de datos como un catálogo. Por ejemplo, un controlador de Microsoft Access trata cada archivo de Microsoft Access como una base de datos completa.  
  
 Una aplicación puede utilizar esto para determinar cómo seleccionarán los usuarios los datos. Por ejemplo, los usuarios de Xbase a menudo pensar datos tal como se almacena en archivos, mientras que los usuarios ORACLE y Microsoft Access generalmente se considera datos tal como se almacena en tablas.  
  
 Cuando un usuario selecciona un origen de datos de Xbase, la aplicación podría mostrar el Windows **abrir archivo** cuadro de diálogo común; cuando el usuario selecciona un origen de datos Microsoft Access u ORACLE, la aplicación podría mostrar un personalizado  **Seleccionar tabla** cuadro de diálogo.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor de solo avance que son compatibles con el controlador. Esta máscara de bits contiene el subconjunto de atributos; primera para el segundo subconjunto, consulte SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 Las máscaras de bits siguientes se utilizan para determinar los atributos que son compatibles con:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_ UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (y sustituya "forward-only cursor" para "cursor dinámico" en las descripciones).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor de solo avance que son compatibles con el controlador. Esta máscara de bits contiene el subconjunto de segundo de los atributos. para el subconjunto de la primera, consulte SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 Las máscaras de bits siguientes se utilizan para determinar los atributos que son compatibles con:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (y sustituya "forward-only cursor" para "cursor dinámico" en las descripciones).  
  
 SQL_GETDATA_EXTENSIONS(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar extensiones de **SQLGetData**.  
  
 Las máscaras de bits siguientes se usan junto con la marca para determinar qué extensiones comunes para el controlador admite para **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData** se puede llamar para cualquier columna sin enlazar, las incluidas antes de la última columna enlazada. Tenga en cuenta que deben llamarse a las columnas en orden ascendente de número de columna, a menos que también se devuelve SQL_GD_ANY_ORDER.  
  
 SQL_GD_ANY_ORDER = **SQLGetData** se puede llamar a las columnas sin enlazar en cualquier orden. Tenga en cuenta que **SQLGetData** se puede llamar solo para las columnas después de la última columna enlazada a menos que también se devuelve SQL_GD_ANY_COLUMN.  
  
 SQL_GD_BLOCK = **SQLGetData** puede llamarse para una columna independiente de cualquier fila de un bloque (donde el tamaño del conjunto de filas es mayor que 1) de datos después de colocar esa fila con **SQLSetPos**.  
  
 SQL_GD_BOUND = **SQLGetData** se puede llamar a las columnas enlazadas, además de las columnas sin enlazar. Un controlador no puede devolver este valor a menos que también devuelve SQL_GD_ANY_COLUMN.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** se puede llamar para devolver valores de parámetro de salida. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **SQLGetData** es necesaria para devolver datos solo de las columnas sin enlazar que se producen después de la última columna, enlazada se llaman en orden creciente de número de columna y no están en una fila en un bloque de filas.  
  
 Si un controlador es compatible con marcadores (de longitud fija o de longitud variable), debe admitir llamada **SQLGetData** en la columna 0. Esta compatibilidad es necesaria, independientemente de lo que devuelve el controlador para una llamada a **SQLGetInfo** con el SQL_GETDATA_EXTENSIONS *InfoType*.  
  
 SQL_GROUP_BY(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica la relación entre las columnas de la **GROUP BY** cláusula y las columnas no agregadas en la lista de selección:  
  
 SQL_GB_COLLATE = un **COLLATE** se puede especificar la cláusula al final de cada columna de agrupamiento. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY** no se admiten las cláusulas. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = el **GROUP BY** cláusula debe contener todas las columnas no agregadas de la lista de selección. No puede contener cualquier otra columna. Por ejemplo, **seleccione DEPT, MAX(SALARY) de empleado GROUP BY departamento**. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = el **GROUP BY** cláusula debe contener todas las columnas no agregadas de la lista de selección. Puede contener columnas que no están en la lista de selección. Por ejemplo, **seleccione DEPT, MAX(SALARY) de empleado GROUP BY departamento, edad**. (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = las columnas de la **GROUP BY** cláusula y la lista de selección no están relacionados. El significado de nongrouped, sin agregadas columnas en la lista de selección es depende del origen de datos. Por ejemplo, **seleccione DEPT, salario del empleado GROUP BY departamento, edad**. (ODBC 2.0)  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá la opción SQL_GB_GROUP_BY_EQUALS_SELECT como compatible. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá la opción SQL_GB_COLLATE como compatible. Si no se admite ninguna de las opciones, el **GROUP BY** cláusula no es compatible con el origen de datos.  
  
 SQL_IDENTIFIER_CASE(ODBC 1.0)  
 Un SQLUSMALLINT valor como sigue:  
  
 SQL_IC_UPPER = los identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en mayúsculas en el catálogo del sistema.  
  
 SQL_IC_LOWER = identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en minúsculas en el catálogo del sistema.  
  
 Sql_ic_sensitive está = identificadores en SQL distinguen mayúsculas de minúsculas y se almacenan en mayúsculas y minúsculas mezcladas en el catálogo del sistema.  
  
 SQL_IC_MIXED = los identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en mayúsculas y minúsculas mezcladas en el catálogo del sistema.  
  
 Dado que los identificadores de SQL-92 nunca distinguen mayúsculas de minúsculas, un controlador que se ajusta estrictamente a SQL-92 (cualquier nivel) nunca devolverá la opción sql_ic_sensitive está ya admiten.  
  
 SQL_IDENTIFIER_QUOTE_CHAR(ODBC 1.0)  
 La cadena de caracteres que se usa como el delimitador inicial y final de un entre comillas (delimitado) identificador en instrucciones SQL. (Los identificadores que se pasan como argumentos a funciones ODBC no tienen que se entrecomillará.) Si el origen de datos no es compatible con los identificadores entre comillas, se devuelve un valor en blanco.  
  
 Esta cadena de caracteres puede usarse también para entrecomillar los argumentos de la función de catálogo cuando el atributo de conexión SQL_ATTR_METADATA_ID está establecido en SQL_TRUE.  
  
 Dado que el carácter de comilla del identificador de SQL-92 es las comillas dobles ("), un controlador que se ajusta estrictamente a SQL-92 siempre devolverá el carácter de comillas dobles.  
  
 SQL_INDEX_KEYWORDS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que enumera las palabras clave que son compatibles con el controlador en la instrucción CREATE INDEX:  
  
 SQL_IK_NONE = no se admite ninguna de las palabras clave.  
  
 SQL_IK_ASC = ASC se admite la palabra clave.  
  
 SQL_IK_DESC = DESC se admite la palabra clave.  
  
 SQL_IK_ALL = All se admiten palabras clave.  
  
 Para ver si se admite la instrucción CREATE INDEX, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_DLL_INDEX.  
  
 SQL_INFO_SCHEMA_VIEWS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las vistas INFORMATION_SCHEMA que son compatibles con el controlador. Las vistas y el contenido de, INFORMATION_SCHEMA son tal como se define en SQL-92.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se usan para determinar qué vistas se admiten:  
  
 SQL_ISV_ASSERTIONS = identifica las aserciones del catálogo que pertenecen a un usuario determinado. (Nivel completo)  
  
 SQL_ISV_CHARACTER_SETS = identifica juegos de caracteres del catálogo que se puede acceder a un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_CHECK_CONSTRAINTS = identifica la comprobación de restricciones que pertenecen a un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_COLLATIONS = identifica las intercalaciones de caracteres para el catálogo que se puede acceder a un usuario determinado. (Nivel completo)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = identifica las columnas para el catálogo que dependen de dominios definidos en el catálogo y que pertenecen a un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_COLUMN_PRIVILEGES = identifica los privilegios para columnas de las tablas persistentes que están disponibles en o concedido a un usuario determinado. (Nivel FIPS transitorio)  
  
 SQL_ISV_COLUMNS = identifica las columnas de las tablas persistentes que se pueden acceder a un usuario determinado. (Nivel FIPS transitorio)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = Similar a CONSTRAINT_TABLE_USAGE, vista, se identifican las columnas de las diversas restricciones que pertenecen a un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = identifica las tablas que se usan en las restricciones (referencial, único y aserciones) y son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = identifica las restricciones de dominio (de los dominios en el catálogo) que se pueden acceder a un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_DOMAINS = identifica los dominios definidos en un catálogo que se puede acceder el usuario. (Nivel intermedio)  
  
 SQL_ISV_KEY_COLUMN_USAGE = identifica las columnas definidas en el catálogo que un usuario determinado restringe como claves. (Nivel intermedio)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = identifica las restricciones referenciales que pertenecen a un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_SCHEMATA = identifica los esquemas que pertenecen a un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_SQL_LANGUAGES = identifica los niveles de compatibilidad de SQL, opciones y dialectos compatible con la implementación de SQL. (Nivel intermedio)  
  
 SQL_ISV_TABLE_CONSTRAINTS = identifica las restricciones de tabla que pertenecen a un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_TABLE_PRIVILEGES = identifica los privilegios para las tablas persistentes que están disponibles en o concedido a un usuario determinado. (Nivel FIPS transitorio)  
  
 SQL_ISV_TABLES = identifica las tablas persistentes definidas en un catálogo que se puede acceder a un usuario determinado. (Nivel FIPS transitorio)  
  
 SQL_ISV_TRANSLATIONS = identifica las traducciones de caracteres para el catálogo que se puede acceder a un usuario determinado. (Nivel completo)  
  
 SQL_ISV_USAGE_PRIVILEGES = identifica el uso de privilegios en los objetos de catálogo que están disponibles para o pertenecientes a un usuario determinado. (Nivel FIPS transitorio)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = identifica las columnas en el que el catálogo vistas que pertenecen a un usuario determinado son dependientes. (Nivel intermedio)  
  
 SQL_ISV_VIEW_TABLE_USAGE = identifica las tablas en la que el catálogo vistas que pertenecen a un usuario determinado son dependientes. (Nivel intermedio)  
  
 SQL_ISV_VIEWS = identifica las tablas visualizadas definidas en este catálogo que se puede acceder a un usuario determinado. (Nivel FIPS transitorio)  
  
 SQL_INSERT_STATEMENT(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que indica compatibilidad para **insertar** instrucciones:  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá todas estas opciones como compatible.  
  
 SQL_INTEGRITY(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite Integrity Enhancement Facility; "N" Si no es así.  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_ODBC_SQL_OPT_IEF.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de cursores que son compatibles con el controlador. Esta máscara de bits contiene el subconjunto de atributos; primera para el segundo subconjunto, consulte SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 Las máscaras de bits siguientes se utilizan para determinar los atributos que son compatibles con:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (y sustituya "cursor dinámico" para "cursor dinámico" en las descripciones).  
  
 Un controlador de función de nivel intermedio de SQL-92 normalmente devolverá las opciones SQL_CA1_NEXT, SQL_CA1_ABSOLUTE y SQL_CA1_RELATIVE como compatible, porque el controlador es compatible con los cursores desplazables a través de la instrucción FETCH SQL incrustada. Ya que esto no determina directamente del soporte de SQL subyacente, sin embargo, los cursores desplazables pueden no ser compatibles, incluso para un controlador de función de nivel intermedio de SQL-92.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de cursores que son compatibles con el controlador. Esta máscara de bits contiene el subconjunto de segundo de los atributos. para el subconjunto de la primera, consulte SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 Las máscaras de bits siguientes se utilizan para determinar los atributos que son compatibles con:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (y sustituya "cursor dinámico" para "cursor dinámico" en las descripciones).  
  
 SQL_KEYWORDS(ODBC 2.0)  
 Una cadena de caracteres que contiene una lista separada por comas de todas las palabras clave específicas del origen de datos. Esta lista no contiene palabras clave específicas de ODBC o palabras clave utilizadas por el origen de datos y ODBC. Esta lista representa todas las palabras clave reservadas; aplicaciones interoperables no deben usar estas palabras en los nombres de objeto.  
  
 Para obtener una lista de palabras clave ODBC, vea [palabras clave reservadas](../../../odbc/reference/appendixes/reserved-keywords.md) en [Apéndice C: Gramática de SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). El **#define** valor SQL_ODBC_KEYWORDS contiene una lista separada por comas de palabras clave de ODBC.  
  
 Apéndice C: Gramática de SQL  
  
 SQL_LIKE_ESCAPE_CLAUSE(ODBC 2.0)  
 Una cadena de caracteres: "Y" si el origen de datos es compatible con un carácter de escape para el carácter de porcentaje (%) y un carácter de subrayado (_) de caracteres en un **como** predicado y el controlador admite la sintaxis ODBC para definir un **como** predicado carácter de escape; "N" en caso contrario.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS(ODBC 3.0)  
 Un valor SQLUINTEGER que especifica el número máximo de instrucciones simultáneas activas en modo asincrónico que puede admitir el controlador en una conexión determinada. Si no hay ningún límite específico o el límite es desconocido, este valor es cero.  
  
 SQL_MAX_BINARY_LITERAL_LEN(ODBC 2.0)  
 Un valor SQLUINTEGER que especifica la longitud máxima (número de caracteres hexadecimales, excepto el prefijo de literal y el sufijo devuelto por **SQLGetTypeInfo**) de un literal binario de una instrucción SQL. Por ejemplo, el archivo binario 0xFFAA literal tiene una longitud de 4. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 SQL_MAX_CATALOG_NAME_LEN(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de catálogo en el origen de datos. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 Un controlador compatible con el nivel FIPS completa devuelve al menos 128.  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_MAX_QUALIFIER_NAME_LEN.  
  
 SQL_MAX_CHAR_LITERAL_LEN(ODBC 2.0)  
 Un valor SQLUINTEGER que especifica la longitud máxima (número de caracteres, sin incluir el prefijo de literal y el sufijo devuelto por **SQLGetTypeInfo**) de un carácter literal en una instrucción SQL. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 SQL_MAX_COLUMN_NAME_LEN(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de columna del origen de datos. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 Un controlador de entrada de FIPS nivel conforme devolverá como mínimo 18. Un controlador de función de nivel intermedio de FIPS devolverá al menos 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitido en un **GROUP BY** cláusula. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatibles con el nivel de entrada FIPS devolverá al menos 6. Un controlador de función de nivel intermedio de FIPS devolverá al menos 15.  
  
 SQL_MAX_COLUMNS_IN_INDEX(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitido en un índice. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitido en un **ORDER BY** cláusula. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatibles con el nivel de entrada FIPS devolverá al menos 6. Un controlador de función de nivel intermedio de FIPS devolverá al menos 15.  
  
 SQL_MAX_COLUMNS_IN_SELECT(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitido en una lista de selección. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatibles con el nivel de entrada FIPS devolverá al menos 100. Un controlador de función de nivel intermedio de FIPS devolverá al menos 250.  
  
 SQL_MAX_COLUMNS_IN_TABLE(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitido en una tabla. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatibles con el nivel de entrada FIPS devolverá al menos 100. Un controlador de función de nivel intermedio de FIPS devolverá al menos 250.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de instrucciones activas que admite el controlador para una conexión. Una instrucción se define como activo si tiene resultados pendientes, con el término "da como resultado" significado las filas de una **seleccione** operación o filas afectadas por una **insertar**, **actualización**, o **Eliminar** operación (por ejemplo, un recuento de filas), o si se encuentra en un estado NEED_DATA. Este valor puede reflejar una limitación impuesta por el controlador o el origen de datos. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_ACTIVE_STATEMENTS.  
  
 SQL_MAX_CURSOR_NAME_LEN(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de cursor en el origen de datos. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 Un controlador de entrada de FIPS nivel conforme devolverá como mínimo 18. Un controlador de función de nivel intermedio de FIPS devolverá al menos 128.  
  
 SQL_MAX_DRIVER_CONNECTIONS(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de conexiones activas que admite el controlador para un entorno. Este valor puede reflejar una limitación impuesta por el controlador o el origen de datos. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_ACTIVE_CONNECTIONS.  
  
 SQL_MAX_IDENTIFIER_LEN(ODBC 3.0)  
 Un SQLUSMALLINT que indica el tamaño máximo de caracteres que admite el origen de datos para los nombres definidos por el usuario.  
  
 Un controlador de entrada de FIPS nivel conforme devolverá como mínimo 18. Un controlador de función de nivel intermedio de FIPS devolverá al menos 128.  
  
 SQL_MAX_INDEX_SIZE(ODBC 2.0)  
 Un valor SQLUINTEGER que especifica el número máximo de bytes permitidos en los campos de un índice combinados. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 SQL_MAX_PROCEDURE_NAME_LEN(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de procedimiento en el origen de datos. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 SQL_MAX_ROW_SIZE(ODBC 2.0)  
 Un valor SQLUINTEGER que especifica la longitud máxima de una sola fila de una tabla. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatibles con el nivel de entrada FIPS devolverá por lo menos de 2.000. Un controlador de función de nivel intermedio de FIPS devolverá al menos 8000.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG(ODBC 3.0)  
 Una cadena de caracteres: "Y" si el tamaño máximo de filas devuelto por el tipo de información SQL_MAX_ROW_SIZE incluye la longitud de todos los SQL_LONGVARCHAR y SQL_LONGVARBINARY columnas en la fila; "N" en caso contrario.  
  
 SQL_MAX_SCHEMA_NAME_LEN(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de esquema del origen de datos. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 Un controlador de entrada de FIPS nivel conforme devolverá como mínimo 18. Un controlador de función de nivel intermedio de FIPS devolverá al menos 128.  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_MAX_OWNER_NAME_LEN.  
  
 SQL_MAX_STATEMENT_LEN(ODBC 2.0)  
 Un valor SQLUINTEGER que especifica la longitud máxima (número de caracteres, incluidos espacios en blanco) de una instrucción SQL. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 SQL_MAX_TABLE_NAME_LEN(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de tabla del origen de datos. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 Un controlador de entrada de FIPS nivel conforme devolverá como mínimo 18. Un controlador de función de nivel intermedio de FIPS devolverá al menos 128.  
  
 SQL_MAX_TABLES_IN_SELECT(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de tablas permitido en el **FROM** cláusula de una **seleccione** instrucción. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatibles con el nivel de entrada FIPS devolverá al menos 15. Un controlador de función de nivel intermedio de FIPS devolverá al menos 50.  
  
 SQL_MAX_USER_NAME_LEN(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de usuario en el origen de datos. Si no hay ninguna longitud máxima o la longitud se desconozca, este valor se establece en cero.  
  
 SQL_MULT_RESULT_SETS(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite varios conjuntos de resultados, "N" Si no es así.  
  
 Para obtener más información acerca de varios conjuntos de resultados, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el controlador admite más de una transacción activa al mismo tiempo, "N" Si solo puede estar activa una transacción en cualquier momento.  
  
 La información devuelta para este tipo de información no es aplicable en el caso de las transacciones distribuidas.  
  
 SQL_NEED_LONG_DATA_LEN(ODBC 2.0)  
 Una cadena de caracteres: "Y" si el origen de datos tiene la longitud de un valor de datos de tipo long (el tipo de datos es un tipo de datos específicos del origen de datos long, SQL_LONGVARBINARY o SQL_LONGVARCHAR) antes de ese valor se envía al origen de datos, "N" Si no es así. Para obtener más información, consulte [función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) y [función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 SQL_NON_NULLABLE_COLUMNS(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica si el origen de datos admite NOT NULL en columnas:  
  
 SQL_NNC_NULL = todas las columnas deben aceptar valores NULL.  
  
 SQL_NNC_NON_NULL = las columnas no pueden ser que acepta valores NULL. (Los datos de origen es compatible con la **no NULL** restricción de columna en **CREATE TABLE** instrucciones.)  
  
 Un controlador de función de nivel básico de SQL-92 devolverá SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica donde se ordenan los valores NULL en un conjunto de resultados:  
  
 SQL_NC_END = los valores NULL se ordenan al final del conjunto de resultados, independientemente de las palabras clave ASC o DESC.  
  
 SQL_NC_HIGH = los valores NULL están ordenados en el extremo superior del conjunto de resultados, dependiendo de las palabras clave ASC o DESC.  
  
 SQL_NC_LOW = los valores NULL están ordenados en el extremo inferior del conjunto de resultados, dependiendo de las palabras clave ASC o DESC.  
  
 SQL_NC_START = los valores NULL se ordenan al principio del conjunto de resultados, independientemente de las palabras clave ASC o DESC.  
  
 SQL_NUMERIC_FUNCTIONS(ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; Cada máscara de bits se etiqueta con la versión en el que se introdujo.  
  
 Una máscara de bits SQLUINTEGER enumerar las funciones numéricas escalares admitidas por el controlador y el origen de datos asociado.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué funciones numéricas son compatibles con:  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_ATAN SQL_FN_NUM_ATAN2 SQL_ SQL_FN_NUM_DEGREES (ODBC 2.0) DE (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_LOG SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_PI SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) SQL_FN_NUM_RAND (ODBC 1.0) SQL_FN_ NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_SIN SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE(ODBC 3.0)  
 Un valor SQLUINTEGER que indica el nivel de ODBC 3 *.x* interfaz que obedece el controlador.  
  
 SQL_OIC_CORE: El nivel mínimo que son todos los controladores ODBC que se espera que cumplir. Este nivel incluye elementos de la interfaz básica, como las funciones de la conexión, las funciones para preparar y ejecutar una instrucción SQL, funciones de metadatos de conjunto de resultados básica, las funciones de catálogo básica y así sucesivamente.  
  
 SQL_OIC_LEVEL1: Un nivel que incluye marcadores de funciones de nivel de cumplimiento de estándares, además de los cursores desplazables, de core, colocados actualiza y elimina y así sucesivamente.  
  
 SQL_OIC_LEVEL2: Un nivel que incluye funcionalidad de nivel de cumplimiento de normas de estándares de nivel 1, más características avanzadas, como cursores confidenciales; actualizar, eliminar y actualizar por marcadores; compatibilidad con los procedimientos almacenados; funciones de catálogo para las claves principales y externas; compatibilidad con múltiples catálogo; y así sucesivamente.  
  
 Para obtener más información, consulte [niveles de compatibilidad de interfaz](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER(ODBC 1.0)  
 Una cadena de caracteres con la versión de ODBC a la que se ajusta el Administrador de controladores. La versión tiene el formato ##. ##. 0000, donde los dos primeros dígitos son la versión principal y los dos dígitos son la versión secundaria. Esto se implementa solo en el Administrador de controladores.  
  
 SQL_OJ_CAPABILITIES(ODBC 2.01)  
 Una máscara de bits SQLUINTEGER enumerar los tipos de combinaciones externas compatibles con el origen de datos y el controlador. Las máscaras de bits siguientes se usan para determinar qué tipos se admiten:  
  
 SQL_OJ_LEFT = Left se admiten las combinaciones externas.  
  
 SQL_OJ_RIGHT = Right se admiten las combinaciones externas.  
  
 SQL_OJ_FULL = completo se admiten las combinaciones externas.  
  
 SQL_OJ_NESTED = anidados se admiten las combinaciones externas.  
  
 SQL_OJ_NOT_ORDERED = la columna de nombres en la cláusula ON de la combinación externa no tiene que estar en el mismo orden que sus nombres de tabla correspondiente en el **OUTER JOIN** cláusula.  
  
 SQL_OJ_INNER = interno tabla (la tabla derecha en una combinación externa izquierda) o la tabla izquierda en una combinación externa derecha también se puede usar en una combinación interna. Esto no se aplica a las combinaciones externas completas que no tienen una tabla interna.  
  
 SQL_OJ_ALL_COMPARISON_OPS = la comparación de operador en la cláusula ON puede ser cualquiera de los operadores de comparación ODBC. Si no se establece este bit, solo el operador de comparación es igual a (=) se puede usar en las combinaciones externas.  
  
 Si ninguna de estas opciones se devuelve como compatible, no se admite ninguna cláusula de combinación externa.  
  
 Para obtener información sobre la compatibilidad de los operadores de combinación relacional en una instrucción SELECT, como se define en SQL-92, consulte SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT(ODBC 2.0)  
 Una cadena de caracteres: "Y" si las columnas de la **ORDER BY** cláusula debe estar en la lista de selección; en caso contrario, "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS(ODBC 3.0)  
 Una enumeración de propiedades del controlador con respecto a la disponibilidad de la fila de SQLUINTEGER que incluya recuentos en una ejecución con parámetros. Tiene los siguientes valores:  
  
 SQL_PARC_BATCH = individuales están disponibles para cada conjunto de parámetros de recuentos de filas. Esto es conceptualmente equivalente al controlador de generación de un lote de instrucciones SQL, uno para cada parámetro establecido en la matriz. Información extendida de errores se puede recuperar mediante el campo de descriptor SQL_PARAM_STATUS_PTR.  
  
 SQL_PARC_NO_BATCH = hay recuento de solo filas está disponible, que es el recuento acumulado de filas resultantes de la ejecución de la instrucción para toda la matriz de parámetros. Esto es conceptualmente equivalente a tratar la instrucción junto con la matriz de parámetros completa como una unidad atómica. Errores se tratan igual como si se ejecuta una instrucción.  
  
 SQL_PARAM_ARRAY_SELECTS(ODBC 3.0)  
 Un SQLUINTEGER enumerar las propiedades del controlador con respecto a la disponibilidad del resultado se establece en una ejecución con parámetros. Tiene los siguientes valores:  
  
 SQL_PAS_BATCH = hay un conjunto disponible por conjunto de parámetros de resultados. Esto es conceptualmente equivalente al controlador de generación de un lote de instrucciones SQL, uno para cada parámetro establecido en la matriz.  
  
 SQL_PAS_NO_BATCH = hay solo un conjunto de resultados disponible, que representa el resultado acumulado conjunto resultante de la ejecución de la declaración de la matriz completa de parámetros. Esto es conceptualmente equivalente a tratar la instrucción junto con la matriz de parámetros completa como una unidad atómica.  
  
 SQL_PAS_NO_SELECT = un controlador no permite una instrucción de generación de conjunto de resultados que se ejecutará con una matriz de parámetros.  
  
 SQL_PROCEDURE_TERM(ODBC 1.0)  
 Una cadena de caracteres con el nombre del proveedor de origen de datos para un procedimiento; Por ejemplo, "procedimiento de base de datos", "procedimiento almacenado", "procedure", "paquete" o "consulta almacenada".  
  
 SQL_PROCEDURES(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el origen de datos es compatible con los procedimientos y el controlador admite la sintaxis de invocación del procedimiento ODBC; "N" en caso contrario.  
  
 SQL_POS_OPERATIONS(ODBC 2.0)  
 Una máscara de bits SQLINTEGER enumerar las operaciones de soporte técnico en **SQLSetPos**.  
  
 Las máscaras de bits siguientes se usan junto con la marca para determinar qué opciones son compatibles.  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE(ODBC 2.0)  
 Un SQLUSMALLINT valor como sigue:  
  
 SQL_IC_UPPER = entre comillas los identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en mayúsculas en el catálogo del sistema.  
  
 SQL_IC_LOWER = entre comillas los identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en minúsculas en el catálogo del sistema.  
  
 Sql_ic_sensitive está = entre comillas los identificadores de SQL se distinguen mayúsculas de minúsculas y se almacenan en mayúsculas y minúsculas mezcladas en el catálogo del sistema. (En una base de datos compatibles con SQL-92, identificadores entre comillas dobles son siempre entre mayúsculas y minúsculas).  
  
 SQL_IC_MIXED = entre comillas los identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en mayúsculas y minúsculas mezcladas en el catálogo del sistema.  
  
 Sql_ic_sensitive está siempre devuelve un controlador de función de nivel básico de SQL-92.  
  
 SQL_ROW_UPDATES(ODBC 1.0)  
 Una cadena de caracteres: "Y" si un cursor controlado por conjunto de claves o mixto mantiene versiones de fila o los valores para todas las captura las filas y por lo tanto, puede detectar las actualizaciones que se realizaron en una fila por cualquier usuario, puesto que la fila se capturó en último lugar. (Esto se aplica solo a las actualizaciones, no eliminaciones o inserciones). El controlador puede devolver la marca SQL_ROW_UPDATED para el estado de fila de matriz cuando **SQLFetchScroll** se llama. En caso contrario, "N".  
  
 SQL_SCHEMA_TERM(ODBC 1.0)  
 Una cadena de caracteres con el nombre del proveedor de origen de datos para un esquema; Por ejemplo, "owner", "Identificador de autorización" o "Schema".  
  
 La cadena de caracteres se puede devolver en caso de la parte superior, inferior o mixto.  
  
 Un controlador de función de nivel básico de SQL-92 siempre devuelve "esquema".  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_OWNER_TERM.  
  
 SQL_SCHEMA_USAGE(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las instrucciones en el que se pueden usar esquemas:  
  
 SQL_SU_DML_STATEMENTS = se admiten los esquemas en todas las instrucciones de lenguaje de manipulación de datos: **Seleccione**, **insertar**, **actualizar**, **eliminar**y si se admite, **seleccione para actualizar** y posicionadas update y delete instrucciones.  
  
 SQL_SU_PROCEDURE_INVOCATION = se admiten los esquemas en la instrucción de invocación del procedimiento ODBC.  
  
 SQL_SU_TABLE_DEFINITION = se admiten los esquemas en todas las instrucciones de definición de tabla: **CREAR una tabla**, **Crear vista**, **ALTER TABLE**, **DROP TABLE**, y **DROP VIEW**.  
  
 SQL_SU_INDEX_DEFINITION = se admiten los esquemas en todas las instrucciones de definición de índice: **Crear índice** y **DROP INDEX**.  
  
 SQL_SU_PRIVILEGE_DEFINITION = se admiten los esquemas en todas las instrucciones de definición de privilegios: **GRANT** y **REVOCAR**.  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá las opciones SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION y SQL_SU_PRIVILEGE_DEFINITION, como compatible.  
  
 Esto *InfoType* se cambió para ODBC 3.0 desde la versión 2.0 de ODBC *InfoType* SQL_OWNER_USAGE.  
  
 SQL_SCROLL_OPTIONS(ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; Cada máscara de bits se etiqueta con la versión en el que se introdujo.  
  
 Una máscara de bits SQLUINTEGER enumerar las opciones de desplazamiento que se admite para los cursores desplazables.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué opciones son compatibles con:  
  
 SQL_SO_FORWARD_ONLY = el cursor solo se desplaza hacia delante. ODBC (1.0)  
  
 SQL_SO_STATIC = los datos en el resultado de conjunto es estático. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = el controlador de guarda y usa las claves para cada fila del conjunto de resultados. ODBC (1.0)  
  
 SQL_SO_DYNAMIC = el controlador de mantiene las claves para cada fila del conjunto de filas (el tamaño del conjunto de claves es el mismo que el tamaño del conjunto de filas). ODBC (1.0)  
  
 SQL_SO_MIXED = el mantiene las claves de controlador para cada fila en el conjunto de claves y el tamaño del conjunto de claves es mayor que el tamaño del conjunto de filas. El cursor está controlado por conjunto de claves en el conjunto de claves y dinámicos fuera el conjunto de claves. ODBC (1.0)  
  
 Para obtener información acerca de los cursores desplazables, consulte [los cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 SQL_SEARCH_PATTERN_ESCAPE(ODBC 1.0)  
 Una cadena de caracteres que especifica lo que admita el controlador como carácter de escape que permite el uso de la trama coincidencia metacaracteres subrayado (_) y signo de porcentaje (%) como caracteres válidos en patrones de búsqueda. Este carácter de escape se aplica solo a esos argumentos de función de catálogo que admiten las cadenas de búsqueda. Si esta cadena está vacía, el controlador no es compatible con un carácter de escape del patrón de búsqueda.  
  
 Dado que este tipo de información no indica compatibilidad general de carácter de escape en el **como** predicado, SQL-92 no incluye los requisitos para esta cadena de caracteres.  
  
 Esto *InfoType* se limita a las funciones de catálogo. Para obtener una descripción del uso del carácter de escape en cadenas de patrón de búsqueda, vea [argumentos de valor de patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER_NAME(ODBC 1.0)  
 Una cadena de caracteres con el nombre de servidor específicas del origen de datos reales; resulta útil cuando se usa un nombre de origen de datos durante **SQLConnect**, **SQLDriverConnect**, y **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS(ODBC 2.0)  
 Una cadena de caracteres que contiene todos los caracteres especiales (es decir, todos los caracteres excepto a z, A Z, 0 al 9 y caracteres de subrayado) que pueden usarse en un nombre de identificador, por ejemplo, un nombre de tabla, el nombre de columna o el nombre del índice en el origen de datos. Por ejemplo, "#$^". Si un identificador contiene uno o varios de estos caracteres, el identificador debe ser un identificador delimitado.  
  
 SQL_SQL_CONFORMANCE(ODBC 3.0)  
 Un valor SQLUINTEGER que indica el nivel de SQL-92 compatibles con el controlador:  
  
 SQL_SC_SQL92_ENTRY = entrada nivel SQL-92 compatible.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 nivel transitoria compatible.  
  
 SQL_SC_SQL92_FULL = nivel completo compatible con SQL-92.  
  
 SQL_SC_ SQL92_INTERMEDIATE = intermedio nivel SQL-92 compatible.  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones escalares de fecha y hora que son compatibles con el controlador y el origen de datos asociado, tal como se define en SQL-92.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué funciones de fecha y hora son compatibles con:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las reglas compatibles con una clave externa en una **eliminar** instrucción, tal como se define en SQL-92.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con el origen de datos:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Un controlador de nivel compatibles con FIPS transitorio siempre devolverá todas estas opciones como compatible.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las reglas compatibles con una clave externa en una **actualización** instrucción, tal como se define en SQL-92.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con el origen de datos:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones como compatible.  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas que se admiten en el **GRANT** instrucción, tal como se define en SQL-92.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con el origen de datos:  
  
 () (Nivel intermedio) SQL_SG_INSERT_COLUMN SQL_SG_INSERT_TABLE (nivel de entrada) SQL_SG_REFERENCES_TABLE (nivel de entrada) SQL_SG_REFERENCES_COLUMN (nivel de entrada) (nivel de entrada) de SQL_SG_SELECT_TABLE SQL_SG_UPDATE_COLUMN SQL_SG_DELETE_TABLE (nivel de entrada) Nivel de entrada) SQL_SG_UPDATE_TABLE (nivel de entrada) SQL_SG_USAGE_ON_DOMAIN (nivel FIPS transitorio) SQL_SG_USAGE_ON_CHARACTER_SET (nivel FIPS transitorio) SQL_SG_USAGE_ON_COLLATION (nivel FIPS transitorio) SQL_SG_USAGE_ON_TRANSLATION (FIPS Nivel transitorio) SQL_SG_WITH_GRANT_OPTION (nivel de entrada)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones escalares de valor numérico que son compatibles con el controlador y el origen de datos asociado, tal como se define en SQL-92.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué funciones numéricas son compatibles con:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerando los predicados que se admiten en un **seleccione** instrucción, tal como se define en SQL-92.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se usan para determinar qué opciones son compatibles con el origen de datos:  
  
 SQL_SP_BETWEEN (nivel de entrada) (nivel de entrada) de SQL_SP_COMPARISON SQL_SP_EXISTS (nivel de entrada) SQL_SP_IN (nivel de entrada) SQL_SP_ISNOTNULL (nivel de entrada) SQL_SP_ISNULL (nivel de entrada) SQL_SP_LIKE (nivel de entrada) SQL_SP_MATCH_FULL (nivel Full) SQL_SP_MATCH_PARTIAL (Nivel completo) SQL_SP_MATCH_UNIQUE_FULL (nivel completo) SQL_SP_MATCH_UNIQUE_PARTIAL (nivel Full) SQL_SP_OVERLAPS (nivel FIPS transitorio) (nivel de entrada) de SQL_SP_QUANTIFIED_COMPARISON SQL_SP_UNIQUE (nivel de entrada)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerando los operadores de combinación relacional admitidos en un **seleccione** instrucción, tal como se define en SQL-92.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se usan para determinar qué opciones son compatibles con el origen de datos:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (nivel intermedio) SQL_SRJO_CROSS_JOIN (nivel completo) (nivel intermedio) SQL_SRJO_EXCEPT_JOIN SQL_SRJO_FULL_OUTER_JOIN (nivel intermedio) SQL_SRJO_INNER_JOIN (nivel FIPS transitorio) SQL_SRJO_INTERSECT_JOIN (Nivel intermedio) SQL_SRJO_LEFT_OUTER_JOIN (nivel FIPS transitorio) SQL_SRJO_NATURAL_JOIN (nivel FIPS transitorio) SQL_SRJO_RIGHT_OUTER_JOIN (nivel FIPS transitorio) SQL_SRJO_UNION_JOIN (nivel completo)  
  
 SQL_SRJO_INNER_JOIN indica compatibilidad para la **INNER JOIN** sintaxis, no para la funcionalidad de combinación interna. Compatibilidad con la **INNER JOIN** sintaxis es transitorio de FIPS, mientras que la compatibilidad con la funcionalidad de combinación interna es **entrada**.  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas que se admiten en el **REVOCAR** instrucción, tal como se define en SQL-92, admitidos por el origen de datos.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con el origen de datos:  
  
 SQL_SR_CASCADE (nivel transitorias FIPS) (nivel de entrada) de SQL_SR_DELETE_TABLE SQL_SR_GRANT_OPTION_FOR (nivel intermedio) SQL_SR_INSERT_COLUMN (nivel intermedio) SQL_SR_INSERT_TABLE (nivel de entrada) SQL_SR_REFERENCES_COLUMN (nivel de entrada) SQL_SR_ REFERENCES_TABLE (nivel de entrada) SQL_SR_RESTRICT (nivel transitorias FIPS) (nivel de entrada) de SQL_SR_SELECT_TABLE SQL_SR_UPDATE_COLUMN (nivel de entrada) SQL_SR_UPDATE_TABLE (nivel de entrada) SQL_SR_USAGE_ON_DOMAIN (nivel FIPS transitorio) SQL_SR_USAGE_ON_ CHARACTER_SET (nivel FIPS transitorio) (nivel FIPS transitorio) SQL_SR_USAGE_ON_COLLATION SQL_SR_USAGE_ON_TRANSLATION (nivel FIPS transitorio)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las expresiones de constructor de valor de fila admitidas un **seleccione** instrucción, tal como se define en SQL-92. Las máscaras de bits siguientes se usan para determinar qué opciones son compatibles con el origen de datos:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones escalares de cadena que son compatibles con el controlador y el origen de datos asociado, tal como se define en SQL-92.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué funciones de cadena son compatibles con:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las expresiones de valor compatibles, tal como se define en SQL-92.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se usan para determinar qué opciones son compatibles con el origen de datos:  
  
 SQL_SVE_CASE (nivel intermedio) SQL_SVE_CAST (nivel transitorias FIPS) (nivel intermedio) SQL_SVE_COALESCE SQL_SVE_NULLIF (nivel intermedio)  
  
 SQL_STANDARD_CLI_CONFORMANCE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumere el estándar de la CLI o estándares a la que se ajusta el controlador. Las máscaras de bits siguientes se usan para determinar qué niveles que obedece el controlador:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: El controlador cumple con la CLI de grupo de abrir la versión 1.  
  
 SQL_SCC_ISO92_CLI: El controlador cumple con la CLI de 92 ISO.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor estático que son compatibles con el controlador. Esta máscara de bits contiene el subconjunto de atributos; primera para el segundo subconjunto, consulte SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 Las máscaras de bits siguientes se utilizan para determinar los atributos que son compatibles con:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (y sustituya "cursor estático" para "cursor dinámico" en las descripciones).  
  
 Un controlador de función de nivel intermedio de SQL-92 normalmente devolverá las opciones SQL_CA1_NEXT, SQL_CA1_ABSOLUTE y SQL_CA1_RELATIVE como compatible, porque el controlador es compatible con los cursores desplazables a través de la instrucción FETCH SQL incrustada. Ya que esto no determina directamente del soporte de SQL subyacente, sin embargo, los cursores desplazables pueden no ser compatibles, incluso para un controlador de función de nivel intermedio de SQL-92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor estático que son compatibles con el controlador. Esta máscara de bits contiene el subconjunto de segundo de los atributos. para el subconjunto de la primera, consulte SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 Las máscaras de bits siguientes se utilizan para determinar los atributos que son compatibles con:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (y sustituya "cursor estático" para "cursor dinámico" en las descripciones).  
  
 SQL_STRING_FUNCTIONS(ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; Cada máscara de bits se etiqueta con la versión en el que se introdujo.  
  
 Una máscara de bits SQLUINTEGER enumerar las funciones de escalar de cadena admitidas por el controlador y el origen de datos asociado.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué funciones de cadena son compatibles con:  
  
 SQL_FN_STR_ASCII (ODBC 1.0) (ODBC 3.0) SQL_FN_STR_BIT_LENGTH SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC 1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_ STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 Si una aplicación puede llamar a la **buscar** función escalar con la *string_exp1*, *string_exp2*, y *iniciar* argumentos, el controlador Devuelve la máscara de bits SQL_FN_STR_LOCATE. Si una aplicación puede llamar a la función escalar de buscar solamente con la *string_exp1* y *string_exp2* argumentos, el controlador devuelve la máscara de bits SQL_FN_STR_LOCATE_2. Los controladores que admiten totalmente la **buscar** función escalar devuelve tanto las máscaras de bits.  
  
 (Para obtener más información, consulte [funciones de cadena](../../../odbc/reference/appendixes/string-functions.md) en el apéndice E, "funciones escalares.")  
  
 SQL_SUBQUERIES(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerando los predicados que admiten las subconsultas:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 La máscara de bits SQL_SQ_CORRELATED_SUBQUERIES indica que todos los predicados que admiten las subconsultas admiten subconsultas correlacionadas.  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá una máscara de bits en el que todos estos bits se establecen.  
  
 SQL_SYSTEM_FUNCTIONS(ODBC 1.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones de sistema escalares admitidas por el controlador y el origen de datos asociado.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué funciones del sistema son compatibles con:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM(ODBC 1.0)  
 Una cadena de caracteres con el nombre del proveedor de origen de datos para una tabla; Por ejemplo, "table" o "archivo".  
  
 Esta cadena de caracteres puede ser en caso de la parte superior, inferior o mixto.  
  
 Un controlador de función de nivel básico de SQL-92 siempre devuelve "table".  
  
 SQL_TIMEDATE_ADD_INTERVALS(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerando los intervalos de marca de hora compatibles con el controlador y el origen de datos asociado para la función escalar de TIMESTAMPADD no.  
  
 Las máscaras de bits siguientes se usan para determinar qué intervalos se admiten:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un controlador de nivel compatibles con FIPS transitorio siempre devolverá una máscara de bits en el que todos estos bits se establecen.  
  
 SQL_TIMEDATE_DIFF_INTERVALS(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerando los intervalos de marca de hora compatibles con el controlador y el origen de datos asociado para la función escalar de TIMESTAMPDIFF no.  
  
 Las máscaras de bits siguientes se usan para determinar qué intervalos se admiten:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un controlador de nivel compatibles con FIPS transitorio siempre devolverá una máscara de bits en el que todos estos bits se establecen.  
  
 SQL_TIMEDATE_FUNCTIONS(ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; Cada máscara de bits se etiqueta con la versión en el que se introdujo.  
  
 Una máscara de bits SQLUINTEGER enumerando los escalar funciones fecha y hora admitidas por el controlador y el origen de datos asociado.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué funciones de fecha y hora son compatibles con:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) SQL_FN_TD_CURRENT_TIME (ODBC 3.0) SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) (ODBC 1.0) SQL_FN_TD_CURTIME SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) (SQL_FN_TD_DAYOFWEEK ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_ SEGUNDO (ODBC 1.0) (ODBC 2.0) SQL_FN_TD_TIMESTAMPADD SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE(ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; cada valor devuelto se etiqueta con la versión en el que se introdujo.  
  
 Un valor SQLUSMALLINT que describe la compatibilidad con transacciones en el controlador u origen de datos:  
  
 SQL_TC_NONE = transacciones no compatibles. ODBC (1.0)  
  
 SQL_TC_DML = transacciones pueden contener solo las instrucciones de lenguaje de manipulación de datos (DML) (**seleccione**, **insertar**, **actualización**, **eliminar** ). Instrucciones de lenguaje de definición (DDL) de datos encontró en una causa de la transacción a un error. ODBC (1.0)  
  
 SQL_TC_DDL_COMMIT = transacciones pueden contener solo las instrucciones DML. Instrucciones de DDL (**CREATE TABLE**, **DROP INDEX**, y así sucesivamente) encontrado en una causa de la transacción se confirma la transacción. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = transacciones pueden contener solo las instrucciones DML. Se omiten las instrucciones de DDL que se encuentra en una transacción. (ODBC 2.0)  
  
 SQL_TC_ALL = transacciones pueden contener instrucciones de DDL y las instrucciones DML en cualquier orden. ODBC (1.0)  
  
 (Dado que admita las transacciones es obligatorio en SQL-92, un controlador compatible de SQL-92 [cualquier nivel] nunca devolverá SQL_TC_NONE.)  
  
 SQL_TXN_ISOLATION_OPTION(ODBC 1.0)  
 Una máscara de bits SQLUINTEGER enumerando los niveles de aislamiento de transacción disponibles desde el controlador u origen de datos.  
  
 Las máscaras de bits siguientes se usan junto con la marca para determinar qué opciones son compatibles con:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Para obtener descripciones de estos niveles de aislamiento, vea la descripción de SQL_DEFAULT_TXN_ISOLATION.  
  
 Para establecer el nivel de aislamiento de transacción, una aplicación llama a **SQLSetConnectAttr** para establecer el atributo SQL_ATTR_TXN_ISOLATION. Para obtener más información, consulte [función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá SQL_TXN_SERIALIZABLE como compatible. Un controlador de función de nivel FIPS transitorias siempre devolverá todas estas opciones como compatible.  
  
 SQL_UNION(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar la compatibilidad con la **UNION** cláusula:  
  
 SQL_U_UNION = el origen de datos admite la **UNION** cláusula.  
  
 SQL_U_UNION_ALL = el origen de datos admite la **todas** palabra clave en el **UNION** cláusula. (**SQLGetInfo** devuelve SQL_U_UNION y SQL_U_UNION_ALL en este caso.)  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá ambas opciones como compatible.  
  
 SQL_USER_NAME(ODBC 1.0)  
 Una cadena de caracteres con el nombre usado en una base de datos determinada, que puede ser diferente del nombre de inicio de sesión.  
  
 SQL_XOPEN_CLI_YEAR(ODBC 3.0)  
 Una cadena de caracteres que indica el año de publicación de la especificación Open Group con el que cumple totalmente la versión del Administrador de controladores ODBC.  
  
 SQL_ACCESSIBLE_PROCEDURES(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el usuario puede ejecutar todos los procedimientos que devuelve **SQLProcedures**; "N" si puede haber procedimientos devuelto que no se puede ejecutar el usuario.  
  
 SQL_ACCESSIBLE_TABLES(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el usuario tiene la garantía **seleccione** privilegios a todas las tablas devueltas por **SQLTables**; "N" si puede haber tablas devuelto que el usuario no tiene acceso.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de los entornos activos que puede admitir el controlador. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar la compatibilidad con las funciones de agregación:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un controlador de función de nivel básico de SQL-92 siempre devolverá todas estas opciones como compatible.  
  
 SQL_ALTER_DOMAIN(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **ALTER dominio** instrucción, tal como se define en SQL-92, admitidos por el origen de datos. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas las máscaras de bits. Un valor devuelto de "0" significa que el **ALTER dominio** no se admite la instrucción.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = agregar una restricción de dominio es compatible (nivel total)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter dominio > \<cláusula predeterminado de set domain > es compatible (nivel total)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<cláusula de definición de restricción name > es compatible con nombres de restricción de dominio (nivel intermedio)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<cláusula de restricción de dominio de destino > es compatible (nivel total)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter dominio > \<cláusula default de colocación dominio > es compatible (nivel total)  
  
 Los bits siguientes especifican admitidos \<atributos restricción > Si \<Agregar restricción de dominio > es compatible (se establece el bit SQL_AD_ADD_DOMAIN_CONSTRAINT):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (nivel completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (nivel completo) (nivel Full) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (nivel completo)  
  
 SQL_ALTER_TABLE(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la **ALTER TABLE** instrucción admitida por el origen de datos.  
  
 El nivel de conformidad con SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las máscaras de bits siguientes se utilizan para determinar qué cláusulas son compatibles con:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<Agregar columna > se admite la cláusula con facilidad para especificar la intercalación de columna (nivel completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<Agregar columna > se admite la cláusula con facilidad para especificar los valores predeterminados de columna (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<Agregar columna > es compatible (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<Agregar columna > se admite la cláusula con facilidad para especificar restricciones de columna (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<Agregar restricción de tabla > se admite la cláusula (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<definición del nombre de restricción > se admite para asignar nombres a las restricciones de columna y tabla (nivel intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<quitar columnas > se admite en cascada (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alteración de columna > \<cláusula predeterminado de drop column > es compatible (nivel intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<quitar columnas > RESTRICT es compatible (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<quitar columnas > RESTRICT es compatible (nivel transitorias FIPS) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alteración de columna > \<cláusula de conjunto de columnas predeterminado > es compatible (nivel intermedio) (ODBC 3.0)  
  
 Los bits siguientes especifican la compatibilidad con \<atributos restricción > Si se admite la especificación de restricciones de columna o tabla (se establece el bit SQL_AT_ADD_CONSTRAINT):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (nivel completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (nivel completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (nivel completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (nivel completo) (ODBC 3.0)  
  
 SQL_ASYNC_MODE(ODBC 3.0)  
 Un valor SQLUINTEGER que indica el nivel de compatibilidad asincrónica en el controlador:  
  
 SQL_AM_CONNECTION = se admite la ejecución asincrónica de nivel de conexión. Todos los identificadores de instrucción asociados con un identificador de conexión determinado están en modo asincrónico o todas están en modo sincrónico. Un identificador de instrucción en una conexión no puede estar en modo asincrónico mientras otro identificador de instrucción en la misma conexión está en modo sincrónico y viceversa.  
  
 SQL_AM_STATEMENT = se admite la ejecución asincrónica de nivel de instrucción. Algunos identificadores de instrucciones asociados con un identificador de conexión pueden estar en modo asíncrono, mientras que otros identificadores de instrucciones en la misma conexión están en modo sincrónico.  
  
 SQL_AM_NONE = asincrónico no se admite el modo.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerando el comportamiento del controlador con respecto a la disponibilidad de la fila de cuenta. Las máscaras de bits siguientes se utilizan junto con el tipo de información:  
  
 SQL_BRC_ROLLED_UP = recuentos de filas para las instrucciones INSERT, DELETE o UPDATE consecutivas se consolidan en uno. Si no se establece este bit, recuentos de filas están disponibles para cada instrucción.  
  
 SQL_BRC_PROCEDURES = recuentos de filas, si existe, están disponibles cuando se ejecuta un lote en un procedimiento almacenado. Si existen recuentos de filas, puede desplegar o disponibles de forma individual, según el bit SQL_BRC_ROLLED_UP.  
  
 SQL_BRC_EXPLICIT = recuentos de filas, si existe, están disponibles cuando se ejecuta un lote directamente mediante una llamada a **SQLExecute** o **SQLExecDirect**. Si existen recuentos de filas, puede desplegar o disponibles de forma individual, según el bit SQL_BRC_ROLLED_UP.  
  
## <a name="example"></a>Ejemplo  
 **SQLGetInfo** devuelve listas de opciones admitidas como una máscara de bits SQLUINTEGER que incluya en **InfoValuePtr*. La máscara de bits para cada opción se usa junto con la marca para determinar si se admite la opción.  
  
 Por ejemplo, una aplicación podría utilizar el código siguiente para determinar si la función escalar de SUBCADENA es compatible con el controlador asociado con la conexión.  
  
 Para obtener otro ejemplo del uso de **SQLGetInfo**, consulte [función SQLTables](../../../odbc/reference/syntax/sqltables-function.md).  
  
```cpp  
SQLUINTEGER fFuncs;  
  
SQLGetInfo(hdbc,   
           SQL_STRING_FUNCTIONS,  
           (SQLPOINTER)&fFuncs,  
           sizeof(fFuncs),  
           NULL);  
  
// SUBSTRING supported  
if (fFuncs & SQL_FN_STR_SUBSTRING)   
   ;   // do something  
  
// SUBSTRING not supported  
else  
   ;   // do something else  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
 Devuelve el valor de un atributo de conexión  
 [Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 Determinar si un controlador es compatible con una función  
 [Función SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Devuelve la configuración de un atributo de instrucción  
 [Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Devolver información acerca de los tipos de datos de un origen de datos  
 [Función SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
