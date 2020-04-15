---
title: Función SQLGetInfo ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 514922fd085cfd2ba19eb5c07dd844db82d55202
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303347"
---
# <a name="sqlgetinfo-function"></a>Función SQLGetInfo
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLGetInfo** devuelve información general sobre el controlador y el origen de datos asociado a una conexión.  
  
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
 [Salida] Puntero a un búfer en el que se va a devolver la información. Dependiendo del *InfoType* solicitado, la información devuelta será una de las siguientes: una cadena de caracteres terminada en null, un valor SQLUSMALLINT, una máscara de bits SQLUINTEGER, un indicador SQLUINTEGER, un valor binario SQLUINTEGER o un valor SQLULEN.  
  
 Si el *InfoType* argumento es SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT, el *InfoValuePtr* argumento es entrada y salida. (Consulte los descriptores SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT más adelante en esta descripción de la función para obtener más información.)  
  
 Si *InfoValuePtr* es NULL, *StringLengthPtr* seguirá devolviendo el número total de bytes (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *InfoValuePtr*.  
  
 *BufferLength*  
 [Entrada] Longitud del \*búfer *InfoValuePtr.* Si el valor de * \*InfoValuePtr* no es una cadena de caracteres o si *InfoValuePtr* es un puntero nulo, se omite el argumento *BufferLength.* El controlador supone que el tamaño de * \*InfoValuePtr* es SQLUSMALLINT o SQLUINTEGER, en función de *InfoType*. Si * \*InfoValuePtr* es una cadena Unicode (al llamar a **SQLGetInfoW**), el *BufferLength* argumento debe ser un número par; si no es así, se devuelve SQLSTATE HY090 (cadena no válida o longitud de búfer).  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de bytes (excluyendo el carácter de terminación nula para los datos de caracteres) disponible para devolver en **InfoValuePtr*.  
  
 Para los datos de caracteres, si el número de bytes disponibles para devolver es mayor o igual que *BufferLength*, la información de \* *InfoValuePtr* se trunca en bytes *BufferLength* menos la longitud de un carácter de terminación nula y está terminada en null por el controlador.  
  
 Para todos los demás tipos de datos, se omite el \*valor de *BufferLength* y el controlador asume que el tamaño de *InfoValuePtr* es SQLUSMALLINT o SQLUINTEGER, dependiendo del *InfoType*.  
  
## <a name="return-value"></a>Valor devuelto  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetInfo** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *identificador* de *ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLGetInfo** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \*búfer *InfoValuePtr* no era lo suficientemente grande como para devolver toda la información solicitada. Por lo tanto, la información se truncó. La longitud de la información solicitada en su forma no truncada se devuelve en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexión no abierta|(DM) El tipo de información solicitada en *InfoType* requiere una conexión abierta. De los tipos de información reservados por ODBC, solo se pueden devolver SQL_ODBC_VER sin una conexión abierta.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY024|Valor de atributo no válido|(DM) el *InfoType* argumento se SQL_DRIVER_HSTMT y el valor señalado por *InfoValuePtr* no era un identificador de instrucción válido.<br /><br /> (DM) el *InfoType* argumento se SQL_DRIVER_HDESC y el valor señalado por *InfoValuePtr* no era un identificador de descriptor válido.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.<br /><br /> (DM) el valor especificado para *BufferLength* era un número impar e * \*InfoValuePtr* era de un tipo de datos Unicode.|  
|HY096|Tipo de información fuera del rango|El valor especificado para el argumento *InfoType* no era válido para la versión de ODBC admitida por el controlador.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Campo opcional no implementado|El valor especificado para el argumento *InfoType* era un valor específico del controlador que no es compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador que corresponde a *ConnectionHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Los tipos de información definidos actualmente se muestran en "Tipos de información", más adelante en esta sección; se espera que se definan más para aprovechar las diferentes fuentes de datos. ODBC reserva un rango de tipos de información; los desarrolladores de controladores deben reservar valores para su propio uso específico del controlador de Open Group. **SQLGetInfo** no realiza ninguna conversión Unicode o *thunking* (consulte [Apéndice A: Códigos](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) de error ODBC de la *referencia del programador ODBC*) para *InfoTypes*definidos por el controlador . Para obtener más información, vea [Tipos de datos específicos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)del controlador, Tipos de descriptor, Tipos de información, Tipos de diagnóstico y Atributos . El formato de la \*información devuelta en *InfoValuePtr* depende del *InfoType* solicitado. **SQLGetInfo** devolverá información en uno de los cinco formatos diferentes:  
  
-   Una cadena de caracteres terminada en null  
  
-   Un valor SQLUSMALLINT  
  
-   Una máscara de bits SQLUINTEGER  
  
-   Un valor SQLUINTEGER  
  
-   Un valor binario SQLUINTEGER  
  
 El formato de cada uno de los siguientes tipos de información se indica en la descripción del tipo. La aplicación debe convertir el valor devuelto en **InfoValuePtr* en consecuencia. Para obtener un ejemplo de cómo una aplicación podría recuperar datos de una máscara de bits SQLUINTEGER, vea "Ejemplo de código."  
  
 Un controlador debe devolver un valor para cada tipo de información que se define en las tablas siguientes. Si un tipo de información no se aplica al controlador o al origen de datos, el controlador devuelve uno de los valores enumerados en la tabla siguiente.  
  
 Cadena de caracteres ("Y" o "N")  
 "N"  
  
 Cadena de caracteres (no "Y" o "N")  
 cadena vacía.  
  
 SQLUSMALLINT  
 0  
  
 Máscara de bits SQLUINTEGER o valor binario SQLUINTEGER  
 0L  
  
 Por ejemplo, si un origen de datos no admite procedimientos, **SQLGetInfo** devuelve los valores enumerados en la tabla siguiente para los valores de *InfoType* relacionados con procedimientos.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 cadena vacía.  
  
 **SQLGetInfo** devuelve SQLSTATE HY096 (valor de argumento no válido) para los valores de *InfoType* que están en el intervalo de tipos de información reservados para su uso por ODBC pero no están definidos por la versión de ODBC compatible con el controlador. Para determinar qué versión de ODBC cumple un controlador, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_DRIVER_ODBC_VER. **SQLGetInfo** devuelve SQLSTATE HYC00 (característica opcional no implementada) para los valores de *InfoType* que se encuentran en el intervalo de tipos de información reservados para el uso específico del controlador, pero no son compatibles con el controlador.  
  
 Todas las llamadas a **SQLGetInfo** requieren una conexión abierta, excepto cuando el *InfoType* es SQL_ODBC_VER, que devuelve la versión del Administrador de controladores.  
  
## <a name="information-types"></a>Tipos de información  
 En esta sección se enumeran los tipos de información admitidos por **SQLGetInfo**. Los tipos de información se agrupan categóricamente y se enumeran alfabéticamente. También se enumeran los tipos de información que se agregaron o cambiaron el nombre para ODBC 3 *.x.*  
  
## <a name="driver-information"></a>Información del conductor  
 Los siguientes valores del argumento *InfoType* devuelven información sobre el controlador ODBC, como el número de instrucciones activas, el nombre del origen de datos y el nivel de cumplimiento de los estándares de interfaz:  
  
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
>  Al implementar **SQLGetInfo**, un controlador puede mejorar el rendimiento minimizando el número de veces que se envía o solicita la información desde el servidor.  
  
## <a name="dbms-product-information"></a>Información del producto DBMS  
 Los siguientes valores del argumento *InfoType* devuelven información sobre el producto DBMS, como el nombre y la versión de DBMS:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Información de la fuente de datos  
 Los siguientes valores del argumento *InfoType* devuelven información sobre el origen de datos, como las características del cursor y las capacidades de transacción:  
  
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
  
## <a name="supported-sql"></a>SQL soportado  
 Los siguientes valores del argumento *InfoType* devuelven información sobre las instrucciones SQL admitidas por el origen de datos. La sintaxis SQL de cada característica descrita por estos tipos de información es la sintaxis SQL-92. Estos tipos de información no describen exhaustivamente toda la gramática SQL-92. En su lugar, describen las partes de la gramática para las que los orígenes de datos suelen ofrecer diferentes niveles de soporte. En concreto, se tratan la mayoría de las instrucciones DDL de SQL-92.  
  
 Las aplicaciones deben determinar el nivel general de gramática admitida a partir del tipo de información SQL_SQL_CONFORMANCE y utilizar los otros tipos de información para determinar las variaciones del nivel de cumplimiento de estándares indicado.  
  
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
  
## <a name="sql-limits"></a>Límites SQL  
 Los siguientes valores del argumento *InfoType* devuelven información sobre los límites aplicados a los identificadores y las cláusulas de las instrucciones SQL, como las longitudes máximas de identificadores y el número máximo de columnas de una lista de selección. El controlador o el origen de datos pueden imponer limitaciones.  
  
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
 Los siguientes valores del argumento *InfoType* devuelven información sobre las funciones escalares admitidas por el origen de datos y el controlador. Para obtener más información acerca de las funciones escalares, consulte [Apéndice E: Funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Información de conversión  
 Los siguientes valores del argumento *InfoType* devuelven una lista de los tipos de datos SQL a los que el origen de datos puede convertir el tipo de datos SQL especificado con la función escalar **CONVERT:**  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>Tipos de información añadidos para ODBC 3.x  
 Se han agregado los siguientes valores del argumento *InfoType* para ODBC 3 *.x:*  
  
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
  
## <a name="information-types-renamed-for-odbc-3x"></a>Tipos de información renombrados para ODBC 3.x  
 Se ha cambiado el nombre de los siguientes valores del argumento *InfoType* para ODBC 3 *.x*.  
  
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
 Los siguientes valores del argumento *InfoType* han quedado obsoletos en ODBC 3 *.x*. Los controladores ODBC 3 *.x* deben seguir admitiendo estos tipos de información para la compatibilidad con versiones anteriores de las aplicaciones ODBC 2 *.x.* (Para obtener más información acerca de estos tipos, vea [Compatibilidad con SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md) en apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Descripciones del tipo de información  
 En la tabla siguiente se enumera alfabéticamente cada tipo de información, la versión de ODBC en la que se introdujo y su descripción.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 Una cadena de caracteres: "Y" si el usuario puede ejecutar todos los procedimientos devueltos por **SQLProcedures**; "N" si puede haber procedimientos devueltos que el usuario no puede ejecutar.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 Una cadena de caracteres: "Y" si se garantiza al usuario privilegios **SELECT** para todas las tablas devueltas por **SQLTables**; "N" si puede haber tablas devueltas a las que el usuario no pueda acceder.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de entornos activos que el controlador puede admitir. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que enumera la compatibilidad con funciones de agregación:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **ALTER DOMAIN,** tal como se define en SQL-92, compatible con el origen de datos. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas las máscaras de bits. Un valor devuelto de "0" significa que no se admite la instrucción **ALTER DOMAIN.**  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT: se admite la adición de una restricción de dominio (nivel completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT: \<modificar \<la cláusula predeterminada de> dominio establecida> (nivel completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<se admite la cláusula de definición de nombre de restricción> para asignar nombres a la restricción de dominio (nivel intermedio)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<se admite la cláusula de restricción de dominio de colocación> (nivel completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT: \<modificar \<la cláusula predeterminada de> dominio de colocación> (nivel completo)  
  
 Los bits siguientes \<especifican los \<atributos de restricción admitidos> si se admite agregar> de restricción de dominio (se establece el bit SQL_AD_ADD_DOMAIN_CONSTRAINT):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (Nivel completo)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (Nivel completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (Nivel completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (Nivel completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **ALTER TABLE** admitida por el origen de datos.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_AT_ADD_COLUMN_COLLATION \<se admite la cláusula de> de columna de agregar, con facilidad para especificar la intercalación de columnas (nivel completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<se admite la cláusula de> de columna de agregar, con facilidad para especificar los valores predeterminados de columna (nivel de transición de FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE \<se admite la> de agregar columna (nivel de transición DE FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT \<se admite la cláusula de> de columna de agregar, con facilidad para especificar restricciones de columna (nivel de transición DE FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<se admite la cláusula de> de restricción de tabla de agregar (nivel de transición FIPS) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<se admite la definición de nombre de restricción> para las restricciones de columna y tabla de nomenclatura (nivel intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE \<se admite la columna de colocación> CASCADE (nivel de transición de FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<se admite \<la cláusula predeterminada de la columna de modificación> de la columna de colocación> (nivel intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT \<se admite la columna de colocación> RESTRICT (nivel de transición DE FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<se admite la> de la columna de colocación> DE restricción (nivel de transición DE FIPS) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<se admite \<la cláusula predeterminada de la columna de modificación> de columna> (nivel intermedio) (ODBC 3.0)  
  
 Los bits siguientes \<especifican los atributos de restricción de soporte> si se admite la especificación de restricciones de columna o tabla (se establece el bit SQL_AT_ADD_CONSTRAINT):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (Nivel completo) (ODBC 3.0)SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (Nivel completo) (ODBC 3.0)SQL_AT_CONSTRAINT_DEFERRABLE (Nivel completo) (ODBC 3.0)SQL_AT_CONSTRAINT_NON_DEFERRABLE (Nivel completo) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 Un valor SQLUINTEGER que indica si el controlador puede ejecutar funciones de forma asincrónica en el identificador de conexión.  
  
 SQL_ASYNC_DBC_CAPABLE: el controlador puede ejecutar funciones de conexión de forma asincrónica.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE: el controlador no puede ejecutar funciones de conexión de forma asincrónica.  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Un valor SQLUINTEGER que indica el nivel de compatibilidad asincrónica en el controlador:  
  
 SQL_AM_CONNECTION: se admite la ejecución asincrónica de nivel de conexión. Todos los identificadores de instrucción asociados a un identificador de conexión determinado están en modo asincrónico o todos están en modo sincrónico. Un identificador de instrucción en una conexión no puede estar en modo asincrónico mientras que otro identificador de instrucción en la misma conexión está en modo sincrónico y viceversa.  
  
 SQL_AM_STATEMENT: se admite la ejecución asincrónica de nivel de instrucción. Algunos identificadores de instrucción asociados a un identificador de conexión pueden estar en modo asincrónico, mientras que otros identificadores de instrucción en la misma conexión están en modo sincrónico.  
  
 SQL_AM_NONE: no se admite el modo asincrónico.  
  
 SQL_ASYNC_NOTIFICATION  
 Un valor SQLUINTEGER que indica si el controlador admite la notificación asincrónica:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** El controlador admite la notificación de ejecución asincrónica.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** El controlador no admite la notificación de ejecución asincrónica.  
  
 Hay dos categorías de operaciones asincrónicas ODBC: operaciones asincrónicas de nivel de conexión y operaciones asincrónicas de nivel de instrucción.  Si un controlador devuelve SQL_ASYNC_NOTIFICATION_CAPABLE, debe admitir la notificación para todas las API que puede ejecutar de forma asincrónica.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que enumera el comportamiento del controlador con respecto a la disponibilidad de recuentos de filas. Las siguientes máscaras de bits se utilizan junto con el tipo de información:  
  
 SQL_BRC_ROLLED_UP: los recuentos de filas de las instrucciones INSERT, DELETE o UPDATE consecutivas se acumulan en una sola. Si no se establece este bit, los recuentos de filas están disponibles para cada instrucción.  
  
 SQL_BRC_PROCEDURES: los recuentos de filas, si los hay, están disponibles cuando se ejecuta un lote en un procedimiento almacenado. Si los recuentos de filas están disponibles, se pueden enrollar o individualmente disponibles, dependiendo del SQL_BRC_ROLLED_UP bit.  
  
 SQL_BRC_EXPLICIT: los recuentos de filas, si los hay, están disponibles cuando se ejecuta un lote directamente llamando a **SQLExecute** o **SQLExecDirect**. Si los recuentos de filas están disponibles, se pueden enrollar o individualmente disponibles, dependiendo del SQL_BRC_ROLLED_UP bit.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar la compatibilidad del controlador para lotes. Las siguientes máscaras de bits se utilizan para determinar qué nivel se admite:  
  
 SQL_BS_SELECT_EXPLICIT: el controlador admite lotes explícitos que pueden tener instrucciones de generación de conjuntos de resultados.  
  
 SQL_BS_ROW_COUNT_EXPLICIT: el controlador admite lotes explícitos que pueden tener instrucciones de generación de recuento de filas.  
  
 SQL_BS_SELECT_PROC: el controlador admite procedimientos explícitos que pueden tener instrucciones de generación de conjuntos de resultados.  
  
 SQL_BS_ROW_COUNT_PROC: el controlador admite procedimientos explícitos que pueden tener instrucciones de generación de recuento de filas.  
  
 SQL_BOOKMARK_PERSISTENCE(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las operaciones a través de las cuales persisten los marcadores.  
  
 Las siguientes máscaras de bits se utilizan junto con la marca para determinar a través de qué opciones persisten los marcadores:  
  
 SQL_BP_CLOSE: los marcadores son válidos después de que una aplicación llama a **SQLFreeStmt** con la opción SQL_CLOSE o **SQLCloseCursor** para cerrar el cursor asociado a una instrucción.  
  
 SQL_BP_DELETE: el marcador de una fila es válido después de que se haya eliminado esa fila.  
  
 SQL_BP_DROP: los marcadores son válidos después de que una aplicación llama a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT quitar una instrucción.  
  
 SQL_BP_TRANSACTION: los marcadores son válidos después de que una aplicación confirma o revierte una transacción.  
  
 SQL_BP_UPDATE: el marcador de una fila es válido después de actualizar cualquier columna de esa fila, incluidas las columnas de clave.  
  
 SQL_BP_OTHER_HSTMT: se puede utilizar un marcador asociado a una instrucción con otra instrucción. A menos que se especifique SQL_BP_CLOSE o SQL_BP_DROP, el cursor de la primera instrucción debe estar abierto.  
  
 SQL_CATALOG_LOCATION(ODBC 2.0)  
 Un valor SQLUSMALLINT que indica la posición del catálogo en un nombre de tabla calificado:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Por ejemplo, un controlador de Xbase devuelve SQL_CL_START porque el nombre del directorio (catálogo) está al principio del nombre de la tabla, como en el nombre de la tabla. Dbf. Un controlador de ORACLE Server devuelve SQL_CL_END porque el catálogo ADMIN.EMP@EMPDATAestá al final del nombre de la tabla, como en .  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá SQL_CL_START. Se devuelve un valor de 0 si el origen de datos no admite catálogos. Para determinar si se admiten catálogos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_CATALOG_NAME.  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el SQL_QUALIFIER_LOCATION odbc 2.0 *InfoType.*  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 Una cadena de caracteres: "Y" si el servidor admite nombres de catálogo, o "N" si no lo hace.  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá "Y".  
  
 SQL_CATALOG_NAME_SEPARATOR (ODBC 1.0)  
 Una cadena de caracteres: el carácter o caracteres que el origen de datos define como separador entre un nombre de catálogo y el elemento de nombre completo que sigue o precede a él.  
  
 Se devuelve una cadena vacía si el origen de datos no admite catálogos. Para determinar si se admiten catálogos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_CATALOG_NAME. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá ".".  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el infotype ODBC 2.0 *SQL_QUALIFIER_NAME_SEPARATOR.*  
  
 SQL_CATALOG_TERM (ODBC 1.0)  
 Una cadena de caracteres con el nombre del proveedor del origen de datos para un catálogo; por ejemplo, "base de datos" o "directorio". Esta cadena puede estar en mayúsculas, minúsculas o mixtas.  
  
 Se devuelve una cadena vacía si el origen de datos no admite catálogos. Para determinar si se admiten catálogos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_CATALOG_NAME. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá "catálogo".  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el SQL_QUALIFIER_TERM *de InfoType* ODBC 2.0.  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las instrucciones en las que se pueden usar catálogos.  
  
 Las siguientes máscaras de bits se utilizan para determinar dónde se pueden utilizar los catálogos:  
  
 SQL_CU_DML_STATEMENTS se admiten catálogos en todas las instrucciones de lenguaje de manipulación de datos: **SELECT**, **INSERT**, **UPDATE**, **DELETE**y, si se admite, SELECT **FOR UPDATE** y las instrucciones de actualización y eliminación posicionadas.  
  
 SQL_CU_PROCEDURE_INVOCATION: los catálogos se admiten en la instrucción de invocación de procedimiento ODBC.  
  
 SQL_CU_TABLE_DEFINITION se admiten catálogos en todas las instrucciones de definición de tabla: **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**, DROP **TABLE**y **DROP VIEW**.  
  
 SQL_CU_INDEX_DEFINITION: se admiten catálogos en todas las instrucciones de definición de índice: **CREATE INDEX** y **DROP INDEX**.  
  
 SQL_CU_PRIVILEGE_DEFINITION se admiten los catálogos en todas las instrucciones de definición de privilegios: **GRANT** y **REVOKE**.  
  
 Se devuelve un valor de 0 si el origen de datos no admite catálogos. Para determinar si se admiten catálogos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_CATALOG_NAME. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá una máscara de bits con todos estos bits establecidos.  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el infotype ODBC 2.0 *SQL_QUALIFIER_USAGE.*  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 El nombre de la secuencia de intercalación. Se trata de una cadena de caracteres que indica el nombre de la intercalación predeterminada para el juego de caracteres predeterminado para este servidor (por ejemplo, 'ISO 8859-1' o EBCDIC). Si se desconoce esto, se devolverá una cadena vacía. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá una cadena no vacía.  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite alias de columna; de lo contrario, "N".  
  
 Un alias de columna es un nombre alternativo que se puede especificar para una columna de la lista de selección mediante una cláusula AS. Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá "Y".  
  
 SQL_CONCAT_NULL_BEHAVIOR (ODBC 1.0)  
 Un valor SQLUSMALLINT que indica cómo el origen de datos controla la concatenación de columnas de tipo de datos de caracteres con valores NULL con columnas de tipo de datos de caracteres con valores no NULL:  
  
 SQL_CB_NULL: el resultado es NULL valorado.  
  
 SQL_CB_NON_NULL: el resultado es la concatenación de columnas o columnas con valores no NULL.  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 Una máscara de bits SQLUINTEGER. La máscara de bits indica las conversiones admitidas por el origen de datos con la función escalar **CONVERT** para los datos del tipo denominado en *InfoType*. Si la máscara de bits es igual a cero, el origen de datos no admite ninguna conversión de datos del tipo con nombre, incluida la conversión al mismo tipo de datos.  
  
 Por ejemplo, para determinar si un origen de datos admite la conversión de datos de SQL_INTEGER al tipo de datos SQL_BIGINT, una aplicación llama a **SQLGetInfo** con el *InfoType* de SQL_CONVERT_INTEGER. La aplicación realiza una operación **AND** con la máscara de bits y SQL_CVT_BIGINT de bits devueltas. Si el valor resultante es distinto de cero, se admite la conversión.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué conversiones son compatibles:  
  
 SQL_CVT_BIGINT (ODBC 1.0)SQL_CVT_BINARY (ODBC 1.0)SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5)SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0)SQL_CVT_DECIMAL (ODBC 1.0)SQL_CVT_DOUBLE (ODBC 1.0)SQL_CVT_FLOAT (ODBC 1.0)SQL_CVT_INTEGER (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0)SQL_CVT_LONGVARBINARY (ODBC 1.0)SQL_CVT_LONGVARCHAR (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_ SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1. CVT_REAL ODBC 1.0)SQL_CVT_SMALLINT (ODBC 1.0)SQL_CVT_TIME (ODBC 1.0)SQL_CVT_TIMESTAMP (ODBC 1.0)SQL_CVT_TINYINT (ODBC 1.0)SQL_CVT_VARBINARY (ODBC 1.0)SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones de conversión escalar admitidas por el controlador y el origen de datos asociado.  
  
 La siguiente máscara de bits se utiliza para determinar qué funciones de conversión son compatibles:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME (ODBC 1.0)  
 Un valor SQLUSMALLINT que indica si se admiten nombres de correlación de tabla:  
  
 SQL_CN_NONE no se admiten los nombres de correlación.  
  
 SQL_CN_DIFFERENT: se admiten nombres de correlación, pero deben diferir de los nombres de las tablas que representan.  
  
 SQL_CN_ANY: se admiten los nombres de correlación y pueden ser cualquier nombre válido definido por el usuario.  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá SQL_CN_ANY.  
  
 SQL_CREATE_ASSERTION(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **CREATE ASSERTION,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_CA_CREATE_ASSERTION  
  
 Los bits siguientes especifican el atributo de restricción admitido si se admite explícitamente la capacidad de especificar atributos de restricción (consulte los tipos de información SQL_ALTER_TABLE y SQL_CREATE_TABLE):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones según sea compatible. Un valor devuelto de "0" significa que no se admite la instrucción **CREATE ASSERTION.**  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **CREATE CHARACTER SET,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones según sea compatible. Un valor devuelto de "0" significa que no se admite la instrucción **CREATE CHARACTER SET.**  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **CREATE COLLATION,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 La siguiente máscara de bits se utiliza para determinar qué cláusulas se admiten:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como se admite. Un valor devuelto de "0" significa que no se admite la instrucción **CREATE COLLATION.**  
  
 SQL_CREATE_DOMAIN(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **CREATE DOMAIN,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_CDO_CREATE_DOMAIN: se admite la instrucción CREATE DOMAIN (nivel intermedio).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION \<se admite la definición de nombre de restricción> para asignar nombres a restricciones de dominio (nivel intermedio).  
  
 Los bits siguientes especifican la capacidad de crear restricciones de columna:SQL_CDO_DEFAULT - Se admite la especificación de restricciones de dominio (nivel intermedio)SQL_CDO_CONSTRAINT - Especificar los valores predeterminados de dominio (nivel intermedio)SQL_CDO_COLLATION - Especificar la intercalación de dominio se admite (nivel completo)  
  
 Los bits siguientes especifican los atributos de restricción admitidos si se admite la especificación de restricciones de dominio (se establece SQL_CDO_DEFAULT):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (Nivel completo)SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (Nivel completo)SQL_CDO_CONSTRAINT_DEFERRABLE (Nivel completo)SQL_CDO_CONSTRAINT_NON_DEFERRABLE (Nivel completo)  
  
 Un valor devuelto de "0" significa que no se admite la instrucción **CREATE DOMAIN.**  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **CREATE SCHEMA,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Un controlador compatible con nivel intermedio de SQL-92 siempre devolverá las opciones SQL_CS_CREATE_SCHEMA y SQL_CS_AUTHORIZATION como se admiten. También se deben admitir en el nivel de entrada de SQL-92, pero no necesariamente como instrucciones SQL. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **CREATE TABLE,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_CT_CREATE_TABLE: se admite la instrucción CREATE TABLE. (Nivel de entrada)  
  
 SQL_CT_TABLE_CONSTRAINT: se admite la especificación de restricciones de tabla (nivel de transición DE FIPS)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION: \<se admite la definición de nombre de restricción> cláusula para las restricciones de columna y tabla de nomenclatura (nivel intermedio)  
  
 Los bits siguientes especifican la capacidad de crear tablas temporales:  
  
 SQL_CT_COMMIT_PRESERVE: las filas eliminadas se conservan al confirmar. (Nivel completo) SQL_CT_COMMIT_DELETE: las filas eliminadas se eliminan al confirmar. (Nivel completo) SQL_CT_GLOBAL_TEMPORARY: se pueden crear tablas temporales globales. (Nivel completo) SQL_CT_LOCAL_TEMPORARY: se pueden crear tablas temporales locales. (Nivel completo)  
  
 Los bits siguientes especifican la capacidad de crear restricciones de columna:  
  
 SQL_CT_COLUMN_CONSTRAINT: se admite la especificación de restricciones de columna (nivel de transición de FIPS)SQL_CT_COLUMN_DEFAULT - Especificar valores predeterminados de columna (nivel de transición de FIPS)SQL_CT_COLUMN_COLLATION , se admite la especificación de la intercalación de columnas (nivel completo)  
  
 Los bits siguientes especifican los atributos de restricción admitidos si se admite la especificación de restricciones de columna o tabla:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (nivel completo)SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (nivel completo)SQL_CT_CONSTRAINT_DEFERRABLE (nivel completo)SQL_CT_CONSTRAINT_NON_DEFERRABLE (nivel completo)  
  
 SQL_CREATE_TRANSLATION(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **CREATE TRANSLATION,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 La siguiente máscara de bits se utiliza para determinar qué cláusulas se admiten:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá estas opciones según sea compatible. Un valor devuelto de "0" significa que no se admite la instrucción **CREATE TRANSLATION.**  
  
 SQL_CREATE_VIEW(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **CREATE VIEW,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Un valor devuelto de "0" significa que no se admite la instrucción **CREATE VIEW.**  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá las opciones SQL_CV_CREATE_VIEW y SQL_CV_CHECK_OPTION como se admiten.  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1.0)  
 Un valor SQLUSMALLINT que indica cómo una operación **COMMIT** afecta a cursores y instrucciones preparadas en el origen de datos (el comportamiento del origen de datos al confirmar una transacción).  
  
 El valor de este atributo reflejará el estado actual de la siguiente configuración: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE: cierre los cursores y elimine las instrucciones preparadas. Para volver a utilizar el cursor, la aplicación debe repreparar y volver a ejecutar la instrucción.  
  
 SQL_CB_CLOSE: Cerrar cursores. Para las instrucciones preparadas, la aplicación puede llamar a **SQLExecute** en la instrucción sin llamar a **SQLPrepare** de nuevo. El valor predeterminado para el controlador ODBC de SQL es SQL_CB_CLOSE. Esto significa que el controlador ODBC de SQL cerrará los cursores al confirmar una transacción.  
  
 SQL_CB_PRESERVE: conservar los cursores en la misma posición que antes de la operación **COMMIT.** La aplicación puede continuar capturando datos, o puede cerrar el cursor y volver a ejecutar la instrucción sin volver a prepararla.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR(ODBC 1.0)  
 Un valor SQLUSMALLINT que indica cómo una operación **ROLLBACK** afecta a cursores y instrucciones preparadas en el origen de datos:  
  
 SQL_CB_DELETE: cierre los cursores y elimine las instrucciones preparadas. Para volver a utilizar el cursor, la aplicación debe repreparar y volver a ejecutar la instrucción.  
  
 SQL_CB_CLOSE: Cerrar cursores. Para las instrucciones preparadas, la aplicación puede llamar a **SQLExecute** en la instrucción sin llamar a **SQLPrepare** de nuevo.  
  
 SQL_CB_PRESERVE: conservar los cursores en la misma posición que antes de la operación **ROLLBACK.** La aplicación puede continuar capturando datos, o puede cerrar el cursor y volver a ejecutar la instrucción sin reprepararla.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 Un valor SQLUINTEGER que indica la compatibilidad con la sensibilidad del cursor:  
  
 SQL_INSENSITIVE: todos los cursores del identificador de instrucción muestran el conjunto de resultados sin reflejar los cambios realizados en él por cualquier otro cursor dentro de la misma transacción.  
  
 SQL_UNSPECIFIED: no se especifica si los cursores del identificador de instrucción hacen visibles los cambios realizados en un conjunto de resultados por otro cursor dentro de la misma transacción. Los cursores en el identificador de instrucción pueden hacer visible ninguno, algunos o todos estos cambios.  
  
 SQL_SENSITIVE: los cursores son sensibles a los cambios realizados por otros cursores dentro de la misma transacción.  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá la opción SQL_UNSPECIFIED como se admite.  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá la opción SQL_INSENSITIVE como se admite.  
  
 SQL_DATA_SOURCE_NAME (ODBC 1.0)  
 Cadena de caracteres con el nombre del origen de datos que se usó durante la conexión. Si la aplicación denominada **SQLConnect**, este es el valor del argumento *szDSN.* Si la aplicación denominada **SQLDriverConnect** o **SQLBrowseConnect**, este es el valor de la palabra clave DSN en la cadena de conexión que se pasa al controlador. Si la cadena de conexión no contenía la palabra clave **DSN** (por ejemplo, cuando contiene la palabra clave **DRIVER),** se trata de una cadena vacía.  
  
 SQL_DATA_SOURCE_READ_ONLY (ODBC 1.0)  
 Una cadena de caracteres. "Y" si el origen de datos está establecido en el modo READ ONLY, "N" si es de lo contrario.  
  
 Esta característica pertenece únicamente al propio origen de datos; no es una característica del controlador que permite el acceso al origen de datos. Un controlador que es de lectura y escritura se puede utilizar con un origen de datos que es de solo lectura. Si un controlador es de solo lectura, todos sus orígenes de datos deben ser de solo lectura y deben devolver SQL_DATA_SOURCE_READ_ONLY.  
  
 SQL_DATABASE_NAME(ODBC 1.0)  
 Cadena de caracteres con el nombre de la base de datos actual en uso, si el origen de datos define un objeto con nombre denominado "base de datos".  
  
> [!NOTE]
>  En ODBC 3 *.x*, el valor devuelto para este *InfoType* también se puede devolver llamando a **SQLGetConnectAttr** con un *atributo* argumento de SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar los literales datetime de SQL-92 admitidos por el origen de datos. Tenga en cuenta que estos son los literales datetime enumerados en la especificación SQL-92 y son independientes de las cláusulas de escape literaldatetime definidas por ODBC. Para obtener más información acerca de las cláusulas de escape literal de fecha y hora ODBC, vea [Fecha, Hora y Literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)de marca de tiempo .  
  
 Un controlador compatible con el nivel de transición FIPS siempre devolverá el valor "1" en la máscara de bits para los bits de la lista siguiente. Un valor de "0" significa que no se admiten literales datetime de SQL-92.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué literales son compatibles:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1.0)  
 Cadena de caracteres con el nombre del producto DBMS al que tiene acceso el controlador.  
  
 SQL_DBMS_VER (ODBC 1.0)  
 Cadena de caracteres que indica la versión del producto DBMS al que tiene acceso el controlador. La versión tiene la forma de la versión de la versión de la versión principal, los dos dígitos siguientes son la versión secundaria y los cuatro últimos dígitos son la versión de lanzamiento. El controlador debe representar la versión del producto DBMS en este formulario, pero también puede anexar la versión específica del producto DBMS. Por ejemplo, "04.01.0000 Rdb 4.1".  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 Un valor SQLUINTEGER que indica la compatibilidad con la creación y eliminación de índices:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION(ODBC 1.0)  
 Un valor SQLUINTEGER que indica el nivel de aislamiento de transacción predeterminado admitido por el controlador o el origen de datos, o cero si el origen de datos no admite transacciones. Los siguientes términos se utilizan para definir los niveles de aislamiento de transacción:  
  
 **Lectura sucia** La transacción 1 cambia una fila. La transacción 2 lee la fila modificada antes de que la transacción 1 confirme el cambio. Si la transacción 1 revierte el cambio, la transacción 2 habrá leído una fila que se considera que nunca existió.  
  
 **Lectura no repetible** La transacción 1 lee una fila. La transacción 2 actualiza o elimina esa fila y confirma este cambio. Si la transacción 1 intenta volver a leer la fila, recibirá valores de fila diferentes o descubrirá que la fila se ha eliminado.  
  
 **Phantom** La transacción 1 lee un conjunto de filas que cumplen algunos criterios de búsqueda. La transacción 2 genera una o más filas (mediante inserciones o actualizaciones) que coinciden con los criterios de búsqueda. Si la transacción 1 vuelve a ejecutar la instrucción que lee las filas, recibe un conjunto diferente de filas.  
  
 Si el origen de datos admite transacciones, el controlador devuelve una de las siguientes máscaras de bits:  
  
 SQL_TXN_READ_UNCOMMITTED: son posibles lecturas sucias, lecturas no repetibles y fantasmas.  
  
 SQL_TXN_READ_COMMITTED - No es posible leer sucios. Lecturas y fantasmas no repetibles son posibles.  
  
 SQL_TXN_REPEATABLE_READ- No es posible lecturas sucias y lecturas no repetibles. Los fantasmas son posibles.  
  
 SQL_TXN_SERIALIZABLE: las transacciones son serializables. Las transacciones serializables no permiten lecturas sucias, lecturas no repetibles ni fantasmas.  
  
 SQL_DESCRIBE_PARAMETER(ODBC 3.0)  
 Una cadena de caracteres: "Y" si se pueden describir parámetros; "N", si no.  
  
 Un controlador compatible con el nivel completo de SQL-92 normalmente devolverá "Y" porque admitirá la instrucción **DESCRIBE INPUT.** Sin embargo, dado que esto no especifica directamente la compatibilidad de SQL subyacente, es posible que no se admita la descripción de los parámetros, incluso en un controlador compatible con nivel completo de SQL-92.  
  
 SQL_DM_VER (ODBC 3.0)  
 Una cadena de caracteres con la versión del Administrador de controladores. La versión tiene la forma de . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .  
  
 El primer conjunto de dos dígitos es la versión principal de ODBC, como lo indica la constante SQL_SPEC_MAJOR.  
  
 El segundo conjunto de dos dígitos es la versión ODBC secundaria, como indica la constante SQL_SPEC_MINOR.  
  
 El tercer conjunto de cuatro dígitos es el número de compilación principal del Administrador de controladores.  
  
 El último conjunto de cuatro dígitos es el número de compilación menor del Administrador de controladores.  
  
 La versión del Administrador de controladores de Windows 7 es 03.80. La versión del Administrador de controladores de Windows 8 es 03.81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 Un valor SQLUINTEGER que indica si el controlador admite la agrupación compatible con controladores. (Para obtener más información, consulte Agrupación de [conexiones compatible con controladores](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE indica que el controlador puede admitir el mecanismo de agrupación compatible con el controlador.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE indica que el controlador no puede admitir el mecanismo de agrupación compatible con el controlador.  
  
 Un controlador no necesita implementar SQL_DRIVER_AWARE_POOLING_SUPPORTED y el Administrador de controladores no respetará el valor devuelto del controlador.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1.0)  
 Un valor SQLULEN, el identificador de entorno del controlador o el identificador de conexión, determinado por el argumento *InfoType*.  
  
 El Administrador de controladores solo implementa estos tipos de información.  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 Un valor SQLULEN, el identificador de descriptor del controlador determinado por el identificador \*de descriptor del Administrador de controladores, que se debe pasar en la entrada en *InfoValuePtr* desde la aplicación. En este caso, *InfoValuePtr* es un argumento de entrada y salida. El identificador del \*descriptor de entrada pasado en *InfoValuePtr* debe haberse asignado explícita o implícitamente en *ConnectionHandle*.  
  
 La aplicación debe realizar una copia del identificador de descriptor del Administrador de controladores antes de llamar a **SQLGetInfo** con este tipo de información, para asegurarse de que el identificador no se sobrescribe en la salida.  
  
 El Administrador de controladores solo implementa este tipo de información.  
  
 SQL_DRIVER_HLIB(ODBC 2.0)  
 Un valor SQLULEN, el *hinst* de la biblioteca de carga devuelto al Administrador de controladores cuando cargó el archivo DLL del controlador en un sistema operativo Microsoft Windows, o su equivalente en otro sistema operativo. El identificador solo es válido para el identificador de conexión especificado en la llamada a **SQLGetInfo**.  
  
 El Administrador de controladores solo implementa este tipo de información.  
  
 SQL_DRIVER_HSTMT (ODBC 1.0)  
 Un valor SQLULEN, el identificador de instrucción del controlador determinado por el \*identificador de instrucción del Administrador de controladores, que se debe pasar en la entrada en *InfoValuePtr* desde la aplicación. En este caso, *InfoValuePtr* es una entrada y un argumento de salida. El identificador de \*instrucción de entrada pasado en *InfoValuePtr* debe haberse asignado en el argumento *ConnectionHandle*.  
  
 La aplicación debe realizar una copia del identificador de instrucción del Administrador de controladores antes de llamar a **SQLGetInfo** con este tipo de información, para asegurarse de que el identificador no se sobrescribe en la salida.  
  
 El Administrador de controladores solo implementa este tipo de información.  
  
 SQL_DRIVER_NAME (ODBC 1.0)  
 Cadena de caracteres con el nombre de archivo del controlador utilizado para tener acceso al origen de datos.  
  
 SQL_DRIVER_ODBC_VER(ODBC 2.0)  
 Cadena de caracteres con la versión de ODBC que admite el controlador. La versión tiene la forma de la versión . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . SQL_SPEC_MAJOR y SQL_SPEC_MINOR definir los números de versión principal y secundaria. Para la versión de ODBC que se describe en este manual, estos son 3 y 0, y el controlador debe devolver "03.00".  
  
 El Administrador de controladores ODBC no modificará el valor devuelto de SQLGetInfo(SQL_DRIVER_ODBC_VER) para mantener la compatibilidad con versiones anteriores de las aplicaciones existentes. El controlador especifica qué valor se devolverá. Sin embargo, un controlador que admite la extensibilidad de tipo de datos C debe devolver 3.8 (o superior) cuando una aplicación llama a **SQLSetEnvAttr** para establecer SQL_ATTR_ODBC_VERSION 3.8. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER (ODBC 1.0)  
 Una cadena de caracteres con la versión del controlador y, opcionalmente, una descripción del controlador. Como mínimo, la versión tiene la forma de la versión de la versión principal, los dos dígitos siguientes y los últimos cuatro dígitos son la versión de lanzamiento.  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **DROP ASSERTION,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 La siguiente máscara de bits se utiliza para determinar qué cláusulas se admiten:  
  
 SQL_DA_DROP_ASSERTION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como se admite.  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **DROP CHARACTER SET,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 La siguiente máscara de bits se utiliza para determinar qué cláusulas se admiten:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como se admite.  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **DROP COLLATION,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 La siguiente máscara de bits se utiliza para determinar qué cláusulas se admiten:  
  
 SQL_DC_DROP_COLLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como se admite.  
  
 SQL_DROP_DOMAIN(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **DROP DOMAIN,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Un controlador compatible con nivel intermedio de SQL-92 siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_DROP_SCHEMA(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **DROP SCHEMA,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Un controlador compatible con nivel intermedio de SQL-92 siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_DROP_TABLE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **DROP TABLE,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Un controlador compatible con el nivel de transición de FIPS siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **DROP TRANSLATION,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 La siguiente máscara de bits se utiliza para determinar qué cláusulas se admiten:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá esta opción como se admite.  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **DROP VIEW,** tal como se define en SQL-92, compatible con el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Un controlador compatible con el nivel de transición de FIPS siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor dinámico que son compatibles con el controlador. Esta máscara de bits contiene el primer subconjunto de atributos; para el segundo subconjunto, véase SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué atributos se admiten:  
  
 SQL_CA1_NEXT: un argumento *FetchOrientation* de SQL_FETCH_NEXT se admite en una llamada a **SQLFetchScroll** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_ABSOLUTE de los argumentos *FetchOrientation* de SQL_FETCH_FIRST, SQL_FETCH_LAST y SQL_FETCH_ABSOLUTE se admiten en una llamada a **SQLFetchScroll** cuando el cursor es un cursor dinámico. (El conjunto de filas que se recuperará es independiente de la posición actual del cursor.)  
  
 SQL_CA1_RELATIVE - *FetchOrientation* argumentos de SQL_FETCH_PRIOR y SQL_FETCH_RELATIVE se admiten en una llamada a **SQLFetchScroll** cuando el cursor es un cursor dinámico. (El conjunto de filas que se recuperará depende de la posición actual del cursor. Tenga en cuenta que esto está separado de SQL_FETCH_NEXT porque en un cursor de solo avance, solo se admite SQL_FETCH_NEXT.)  
  
 SQL_CA1_BOOKMARK: un argumento *FetchOrientation* de SQL_FETCH_BOOKMARK se admite en una llamada a **SQLFetchScroll** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_LOCK_EXCLUSIVE: se admite un argumento *LockType* de SQL_LOCK_EXCLUSIVE en una llamada a **SQLSetPos** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_LOCK_NO_CHANGE: se admite un argumento *LockType* de SQL_LOCK_NO_CHANGE en una llamada a **SQLSetPos** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_LOCK_UNLOCK: se admite un argumento *LockType* de SQL_LOCK_UNLOCK en una llamada a **SQLSetPos** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_POS_POSITION: se admite un argumento *Operation* de SQL_POSITION en una llamada a **SQLSetPos** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_POS_UPDATE: se admite un argumento *Operation* de SQL_UPDATE en una llamada a **SQLSetPos** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_POS_DELETE: se admite un argumento *Operation* de SQL_DELETE en una llamada a **SQLSetPos** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_POS_REFRESH: se admite un argumento *Operation* de SQL_REFRESH en una llamada a **SQLSetPos** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_POSITIONED_UPDATE: se admite una instrucción UPDATE WHERE CURRENT OF SQL cuando el cursor es un cursor dinámico. (Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá esta opción como compatible.)  
  
 SQL_CA1_POSITIONED_DELETE: se admite una instrucción DELETE WHERE CURRENT OF SQL cuando el cursor es un cursor dinámico. (Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá esta opción como compatible.)  
  
 SQL_CA1_SELECT_FOR_UPDATE: se admite una instrucción SQL SELECT FOR UPDATE cuando el cursor es un cursor dinámico. (Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá esta opción como compatible.)  
  
 SQL_CA1_BULK_ADD: se admite un argumento *Operation* de SQL_ADD en una llamada a **SQLBulkOperations** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK: se admite un argumento *Operation* de SQL_UPDATE_BY_BOOKMARK en una llamada a **SQLBulkOperations** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK: se admite un argumento *Operation* de SQL_DELETE_BY_BOOKMARK en una llamada a **SQLBulkOperations** cuando el cursor es un cursor dinámico.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK: se admite un argumento *Operation* de SQL_FETCH_BY_BOOKMARK en una llamada a **SQLBulkOperations** cuando el cursor es un cursor dinámico.  
  
 Un controlador compatible con nivel intermedio de SQL-92 normalmente devolverá las opciones SQL_CA1_NEXT, SQL_CA1_ABSOLUTE y SQL_CA1_RELATIVE según se admita, ya que admite cursores desplazables a través de la instrucción FETCH de SQL incrustada. Dado que esto no determina directamente la compatibilidad de SQL subyacente, sin embargo, es posible que no se admitan cursores desplazables, incluso para un controlador compatible con nivel intermedio de SQL-92.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor dinámico que son compatibles con el controlador. Esta máscara de bits contiene el segundo subconjunto de atributos; para el primer subconjunto, véase SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué atributos se admiten:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY: se admite un cursor dinámico de solo lectura, en el que no se permiten actualizaciones. (El atributo de instrucción SQL_ATTR_CONCURRENCY se puede SQL_CONCUR_READ_ONLY para un cursor dinámico).  
  
 SQL_CA2_LOCK_CONCURRENCY: se admite un cursor dinámico que utiliza el nivel más bajo de bloqueo suficiente para asegurarse de que la fila se puede actualizar. (El atributo de instrucción SQL_ATTR_CONCURRENCY se puede SQL_CONCUR_LOCK para un cursor dinámico.) Estos bloqueos deben ser coherentes con el nivel de aislamiento de transacción establecido por el atributo de conexión SQL_ATTR_TXN_ISOLATION.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY: se admite un cursor dinámico que usa el control de simultaneidad optimista que compara las versiones de fila. (El atributo de instrucción SQL_ATTR_CONCURRENCY se puede SQL_CONCUR_ROWVER para un cursor dinámico.)  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY: se admite un cursor dinámico que utiliza el control de simultaneidad optimista que compara valores. (El atributo de instrucción SQL_ATTR_CONCURRENCY se puede SQL_CONCUR_VALUES para un cursor dinámico.)  
  
 SQL_CA2_SENSITIVITY_ADDITIONS: las filas agregadas son visibles para un cursor dinámico; el cursor puede desplazarse a esas filas. (Cuando estas filas se agregan al cursor depende del controlador.)  
  
 SQL_CA2_SENSITIVITY_DELETIONS - Las filas eliminadas ya no están disponibles para un cursor dinámico y no dejan un "agujero" en el conjunto de resultados; después de que el cursor dinámico se desplaza de una fila eliminada, no puede volver a esa fila.  
  
 SQL_CA2_SENSITIVITY_UPDATES: las actualizaciones de las filas son visibles para un cursor dinámico; si el cursor dinámico se desplaza y vuelve a una fila actualizada, los datos devueltos por el cursor son los datos actualizados, no los datos originales.  
  
 SQL_CA2_MAX_ROWS_SELECT: el atributo de instrucción SQL_ATTR_MAX_ROWS afecta a las instrucciones **SELECT** cuando el cursor es un cursor dinámico.  
  
 SQL_CA2_MAX_ROWS_INSERT: el atributo de instrucción SQL_ATTR_MAX_ROWS afecta a las instrucciones **INSERT** cuando el cursor es un cursor dinámico.  
  
 SQL_CA2_MAX_ROWS_DELETE: el atributo de instrucción SQL_ATTR_MAX_ROWS afecta a las instrucciones **DELETE** cuando el cursor es un cursor dinámico.  
  
 SQL_CA2_MAX_ROWS_UPDATE: el atributo de instrucción SQL_ATTR_MAX_ROWS afecta a las instrucciones **UPDATE** cuando el cursor es un cursor dinámico.  
  
 SQL_CA2_MAX_ROWS_CATALOG: el atributo de instrucción SQL_ATTR_MAX_ROWS afecta a los conjuntos de resultados **CATALOG** cuando el cursor es un cursor dinámico.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL: el atributo de instrucción SQL_ATTR_MAX_ROWS afecta a las instrucciones **SELECT**, **INSERT**, **DELETE**y **UPDATE** y a los conjuntos de resultados **CATALOG,** cuando el cursor es dinámico.  
  
 SQL_CA2_CRC_EXACT: el recuento exacto de filas está disponible en el campo de diagnóstico SQL_DIAG_CURSOR_ROW_COUNT cuando el cursor es un cursor dinámico.  
  
 SQL_CA2_CRC_APPROXIMATE: un recuento aproximado de filas está disponible en el campo de diagnóstico SQL_DIAG_CURSOR_ROW_COUNT cuando el cursor es un cursor dinámico.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE: el controlador no garantiza que las instrucciones de actualización o eliminación posicionadas simuladas afectarán a una sola fila cuando el cursor es un cursor dinámico; es responsabilidad de la aplicación garantizarlo. (Si una instrucción afecta a más de una fila, **SQLExecute** o **SQLExecDirect** devuelve SQLSTATE 01001 [conflicto de operación de cursor].) Para establecer este comportamiento, la aplicación llama a **SQLSetStmtAttr** con el atributo SQL_ATTR_SIMULATE_CURSOR establecido en SQL_SC_NON_UNIQUE.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE: el controlador intenta garantizar que las instrucciones de actualización o eliminación posicionadas simuladas afectarán a una sola fila cuando el cursor es un cursor dinámico. El controlador siempre ejecuta estas instrucciones, incluso si pueden afectar a más de una fila, como cuando no hay ninguna clave única. (Si una instrucción afecta a más de una fila, **SQLExecute** o **SQLExecDirect** devuelve SQLSTATE 01001 [conflicto de operación de cursor].) Para establecer este comportamiento, la aplicación llama a **SQLSetStmtAttr** con el atributo SQL_ATTR_SIMULATE_CURSOR establecido en SQL_SC_TRY_UNIQUE.  
  
 SQL_CA2_SIMULATE_UNIQUE: el controlador garantiza que las instrucciones de actualización o eliminación posicionadas simuladas afectarán a una sola fila cuando el cursor sea un cursor dinámico. Si el controlador no puede garantizar esto para una instrucción determinada, **SQLExecDirect** o **SQLPrepare** devuelven SQLSTATE 01001 (conflicto de operación de cursor). Para establecer este comportamiento, la aplicación llama a **SQLSetStmtAttr** con el atributo SQL_ATTR_SIMULATE_CURSOR establecido en SQL_SC_UNIQUE.  
  
 SQL_EXPRESSIONS_IN_ORDERBY(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite expresiones en la lista **ORDER BY;** "N" si no lo hace.  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 Un valor SQLUSMALLINT que indica cómo un controlador de un solo nivel trata directamente los archivos en un origen de datos:  
  
 SQL_FILE_NOT_SUPPORTED: el controlador no es un controlador de un solo nivel. Por ejemplo, un controlador ORACLE es un controlador de dos niveles.  
  
 SQL_FILE_TABLE: un controlador de un solo nivel trata los archivos de un origen de datos como tablas. Por ejemplo, un controlador Xbase trata cada archivo Xbase como una tabla.  
  
 SQL_FILE_CATALOG: un controlador de un solo nivel trata los archivos de un origen de datos como un catálogo. Por ejemplo, un controlador de Microsoft Access trata cada archivo de Microsoft Access como una base de datos completa.  
  
 Una aplicación podría usar esto para determinar cómo seleccionarán los usuarios los datos. Por ejemplo, los usuarios de Xbase a menudo piensan en los datos como almacenados en archivos, mientras que los usuarios de ORACLE y Microsoft Access generalmente piensan en los datos almacenados en tablas.  
  
 Cuando un usuario selecciona un origen de datos Xbase, la aplicación podría mostrar el cuadro de diálogo común **Abrir archivo** de Windows; cuando el usuario selecciona un origen de datos de Microsoft Access u ORACLE, la aplicación podría mostrar un cuadro de diálogo **seleccionar tabla** personalizado.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor de solo avance que son compatibles con el controlador. Esta máscara de bits contiene el primer subconjunto de atributos; para el segundo subconjunto, véase SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué atributos se admiten:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (y sustituya "cursor de solo avance" por "cursor dinámico" en las descripciones).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor de solo avance que son compatibles con el controlador. Esta máscara de bits contiene el segundo subconjunto de atributos; para el primer subconjunto, véase SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué atributos se admiten:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (y sustituya "cursor de solo avance" por "cursor dinámico" en las descripciones).  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar extensiones a **SQLGetData**.  
  
 Las siguientes máscaras de bits se utilizan junto con la marca para determinar qué extensiones comunes admite el controlador para **SQLGetData:**  
  
 SQL_GD_ANY_COLUMN se puede llamar a **SQLGetData** para cualquier columna sin enlazar, incluidas las anteriores a la última columna enlazada. Tenga en cuenta que se debe llamar a las columnas en orden de número de columna ascendente a menos que también se SQL_GD_ANY_ORDER devuelva.  
  
 SQL_GD_ANY_ORDER se puede llamar a **SQLGetData** para las columnas sin enlazar en cualquier orden. Tenga en cuenta que **SQLGetData** solo se puede llamar para las columnas después de la última columna enlazada a menos que también se devuelva SQL_GD_ANY_COLUMN.  
  
 SQL_GD_BLOCK se puede llamar a **SQLGetData** para una columna sin enlazar en cualquier fila de un bloque (donde el tamaño del conjunto de filas es mayor que 1) de datos después de colocarlos en esa fila con **SQLSetPos**.  
  
 SQL_GD_BOUND se puede llamar a **SQLGetData** para las columnas enlazadas además de las columnas sin enlazar. Un controlador no puede devolver este valor a menos que también devuelva SQL_GD_ANY_COLUMN.  
  
 SQL_GD_OUTPUT_PARAMS se puede llamar a **SQLGetData** para devolver valores de parámetro de salida. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **SQLGetData** es necesario devolver datos solo de columnas sin enlazar que se producen después de la última columna enlazada, se llama en orden de aumentar el número de columna y no están en una fila en un bloque de filas.  
  
 Si un controlador admite marcadores (longitud fija o longitud variable), debe admitir la llamada a **SQLGetData** en la columna 0. Esta compatibilidad es necesaria independientemente de lo que devuelve el controlador para una llamada a **SQLGetInfo** con el SQL_GETDATA_EXTENSIONS *InfoType*.  
  
 SQL_GROUP_BY (ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica la relación entre las columnas de la cláusula **GROUP BY** y las columnas no agregadas de la lista de selección:  
  
 SQL_GB_COLLATE: se puede especificar una cláusula **COLLATE** al final de cada columna de agrupación. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED no se admiten las cláusulas **GROUP BY.** (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT: la cláusula **GROUP BY** debe contener todas las columnas no agregadas de la lista de selección. No puede contener ninguna otra columna. Por ejemplo, **SELECT DEPT, MAX(SALARY) FROM EMPLOYEE GROUP BY DEPT**. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT: la cláusula **GROUP BY** debe contener todas las columnas no agregadas de la lista de selección. Puede contener columnas que no están en la lista de selección. Por ejemplo, **SELECT DEPT, MAX(SALARY) FROM EMPLOYEE GROUP BY DEPT, AGE**. (ODBC 2.0)  
  
 SQL_GB_NO_RELATION: las columnas de la cláusula **GROUP BY** y la lista de selección no están relacionadas. El significado de las columnas no agrupadas y no agregadas en la lista de selección depende del origen de datos. Por ejemplo, **SELECT DEPT, SALARY FROM EMPLOYEE GROUP BY DEPT, AGE**. (ODBC 2.0)  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá la opción SQL_GB_GROUP_BY_EQUALS_SELECT como se admite. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá la opción SQL_GB_COLLATE como se admite. Si no se admite ninguna de las opciones, el origen de datos no admite la cláusula **GROUP BY.**  
  
 SQL_IDENTIFIER_CASE (ODBC 1.0)  
 Un valor SQLUSMALLINT como se indica a continuación:  
  
 SQL_IC_UPPER: los identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en mayúsculas en el catálogo del sistema.  
  
 SQL_IC_LOWER: los identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en minúsculas en el catálogo del sistema.  
  
 SQL_IC_SENSITIVE: los identificadores de SQL distinguen entre mayúsculas y minúsculas y se almacenan en mayúsculas y minúsculas mixtas en el catálogo del sistema.  
  
 SQL_IC_MIXED: los identificadores de SQL no distinguen mayúsculas de minúsculas y se almacenan en mayúsculas y minúsculas mixtas en el catálogo del sistema.  
  
 Dado que los identificadores de SQL-92 nunca distinguen mayúsculas de minúsculas, un controlador que se ajusta estrictamente a SQL-92 (cualquier nivel) nunca devolverá la opción SQL_IC_SENSITIVE como se admite.  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1.0)  
 Cadena de caracteres que se utiliza como delimitador inicial y final de un identificador entre comillas (delimitado) en instrucciones SQL. (Los identificadores pasados como argumentos a funciones ODBC no tienen que ser entrecomillados.) Si el origen de datos no admite identificadores entrecomillas, se devuelve un espacio en blanco.  
  
 Esta cadena de caracteres también se puede utilizar para citar argumentos de función de catálogo cuando el atributo de conexión SQL_ATTR_METADATA_ID se establece en SQL_TRUE.  
  
 Dado que el carácter de comillas identificador en SQL-92 es la comilla doble ("), un controlador que se ajusta estrictamente a SQL-92 siempre devolverá el carácter de comillas dobles.  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que enumera las palabras clave de la instrucción CREATE INDEX admitidas por el controlador:  
  
 SQL_IK_NONE: no se admite ninguna de las palabras clave.  
  
 SQL_IK_ASC se admite la palabra clave ASC.  
  
 SQL_IK_DESC se admite la palabra clave DESC.  
  
 SQL_IK_ALL: se admiten todas las palabras clave.  
  
 Para ver si se admite la instrucción CREATE INDEX, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_DLL_INDEX.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las vistas en el INFORMATION_SCHEMA que son compatibles con el controlador. Las vistas y el contenido de INFORMATION_SCHEMA se definen en SQL-92.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué vistas son compatibles:  
  
 SQL_ISV_ASSERTIONS: identifica las aserciones del catálogo que son propiedad de un usuario determinado. (Nivel completo)  
  
 SQL_ISV_CHARACTER_SETS: identifica los conjuntos de caracteres del catálogo a los que puede tener acceso un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_CHECK_CONSTRAINTS: identifica las restricciones CHECK que son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_COLLATIONS: identifica las intercalaciones de caracteres para el catálogo a las que puede tener acceso un usuario determinado. (Nivel completo)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE: identifica las columnas del catálogo que dependen de dominios definidos en el catálogo y que son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_COLUMN_PRIVILEGES: identifica los privilegios en las columnas de tablas persistentes que están disponibles o que un usuario determinado concede o concede. (Nivel de transición FIPS)  
  
 SQL_ISV_COLUMNS: identifica las columnas de tablas persistentes a las que puede tener acceso un usuario determinado. (Nivel de transición FIPS)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE: Similar a CONSTRAINT_TABLE_USAGE vista, las columnas se identifican para las distintas restricciones que son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE: identifica las tablas que utilizan las restricciones (referenciales, únicas y aserciones) y son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS: identifica las restricciones de dominio (de los dominios del catálogo) a las que puede tener acceso un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_DOMAINS: identifica los dominios definidos en un catálogo al que puede tener acceso el usuario. (Nivel intermedio)  
  
 SQL_ISV_KEY_COLUMN_USAGE: identifica las columnas definidas en el catálogo que están restringidas como claves por un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS: identifica las restricciones referenciales que son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_SCHEMATA: identifica los esquemas que son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_SQL_LANGUAGES: identifica los niveles de conformidad de SQL, las opciones y los dialectos admitidos por la implementación de SQL. (Nivel intermedio)  
  
 SQL_ISV_TABLE_CONSTRAINTS: identifica las restricciones de tabla que son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_TABLE_PRIVILEGES: identifica los privilegios de las tablas persistentes que están disponibles o que un usuario determinado concede o concede. (Nivel de transición FIPS)  
  
 SQL_ISV_TABLES: identifica las tablas persistentes definidas en un catálogo al que puede tener acceso un usuario determinado. (Nivel de transición FIPS)  
  
 SQL_ISV_TRANSLATIONS: identifica las traducciones de caracteres para el catálogo a las que puede tener acceso un usuario determinado. (Nivel completo)  
  
 SQL_ISV_USAGE_PRIVILEGES: identifica los privilegios USAGE en los objetos de catálogo que están disponibles para un usuario determinado o que pertenecen a él. (Nivel de transición FIPS)  
  
 SQL_ISV_VIEW_COLUMN_USAGE: identifica las columnas de las que dependen las vistas del catálogo que son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_VIEW_TABLE_USAGE: identifica las tablas de las que dependen las vistas del catálogo que son propiedad de un usuario determinado. (Nivel intermedio)  
  
 SQL_ISV_VIEWS: identifica las tablas vistas definidas en este catálogo a las que puede tener acceso un usuario determinado. (Nivel de transición FIPS)  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que indica compatibilidad con instrucciones **INSERT:**  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_INTEGRITY (ODBC 1.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite Integrity Enhancement Facility; "N" si no lo hace.  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el SQL_ODBC_SQL_OPT_IEF ODBC 2.0 *InfoType.*  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1 (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor de conjunto de claves que son compatibles con el controlador. Esta máscara de bits contiene el primer subconjunto de atributos; para el segundo subconjunto, véase SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué atributos se admiten:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (y sustituya "cursor controlado por conjunto de claves" por "cursor dinámico" en las descripciones).  
  
 Un controlador compatible con nivel intermedio de SQL-92 normalmente devolverá las opciones SQL_CA1_NEXT, SQL_CA1_ABSOLUTE y SQL_CA1_RELATIVE según se admita, ya que el controlador admite cursores desplazables a través de la instrucción FETCH de SQL incrustada. Dado que esto no determina directamente la compatibilidad de SQL subyacente, sin embargo, es posible que no se admitan cursores desplazables, incluso para un controlador compatible con nivel intermedio de SQL-92.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2 (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor de conjunto de claves que son compatibles con el controlador. Esta máscara de bits contiene el segundo subconjunto de atributos; para el primer subconjunto, véase SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué atributos se admiten:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (y sustituya "cursor controlado por conjunto de claves" por "cursor dinámico" en las descripciones).  
  
 SQL_KEYWORDS(ODBC 2.0)  
 Cadena de caracteres que contiene una lista separada por comas de todas las palabras clave específicas del origen de datos. Esta lista no contiene palabras clave específicas de ODBC ni palabras clave utilizadas por el origen de datos y ODBC. Esta lista representa todas las palabras clave reservadas; aplicaciones interoperables no deben utilizar estas palabras en los nombres de objeto.  
  
 Para obtener una lista de palabras clave ODBC, vea [Palabras clave reservadas](../../../odbc/reference/appendixes/reserved-keywords.md) en [Apéndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). El SQL_ODBC_KEYWORDS de valor **#define** contiene una lista separada por comas de palabras clave ODBC.  
  
 Apéndice C: Gramática de SQL  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite un carácter de escape para el carácter de porcentaje (%) y el carácter de subrayado (_) en un predicado **LIKE** y el controlador admite la sintaxis ODBC para definir un carácter de escape de predicado **LIKE;** "N" de lo contrario.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS(ODBC 3.0)  
 Un valor SQLUINTEGER que especifica el número máximo de instrucciones simultáneas activas en modo asincrónico que el controlador puede admitir en una conexión determinada. Si no hay ningún límite específico o el límite es desconocido, este valor es cero.  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 Un valor SQLUINTEGER que especifica la longitud máxima (número de caracteres hexadecimales, excluyendo el prefijo literal y el sufijo devueltos por **SQLGetTypeInfo**) de un literal binario en una instrucción SQL. Por ejemplo, el literal binario 0xFFAA tiene una longitud de 4. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 SQL_MAX_CATALOG_NAME_LEN(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de catálogo en el origen de datos. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 Un controlador compatible con el nivel completo de FIPS devolverá al menos 128.  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el *infotype* ODBC 2.0 SQL_MAX_QUALIFIER_NAME_LEN.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 Un valor SQLUINTEGER que especifica la longitud máxima (número de caracteres, excluyendo el prefijo literal y el sufijo devueltos por **SQLGetTypeInfo**) de un literal de caracteres en una instrucción SQL. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de columna en el origen de datos. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 18. Un controlador compatible con nivel intermedio FIPS devolverá al menos 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitidas en una cláusula **GROUP BY.** Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 6. Un controlador compatible con nivel intermedio FIPS devolverá al menos 15.  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitidas en un índice. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitidas en una cláusula **ORDER BY.** Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 6. Un controlador compatible con nivel intermedio FIPS devolverá al menos 15.  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitidas en una lista de selección. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 100. Un controlador compatible con nivel intermedio FIPS devolverá al menos 250.  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de columnas permitidas en una tabla. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 100. Un controlador compatible con nivel intermedio FIPS devolverá al menos 250.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de instrucciones activas que el controlador puede admitir para una conexión. Una instrucción se define como activa si tiene resultados pendientes, con el término "resultados" que significa filas de una operación **SELECT** o filas afectadas por una operación **INSERT**, **UPDATE**o **DELETE** (como un recuento de filas), o si está en un estado NEED_DATA. Este valor puede reflejar una limitación impuesta por el controlador o el origen de datos. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el SQL_ACTIVE_STATEMENTS odbc 2.0 *InfoType.*  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de cursor en el origen de datos. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 18. Un controlador compatible con nivel intermedio FIPS devolverá al menos 128.  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de conexiones activas que el controlador puede admitir para un entorno. Este valor puede reflejar una limitación impuesta por el controlador o el origen de datos. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el *infotype* ODBC 2.0 SQL_ACTIVE_CONNECTIONS.  
  
 SQL_MAX_IDENTIFIER_LEN(ODBC 3.0)  
 SQLUSMALLINT que indica el tamaño máximo en caracteres que admite el origen de datos para los nombres definidos por el usuario.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 18. Un controlador compatible con nivel intermedio FIPS devolverá al menos 128.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 Un valor SQLUINTEGER que especifica el número máximo de bytes permitidos en los campos combinados de un índice. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de procedimiento en el origen de datos. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 SQL_MAX_ROW_SIZE(ODBC 2.0)  
 Un valor SQLUINTEGER que especifica la longitud máxima de una sola fila en una tabla. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 2.000. Un controlador compatible con nivel intermedio FIPS devolverá al menos 8.000.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG(ODBC 3.0)  
 Una cadena de caracteres: "Y" si el tamaño máximo de fila devuelto para el tipo de información SQL_MAX_ROW_SIZE incluye la longitud de todas las columnas SQL_LONGVARCHAR y SQL_LONGVARBINARY de la fila; "N" de lo contrario.  
  
 SQL_MAX_SCHEMA_NAME_LEN(ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de esquema en el origen de datos. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 18. Un controlador compatible con nivel intermedio FIPS devolverá al menos 128.  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el infotipo ODBC 2.0 *SQL_MAX_OWNER_NAME_LEN.*  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 Un valor SQLUINTEGER que especifica la longitud máxima (número de caracteres, incluido el espacio en blanco) de una instrucción SQL. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de tabla en el origen de datos. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 18. Un controlador compatible con nivel intermedio FIPS devolverá al menos 128.  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de tablas permitidas en la cláusula **FROM** de una instrucción **SELECT.** Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 Un controlador compatible con el nivel de entrada FIPS devolverá al menos 15. Un controlador compatible con nivel intermedio FIPS devolverá al menos 50.  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica la longitud máxima de un nombre de usuario en el origen de datos. Si no hay una longitud máxima o la longitud es desconocida, este valor se establece en cero.  
  
 SQL_MULT_RESULT_SETS(ODBC 1.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite varios conjuntos de resultados, "N" si no lo hace.  
  
 Para obtener más información acerca de varios conjuntos de resultados, vea [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1.0)  
 Una cadena de caracteres: "Y" si el controlador admite más de una transacción activa al mismo tiempo, "N" si solo una transacción puede estar activa en cualquier momento.  
  
 La información devuelta para este tipo de información no se aplica en el caso de transacciones distribuidas.  
  
 SQL_NEED_LONG_DATA_LEN(ODBC 2.0)  
 Una cadena de caracteres: "Y" si el origen de datos necesita la longitud de un valor de datos largo (el tipo de datos es SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo) antes de que ese valor se envíe al origen de datos, "N" si no lo hace. Para obtener más información, vea [SQLBindParameter (función)](../../../odbc/reference/syntax/sqlbindparameter-function.md) y [SQLSetPos (función).](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1.0)  
 Un valor SQLUSMALLINT que especifica si el origen de datos admite NOT NULL en columnas:  
  
 SQL_NNC_NULL: todas las columnas deben tener valores NULL.  
  
 SQL_NNC_NON_NULL: las columnas no pueden aceptar valores NULL. (El origen de datos admite la restricción de columna **NOT NULL** en las instrucciones **CREATE TABLE.)**  
  
 Un controlador compatible con el nivel de entrada de SQL-92 devolverá SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION(ODBC 2.0)  
 Un valor SQLUSMALLINT que especifica dónde se ordenan los valores VALORES NUL en un conjunto de resultados:  
  
 SQL_NC_END: los valores ULUL se ordenan al final del conjunto de resultados, independientemente de las palabras clave ASC o DESC.  
  
 SQL_NC_HIGH- Los valores ULUL se ordenan en el extremo superior del conjunto de resultados, dependiendo de las palabras clave ASC o DESC.  
  
 SQL_NC_LOW, los valores ULUL se ordenan en el extremo más bajo del conjunto de resultados, dependiendo de las palabras clave ASC o DESC.  
  
 SQL_NC_START: los valores ULUL se ordenan al principio del conjunto de resultados, independientemente de las palabras clave ASC o DESC.  
  
 SQL_NUMERIC_FUNCTIONS(ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; cada máscara de bits está etiquetada con la versión en la que se introdujo.  
  
 Una máscara de bits SQLUINTEGER enumerar las funciones numéricas escalares admitidas por el controlador y el origen de datos asociado.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué funciones numéricas son compatibles:  
  
 SQL_FN_NUM_ABS (ODBC 1.0)SQL_FN_NUM_ACOS (ODBC 1.0)SQL_FN_NUM_ASIN (ODBC 1.0)SQL_FN_NUM_ATAN (ODBC 1.0)SQL_FN_NUM_ATAN2 (ODBC 1.0)SQL_FN_NUM_CEILING (ODBC 1.0)SQL_FN_NUM_COS (ODBC 1.0)SQL_FN_NUM_COT (ODBC 1.0)SQL_FN_NUM_DEGREES (ODBC 2.0)SQL_FN_NUM_EXP (ODBC 1.0)SQL_FN_NUM_FLOOR (ODBC 1.0)SQL_FN_NUM_LOG (ODBC 1.0)SQL_FN_NUM_LOG10 (ODBC 2.0)SQL_FN_ NUM_MOD (ODBC 1.0)SQL_FN_NUM_PI (ODBC 1.0)SQL_FN_NUM_POWER (ODBC 2.0)SQL_FN_NUM_RADIANS (ODBC 2.0)SQL_FN_NUM_RAND (ODBC 1.0)SQL_FN_NUM_ROUND (ODBC 2.0)SQL_FN_NUM_SIGN (ODBC 1.0)SQL_FN_NUM_SIN (ODBC 1.0)SQL_FN_NUM_SQRT (ODBC 1.0)SQL_FN_NUM_TAN (ODBC 1.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 Un valor SQLUINTEGER que indica el nivel de la interfaz ODBC 3 *.x* que cumple el controlador.  
  
 SQL_OIC_CORE: el nivel mínimo que se espera que cumplan todos los controladores ODBC. Este nivel incluye elementos básicos de la interfaz como funciones de conexión, funciones para preparar y ejecutar una instrucción SQL, funciones básicas de metadatos del conjunto de resultados, funciones básicas de catálogo, etc.  
  
 SQL_OIC_LEVEL1: Un nivel que incluye la funcionalidad de nivel de cumplimiento de estándares básicos, además de cursores desplazables, marcadores, actualizaciones y eliminaciones posicionadas, etc.  
  
 SQL_OIC_LEVEL2: Un nivel que incluye la funcionalidad de nivel de cumplimiento estándar de nivel 1, además de características avanzadas como cursores sensibles; actualizar, eliminar y actualizar por marcadores; apoyo a procedimientos almacenados; funciones de catálogo para claves principales y externas; Soporte multicatálogo; y así sucesivamente.  
  
 Para obtener más información, consulte Niveles de conformidad de [interfaz](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER (ODBC 1.0)  
 Cadena de caracteres con la versión de ODBC a la que se ajusta el Administrador de controladores. La versión tiene la forma de la versión de la versión de la versión de la versión principal, donde los dos primeros dígitos son la versión principal y los dos dígitos siguientes son la versión secundaria. Esto se implementa solo en el Administrador de controladores.  
  
 SQL_OJ_CAPABILITIES(ODBC 2.01)  
 Una máscara de bits SQLUINTEGER enumerar los tipos de combinaciones externas admitidas por el controlador y el origen de datos. Las siguientes máscaras de bits se utilizan para determinar qué tipos se admiten:  
  
 SQL_OJ_LEFT: se admiten las uniones externas izquierdas.  
  
 SQL_OJ_RIGHT: se admiten las uniones externas derechas.  
  
 SQL_OJ_FULL: se admiten combinaciones externas completas.  
  
 SQL_OJ_NESTED: se admiten las uniones externas anidadas.  
  
 SQL_OJ_NOT_ORDERED: los nombres de columna de la cláusula ON de la combinación externa no tienen que estar en el mismo orden que sus respectivos nombres de tabla en la cláusula **OUTER JOIN.**  
  
 SQL_OJ_INNER la tabla interna (la tabla interna de una combinación externa izquierda o la tabla izquierda en una combinación externa derecha) también se puede utilizar en una combinación interna. Esto no se aplica a las uniones externas completas, que no tienen una tabla interna.  
  
 SQL_OJ_ALL_COMPARISON_OPS: el operador de comparación de la cláusula ON puede ser cualquiera de los operadores de comparación ODBC. Si no se establece este bit, solo se puede utilizar el operador de comparación igual a (-) en combinaciones externas.  
  
 Si ninguna de estas opciones se devuelve como compatible, no se admite ninguna cláusula de combinación externa.  
  
 Para obtener información acerca de la compatibilidad de operadores de combinación relacional en una instrucción SELECT, tal como se define en SQL-92, vea SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 Una cadena de caracteres: "Y" si las columnas de la cláusula **ORDER BY** deben estar en la lista de selección; de lo contrario, "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS(ODBC 3.0)  
 SQLUINTEGER enumerar las propiedades del controlador con respecto a la disponibilidad de recuentos de filas en una ejecución parametrizada. Tiene los siguientes valores:  
  
 SQL_PARC_BATCH: los recuentos de filas individuales están disponibles para cada conjunto de parámetros. Esto es conceptualmente equivalente al controlador que genera un lote de instrucciones SQL, una para cada parámetro establecido en la matriz. La información de error extendida se puede recuperar mediante el campo descriptor de SQL_PARAM_STATUS_PTR.  
  
 SQL_PARC_NO_BATCH: solo hay un recuento de filas disponible, que es el recuento de filas acumulativo resultante de la ejecución de la instrucción para toda la matriz de parámetros. Esto es conceptualmente equivalente a tratar la instrucción junto con la matriz de parámetros completa como una unidad atómica. Los errores se controlan igual que si se ejecutara una instrucción.  
  
 SQL_PARAM_ARRAY_SELECTS(ODBC 3.0)  
 SQLUINTEGER enumerar las propiedades del controlador con respecto a la disponibilidad de conjuntos de resultados en una ejecución parametrizada. Tiene los siguientes valores:  
  
 SQL_PAS_BATCH: hay un conjunto de resultados disponible por conjunto de parámetros. Esto es conceptualmente equivalente al controlador que genera un lote de instrucciones SQL, una para cada parámetro establecido en la matriz.  
  
 SQL_PAS_NO_BATCH: solo hay un conjunto de resultados disponible, que representa el conjunto de resultados acumulativo resultante de la ejecución de la instrucción para la matriz completa de parámetros. Esto es conceptualmente equivalente a tratar la instrucción junto con la matriz de parámetros completa como una unidad atómica.  
  
 SQL_PAS_NO_SELECT: un controlador no permite que se ejecute una instrucción de generación de conjunto de resultados con una matriz de parámetros.  
  
 SQL_PROCEDURE_TERM (ODBC 1.0)  
 Una cadena de caracteres con el nombre del proveedor del origen de datos para un procedimiento; por ejemplo, "procedimiento de base de datos", "procedimiento almacenado", "procedimiento", "paquete" o "consulta almacenada".  
  
 SQL_PROCEDURES (ODBC 1.0)  
 Una cadena de caracteres: "Y" si el origen de datos admite procedimientos y el controlador admite la sintaxis de invocación de procedimiento ODBC; "N" de lo contrario.  
  
 SQL_POS_OPERATIONS(ODBC 2.0)  
 Una máscara de bits SQLINTEGER enumerar las operaciones de soporte en **SQLSetPos**.  
  
 Las siguientes máscaras de bits se utilizan junto con la marca para determinar qué opciones se admiten.  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 Un valor SQLUSMALLINT como se indica a continuación:  
  
 SQL_IC_UPPER: los identificadores entre comillas en SQL no distinguen mayúsculas de minúsculas y se almacenan en mayúsculas en el catálogo del sistema.  
  
 SQL_IC_LOWER: los identificadores entre comillas en SQL no distinguen mayúsculas de minúsculas y se almacenan en minúsculas en el catálogo del sistema.  
  
 SQL_IC_SENSITIVE: los identificadores entre comillas en SQL distinguen entre mayúsculas y minúsculas y se almacenan en mayúsculas y minúsculas mixtas en el catálogo del sistema. (En una base de datos compatible con SQL-92, los identificadores entre comillas siempre distinguen mayúsculas de minúsculas.)  
  
 SQL_IC_MIXED: los identificadores entre comillas en SQL no distinguen mayúsculas de minúsculas y se almacenan en mayúsculas y minúsculas mixtas en el catálogo del sistema.  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá SQL_IC_SENSITIVE.  
  
 SQL_ROW_UPDATES(ODBC 1.0)  
 Una cadena de caracteres: "Y" si un cursor mixto o controlado por conjunto de claves mantiene versiones de fila o valores para todas las filas recuperadas y, por lo tanto, puede detectar las actualizaciones realizadas en una fila por cualquier usuario desde la última vez que se obtuvo la fila. (Esto solo se aplica a las actualizaciones, no a las eliminaciones o inserciones.) El controlador puede devolver el SQL_ROW_UPDATED marca a la matriz de estado de fila cuando **SQLFetchScroll** se llama. De lo contrario, "N".  
  
 SQL_SCHEMA_TERM (ODBC 1.0)  
 Una cadena de caracteres con el nombre del proveedor del origen de datos para un esquema; por ejemplo, "propietario", "ID de autorización" o "Esquema".  
  
 La cadena de caracteres se puede devolver en mayúsculas, minúsculas o mayúsculas y minúsculas.  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá "esquema".  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el infotype ODBC 2.0 *SQL_OWNER_TERM.*  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 Una máscara de bits SQLUINTEGER que enumera las instrucciones en las que se pueden utilizar esquemas:  
  
 SQL_SU_DML_STATEMENTS se admiten esquemas en todas las instrucciones de lenguaje de manipulación de datos: **SELECT**, **INSERT**, **UPDATE**, **DELETE**y, si se admite, SELECT **FOR UPDATE** y las instrucciones de actualización y eliminación posicionadas.  
  
 SQL_SU_PROCEDURE_INVOCATION: se admiten esquemas en la instrucción de invocación de procedimiento ODBC.  
  
 SQL_SU_TABLE_DEFINITION se admiten esquemas en todas las instrucciones de definición de tabla: **CREATE TABLE**, **CREATE VIEW**, ALTER **TABLE**, **DROP TABLE**y DROP **VIEW**.  
  
 SQL_SU_INDEX_DEFINITION: se admiten esquemas en todas las instrucciones de definición de índice: **CREATE INDEX** y **DROP INDEX**.  
  
 SQL_SU_PRIVILEGE_DEFINITION se admiten esquemas en todas las instrucciones de definición de privilegios: **GRANT** y **REVOKE**.  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá las opciones SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION y SQL_SU_PRIVILEGE_DEFINITION, según sea compatible.  
  
 Este *InfoType* se ha cambiado el nombre para ODBC 3.0 desde el infotype ODBC 2.0 *SQL_OWNER_USAGE.*  
  
 SQL_SCROLL_OPTIONS (ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; cada máscara de bits está etiquetada con la versión en la que se introdujo.  
  
 Una máscara de bits SQLUINTEGER enumerar las opciones de desplazamiento admitidas para cursores desplazables.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué opciones son compatibles:  
  
 SQL_SO_FORWARD_ONLY: el cursor solo se desplaza hacia delante. (ODBC 1.0)  
  
 SQL_SO_STATIC: los datos del conjunto de resultados son estáticos. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN: el controlador guarda y utiliza las claves para cada fila del conjunto de resultados. (ODBC 1.0)  
  
 SQL_SO_DYNAMIC: el controlador mantiene las claves de cada fila del conjunto de filas (el tamaño del conjunto de claves es el mismo que el tamaño del conjunto de filas). (ODBC 1.0)  
  
 SQL_SO_MIXED: el controlador mantiene las claves de cada fila del conjunto de claves y el tamaño del conjunto de claves es mayor que el tamaño del conjunto de filas. El cursor está controlado por conjunto de claves dentro del conjunto de claves y dinámico fuera del conjunto de claves. (ODBC 1.0)  
  
 Para obtener información sobre los cursores desplazables, consulte [Cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 SQL_SEARCH_PATTERN_ESCAPE(ODBC 1.0)  
 Cadena de caracteres que especifica lo que el controlador admite como carácter de escape que permite el uso de los metacaracteres de coincidencia de patrón (_) y signo de porcentaje (%) como caracteres válidos en los patrones de búsqueda. Este carácter de escape solo se aplica a los argumentos de función de catálogo que admiten cadenas de búsqueda. Si esta cadena está vacía, el controlador no admite un carácter de escape de patrón de búsqueda.  
  
 Dado que este tipo de información no indica compatibilidad general del carácter de escape en el predicado **LIKE,** SQL-92 no incluye requisitos para esta cadena de caracteres.  
  
 Este *InfoType* está limitado a funciones de catálogo. Para obtener una descripción del uso del carácter de escape en cadenas de patrón de búsqueda, vea Argumentos de valor de [patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER_NAME(ODBC 1.0)  
 Una cadena de caracteres con el nombre de servidor específico del origen de datos real; resulta útil cuando se utiliza un nombre de origen de datos durante **SQLConnect**, **SQLDriverConnect**y **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS(ODBC 2.0)  
 Cadena de caracteres que contiene todos los caracteres especiales (es decir, todos los caracteres excepto a z, de la A a la Z, de 0 a 9 y de subrayado) que se pueden utilizar en un nombre de identificador, como un nombre de tabla, un nombre de columna o un nombre de índice, en el origen de datos. Por ejemplo, "$". Si un identificador contiene uno o varios de estos caracteres, el identificador debe ser un identificador delimitado.  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 Un valor SQLUINTEGER que indica el nivel de SQL-92 admitido por el controlador:  
  
 SQL_SC_SQL92_ENTRY: compatible con SQL-92 de nivel de entrada.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL: cumple con el nivel de transición FIPS 127-2.  
  
 SQL_SC_SQL92_FULL: compatible con SQL-92 de nivel completo.  
  
 SQL_SC_ SQL92_INTERMEDIATE: compatible con SQL-92 de nivel intermedio.  
  
 SQL_SQL92_DATETIME_FUNCTIONS (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones escalares datetime que son compatibles con el controlador y el origen de datos asociado, tal como se define en SQL-92.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué funciones de fecha y hora son compatibles:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las reglas admitidas para una clave externa en una instrucción **DELETE,** tal como se define en SQL-92.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas admite el origen de datos:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Un controlador compatible con el nivel de transición de FIPS siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las reglas admitidas para una clave externa en una instrucción **UPDATE,** tal como se define en SQL-92.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas admite el origen de datos:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas admitidas en la instrucción **GRANT,** tal como se define en SQL-92.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas admite el origen de datos:  
  
 SQL_SG_DELETE_TABLE (Nivel de entrada)SQL_SG_INSERT_COLUMN (Nivel intermedio)SQL_SG_INSERT_TABLE (Nivel de entrada) SQL_SG_REFERENCES_TABLE (Nivel de entrada)SQL_SG_REFERENCES_COLUMN (Nivel de entrada)SQL_SG_SELECT_TABLE (Nivel de entrada)SQL_SG_UPDATE_COLUMN (Nivel de entrada)SQL_SG_UPDATE_TABLE (Nivel de entrada) SQL_SG_USAGE_ON_DOMAIN (nivel de transición FIPS)SQL_SG_USAGE_ON_CHARACTER_SET (nivel de transición FIPS)SQL_SG_USAGE_ON_COLLATION (nivel de transición FIPS)SQL_SG_USAGE_ON_TRANSLATION (FIPS Transitional nivel)SQL_SG_WITH_GRANT_OPTION (Nivel de entrada)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones escalares de valor numérico que son compatibles con el controlador y el origen de datos asociado, tal como se define en SQL-92.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué funciones numéricas son compatibles:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar los predicados admitidos en una instrucción **SELECT,** tal como se define en SQL-92.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué opciones admite el origen de datos:  
  
 SQL_SP_BETWEEN (Nivel de entrada)SQL_SP_COMPARISON (Nivel de entrada)SQL_SP_EXISTS (Nivel de entrada)SQL_SP_IN (Nivel de entrada)SQL_SP_ISNOTNULL (Nivel de entrada)SQL_SP_ISNULL (Nivel de entrada)SQL_SP_LIKE (Nivel de entrada)SQL_SP_MATCH_FULL (Nivel completo)SQL_SP_MATCH_PARTIAL(Nivel completo)SQL_SP_MATCH_UNIQUE_FULL (Nivel completo)SQL_SP_MATCH_UNIQUE_PARTIAL (Nivel completo)SQL_SP_OVERLAPS (Nivel de transición FIPS)SQL_SP_QUANTIFIED_COMPARISON (Nivel de entrada)SQL_SP_UNIQUE (Nivel de entrada)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar los operadores de combinación relacional admitidos en una instrucción **SELECT,** tal como se define en SQL-92.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué opciones admite el origen de datos:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (nivel intermedio)SQL_SRJO_CROSS_JOIN (nivel completo)SQL_SRJO_EXCEPT_JOIN (nivel intermedio)SQL_SRJO_FULL_OUTER_JOIN (nivel intermedio) SQL_SRJO_INNER_JOIN (nivel de transición FIPS)SQL_SRJO_INTERSECT_JOIN (nivel intermedio)SQL_SRJO_LEFT_OUTER_JOIN (nivel de transición FIPS)SQL_SRJO_NATURAL_JOIN (nivel de transición FIPS)SQL_SRJO_RIGHT_OUTER_JOIN (nivel de transición FIPS)SQL_SRJO_UNION_JOIN (nivel completo)  
  
 SQL_SRJO_INNER_JOIN indica compatibilidad con la sintaxis **INNER JOIN,** no para la capacidad de combinación interna. La compatibilidad con la sintaxis **INNER JOIN** es FIPS TRANSITIONAL, mientras que la compatibilidad con la capacidad de combinación interna es **ENTRY**.  
  
 SQL_SQL92_REVOKE (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas admitidas en la instrucción **REVOKE,** tal como se define en SQL-92, admitida por el origen de datos.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas admite el origen de datos:  
  
 SQL_SR_CASCADE (nivel de transición FIPS) SQL_SR_DELETE_TABLE (nivel de entrada)SQL_SR_GRANT_OPTION_FOR (nivel intermedio) SQL_SR_INSERT_COLUMN (nivel intermedio)SQL_SR_INSERT_TABLE (nivel de entrada)SQL_SR_REFERENCES_COLUMN (nivel de entrada)SQL_SR_REFERENCES_TABLE (nivel de entrada)SQL_SR_RESTRICT (nivel de transición FIPS)SQL_SR_SELECT_TABLE (nivel de entrada)SQL_SR_UPDATE_COLUMN (nivel de entrada)SQL_SR_UPDATE_TABLE (nivel de entrada)SQL_SR_USAGE_ON_DOMAIN (nivel de transición FIPS)SQL_SR_USAGE_ON_CHARACTER_ SET (nivel de transición FIPS)SQL_SR_USAGE_ON_COLLATION (nivel de transición FIPS)SQL_SR_USAGE_ON_TRANSLATION (nivel de transición FIPS)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las expresiones de constructor de valor de fila admitidas en una instrucción **SELECT,** tal como se define en SQL-92. Las siguientes máscaras de bits se utilizan para determinar qué opciones admite el origen de datos:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones escalares de cadena que son compatibles con el controlador y el origen de datos asociado, tal como se define en SQL-92.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué funciones de cadena son compatibles:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las expresiones de valor admitidas, tal como se define en SQL-92.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué opciones admite el origen de datos:  
  
 SQL_SVE_CASE (nivel intermedio)SQL_SVE_CAST (nivel de transición FIPS)SQL_SVE_COALESCE (nivel intermedio)SQL_SVE_NULLIF (nivel intermedio)  
  
 SQL_STANDARD_CLI_CONFORMANCE(ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar el estándar de la CLI o los estándares a los que se ajusta el controlador. Las siguientes máscaras de bits se utilizan para determinar qué niveles cumple el controlador:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: El controlador cumple con la versión 1 de la CLI de Open Group.  
  
 SQL_SCC_ISO92_CLI: El controlador cumple con la CLI ISO 92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1 (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor estático admitidos por el controlador. Esta máscara de bits contiene el primer subconjunto de atributos; para el segundo subconjunto, consulte SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué atributos se admiten:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (y sustituya "cursor estático" por "cursor dinámico" en las descripciones).  
  
 Un controlador compatible con nivel intermedio de SQL-92 normalmente devolverá las opciones SQL_CA1_NEXT, SQL_CA1_ABSOLUTE y SQL_CA1_RELATIVE según se admita, ya que el controlador admite cursores desplazables a través de la instrucción FETCH de SQL incrustada. Dado que esto no determina directamente la compatibilidad de SQL subyacente, sin embargo, es posible que no se admitan cursores desplazables, incluso para un controlador compatible con nivel intermedio de SQL-92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2 (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que describe los atributos de un cursor estático admitidos por el controlador. Esta máscara de bits contiene el segundo subconjunto de atributos; para el primer subconjunto, véase SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué atributos se admiten:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Para obtener descripciones de estas máscaras de bits, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (y sustituya "cursor estático" por "cursor dinámico" en las descripciones).  
  
 SQL_STRING_FUNCTIONS (ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; cada máscara de bits está etiquetada con la versión en la que se introdujo.  
  
 Una máscara de bits SQLUINTEGER enumerar las funciones de cadena escalar admitidas por el controlador y el origen de datos asociado.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué funciones de cadena son compatibles:  
  
 SQL_FN_STR_ASCII (ODBC 1.0)SQL_FN_STR_BIT_LENGTH (ODBC 3.0)SQL_FN_STR_CHAR (ODBC 1.0)SQL_FN_STR_CHAR_LENGTH (ODBC 3.0)SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0)SQL_FN_STR_CONCAT (ODBC 1.0)SQL_FN_STR_DIFFERENCE (ODBC 2.0)SQL_FN_STR_INSERT (ODBC 1.0)SQL_FN_STR_LCASE (ODBC 1.0)SQL_FN_STR_LEFT (ODBC 1.0)SQL_FN_STR_LENGTH (ODBC 1.0)SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0)SQL_FN_STR_REPEAT (ODBC 1.0)SQL_FN_STR_REPLACE (ODBC 1.0)SQL_FN_STR_RIGHT (ODBC 1.0)SQL_FN_STR_RTRIM (ODBC 1.0)SQL_FN_STR_SOUNDEX (ODBC 2.0)SQL_FN_STR_SPACE (ODBC 2.0)SQL_FN_STR_SUBSTRING (ODBC 1.0)SQL_FN_STR_UCASE (ODBC 1.0)  
  
 Si una aplicación puede llamar a la función escalar **LOCATE** con los argumentos *string_exp1*, *string_exp2*e *start,* el controlador devuelve la máscara de bits SQL_FN_STR_LOCATE. Si una aplicación puede llamar a la función escalar LOCATE con solo los argumentos *string_exp1* y *string_exp2,* el controlador devuelve la máscara de bits SQL_FN_STR_LOCATE_2. Los controladores que admiten completamente la función escalar **LOCATE** devuelven ambas máscaras de bits.  
  
 (Para obtener más información, consulte [Funciones](../../../odbc/reference/appendixes/string-functions.md) de cadena en el Apéndice E, "Funciones escalares.")  
  
 SQL_SUBQUERIES(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER que enumera los predicados que admiten subconsultas:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 La máscara de bits SQL_SQ_CORRELATED_SUBQUERIES indica que todos los predicados que admiten subconsultas admiten subconsultas correlacionadas.  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá una máscara de bits en la que se establecen todos estos bits.  
  
 SQL_SYSTEM_FUNCTIONS(ODBC 1.0)  
 Una máscara de bits SQLUINTEGER enumerar las funciones escalares del sistema admitidas por el controlador y el origen de datos asociado.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué funciones del sistema son compatibles:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1.0)  
 Una cadena de caracteres con el nombre del proveedor del origen de datos para una tabla; por ejemplo, "tabla" o "archivo".  
  
 Esta cadena de caracteres puede estar en mayúsculas, minúsculas o mixtas.  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá "tabla".  
  
 SQL_TIMEDATE_ADD_INTERVALS(ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar los intervalos de marca de tiempo admitidos por el controlador y el origen de datos asociado para la función escalar TIMESTAMPADD.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué intervalos se admiten:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un controlador compatible con el nivel de transición FIPS siempre devolverá una máscara de bits en la que se establecen todos estos bits.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar los intervalos de marca de tiempo admitidos por el controlador y el origen de datos asociado para la función escalar TIMESTAMPDIFF.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué intervalos se admiten:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un controlador compatible con el nivel de transición FIPS siempre devolverá una máscara de bits en la que se establecen todos estos bits.  
  
 SQL_TIMEDATE_FUNCTIONS (ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; cada máscara de bits está etiquetada con la versión en la que se introdujo.  
  
 Una máscara de bits SQLUINTEGER enumerar las funciones escalares de fecha y hora admitidas por el controlador y el origen de datos asociado.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué funciones de fecha y hora son compatibles:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0)SQL_FN_TD_CURRENT_TIME (ODBC 3.0)SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0)SQL_FN_TD_CURDATE (ODBC 1.0)SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0)SQL_FN_TD_DAYOFMONTH (ODBC 1.0)SQL_FN_TD_DAYOFWEEK (ODBC 1.0)SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0)SQL_FN_TD_HOUR (ODBC 1.0)SQL_FN_TD_MINUTE (ODBC 1.0)SQL_FN_TD_MONTH (ODBC 1.0)SQL_FN_TD_MONTH (ODBC 1.0)SQL_FN_TD_MONTHNAME (ODBC 2.0)SQL_FN_TD_NOW (ODBC 1.0)SQL_FN_TD_QUARTER (ODBC 1.0)SQL_FN_TD_SECOND (ODBC 1.0)SQL_FN_TD_TIMESTAMPADD (ODBC 2.0)SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0)SQL_FN_TD_WEEK (ODBC 1.0)SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE (ODBC 1.0)  
 Nota: El tipo de información se introdujo en ODBC 1.0; cada valor devuelto se etiqueta con la versión en la que se introdujo.  
  
 Un valor SQLUSMALLINT que describe la compatibilidad de transacciones en el controlador o el origen de datos:  
  
 SQL_TC_NONE: no se admiten transacciones. (ODBC 1.0)  
  
 SQL_TC_DML: las transacciones solo pueden contener instrucciones de lenguaje de manipulación de datos (DML) (**SELECT**, **INSERT**, **UPDATE**, **DELETE**). Las instrucciones de lenguaje de definición de datos (DDL) encontradas en una transacción producen un error. (ODBC 1.0)  
  
 SQL_TC_DDL_COMMIT: las transacciones solo pueden contener instrucciones DML. Las instrucciones DDL (**CREATE TABLE**, **DROP INDEX**, etc.) encontradas en una transacción hacen que se confirme la transacción. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE: las transacciones solo pueden contener instrucciones DML. Las instrucciones DDL encontradas en una transacción se omiten. (ODBC 2.0)  
  
 SQL_TC_ALL: las transacciones pueden contener instrucciones DDL e instrucciones DML en cualquier orden. (ODBC 1.0)  
  
 (Debido a que la compatibilidad con transacciones es obligatoria en SQL-92, un controlador compatible con SQL-92 [cualquier nivel] nunca devolverá SQL_TC_NONE.)  
  
 SQL_TXN_ISOLATION_OPTION(ODBC 1.0)  
 Una máscara de bits SQLUINTEGER enumerar los niveles de aislamiento de transacción disponibles desde el controlador o el origen de datos.  
  
 Las siguientes máscaras de bits se utilizan junto con la marca para determinar qué opciones se admiten:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Para obtener descripciones de estos niveles de aislamiento, consulte la descripción de SQL_DEFAULT_TXN_ISOLATION.  
  
 Para establecer el nivel de aislamiento de transacción, una aplicación llama a **SQLSetConnectAttr** para establecer el atributo SQL_ATTR_TXN_ISOLATION. Para obtener más información, vea [Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá SQL_TXN_SERIALIZABLE como se admite. Un controlador compatible con el nivel de transición FIPS siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_UNION (ODBC 2.0)  
 Una máscara de bits SQLUINTEGER que enumera la compatibilidad con la cláusula **UNION:**  
  
 SQL_U_UNION: el origen de datos admite la cláusula **UNION.**  
  
 SQL_U_UNION_ALL: el origen de datos admite la palabra clave **ALL** en la cláusula **UNION.** (**SQLGetInfo** devuelve SQL_U_UNION y SQL_U_UNION_ALL en este caso.)  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá ambas opciones según sea compatible.  
  
 SQL_USER_NAME (ODBC 1.0)  
 Una cadena de caracteres con el nombre utilizado en una base de datos determinada, que puede ser diferente del nombre de inicio de sesión.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 Cadena de caracteres que indica el año de publicación de la especificación de grupo abierto con la que la versión del Administrador de controladores ODBC cumple plenamente.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 Una cadena de caracteres: "Y" si el usuario puede ejecutar todos los procedimientos devueltos por **SQLProcedures**; "N" si puede haber procedimientos devueltos que el usuario no puede ejecutar.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 Una cadena de caracteres: "Y" si se garantiza al usuario privilegios **SELECT** para todas las tablas devueltas por **SQLTables**; "N" si puede haber tablas devueltas a las que el usuario no pueda acceder.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 Un valor SQLUSMALLINT que especifica el número máximo de entornos activos que el controlador puede admitir. Si no hay ningún límite especificado o el límite es desconocido, este valor se establece en cero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER que enumera la compatibilidad con funciones de agregación:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un controlador compatible con el nivel de entrada de SQL-92 siempre devolverá todas estas opciones según sea compatible.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **ALTER DOMAIN,** tal como se define en SQL-92, compatible con el origen de datos. Un controlador compatible con el nivel completo de SQL-92 siempre devolverá todas las máscaras de bits. Un valor devuelto de "0" significa que no se admite la instrucción **ALTER DOMAIN.**  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT: se admite la adición de una restricción de dominio (nivel completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT: \<modificar \<la cláusula predeterminada de> dominio establecida> (nivel completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<se admite la cláusula de definición de nombre de restricción> para asignar nombres a la restricción de dominio (nivel intermedio)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<se admite la cláusula de restricción de dominio de colocación> (nivel completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT: \<modificar \<la cláusula predeterminada de> dominio de colocación> (nivel completo)  
  
 Los bits siguientes \<especifican los \<atributos de restricción admitidos> si se admite agregar> de restricción de dominio (se establece el bit SQL_AD_ADD_DOMAIN_CONSTRAINT):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (Nivel completo)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (Nivel completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (Nivel completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (Nivel completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Una máscara de bits SQLUINTEGER enumerar las cláusulas de la instrucción **ALTER TABLE** admitida por el origen de datos.  
  
 El nivel de conformidad de SQL-92 o FIPS en el que se debe admitir esta característica se muestra entre paréntesis junto a cada máscara de bits.  
  
 Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:  
  
 SQL_AT_ADD_COLUMN_COLLATION \<se admite la cláusula de> de columna de agregar, con facilidad para especificar la intercalación de columnas (nivel completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<se admite la cláusula de> de columna de agregar, con facilidad para especificar los valores predeterminados de columna (nivel de transición de FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE \<se admite la> de agregar columna (nivel de transición DE FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT \<se admite la cláusula de> de columna de agregar, con facilidad para especificar restricciones de columna (nivel de transición DE FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<se admite la cláusula de> de restricción de tabla de agregar (nivel de transición FIPS) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<se admite la definición de nombre de restricción> para las restricciones de columna y tabla de nomenclatura (nivel intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE \<se admite la columna de colocación> CASCADE (nivel de transición de FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<se admite \<la cláusula predeterminada de la columna de modificación> de la columna de colocación> (nivel intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT \<se admite la columna de colocación> RESTRICT (nivel de transición DE FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<se admite la> de la columna de colocación> DE restricción (nivel de transición DE FIPS) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<se admite \<la cláusula predeterminada de la columna de modificación> de columna> (nivel intermedio) (ODBC 3.0)  
  
 Los bits siguientes \<especifican los atributos de restricción de soporte> si se admite la especificación de restricciones de columna o tabla (se establece el bit SQL_AT_ADD_CONSTRAINT):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (Nivel completo) (ODBC 3.0)SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (Nivel completo) (ODBC 3.0)SQL_AT_CONSTRAINT_DEFERRABLE (Nivel completo) (ODBC 3.0)SQL_AT_CONSTRAINT_NON_DEFERRABLE (Nivel completo) (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Un valor SQLUINTEGER que indica el nivel de compatibilidad asincrónica en el controlador:  
  
 SQL_AM_CONNECTION: se admite la ejecución asincrónica de nivel de conexión. Todos los identificadores de instrucción asociados a un identificador de conexión determinado están en modo asincrónico o todos están en modo sincrónico. Un identificador de instrucción en una conexión no puede estar en modo asincrónico mientras que otro identificador de instrucción en la misma conexión está en modo sincrónico y viceversa.  
  
 SQL_AM_STATEMENT: se admite la ejecución asincrónica de nivel de instrucción. Algunos identificadores de instrucción asociados a un identificador de conexión pueden estar en modo asincrónico, mientras que otros identificadores de instrucción en la misma conexión están en modo sincrónico.  
  
 SQL_AM_NONE: no se admite el modo asincrónico.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Una máscara de bits SQLUINTEGER enumerar el comportamiento del controlador con respecto a la disponibilidad de recuentos de filas. Las siguientes máscaras de bits se utilizan junto con el tipo de información:  
  
 SQL_BRC_ROLLED_UP: los recuentos de filas de las instrucciones INSERT, DELETE o UPDATE consecutivas se acumulan en una sola. Si no se establece este bit, los recuentos de filas están disponibles para cada instrucción.  
  
 SQL_BRC_PROCEDURES: los recuentos de filas, si los hay, están disponibles cuando se ejecuta un lote en un procedimiento almacenado. Si los recuentos de filas están disponibles, se pueden enrollar o individualmente disponibles, dependiendo del SQL_BRC_ROLLED_UP bit.  
  
 SQL_BRC_EXPLICIT: los recuentos de filas, si los hay, están disponibles cuando se ejecuta un lote directamente llamando a **SQLExecute** o **SQLExecDirect**. Si los recuentos de filas están disponibles, se pueden enrollar o individualmente disponibles, dependiendo del SQL_BRC_ROLLED_UP bit.  
  
## <a name="example"></a>Ejemplo  
 **SQLGetInfo** devuelve listas de opciones admitidas como una máscara de bits SQLUINTEGER en **InfoValuePtr*. La máscara de bits para cada opción se utiliza junto con la marca para determinar si se admite la opción.  
  
 Por ejemplo, una aplicación podría usar el código siguiente para determinar si el controlador asociado a la conexión admite la función escalar SUBSTRING.  
  
 Para obtener otro ejemplo de uso de **SQLGetInfo**, vea [SQLTables (Función)](../../../odbc/reference/syntax/sqltables-function.md).  
  
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
 Devolver la configuración de un atributo de conexión  
 [Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 Determinar si un controlador admite una función  
 [Función SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Devolver la configuración de un atributo de instrucción  
 [Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Devolver información sobre los tipos de datos de un origen de datos  
 [Función SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
