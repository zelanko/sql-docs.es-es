---
title: SQLGetInfo devuelve valores para el acceso a | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- SQLGetInfo function [ODBC], Access Driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], SQLGetInfo
ms.assetid: c551e07f-30c4-41a2-8991-6010a3511d76
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1b830be937d31e763fbbf517ef07a3c2b8c729d3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-returned-values-for-access"></a>SQLGetInfo devuelve valores para el acceso
La tabla siguiente enumera el lenguaje C# defines para la *fInfoType* argumento y los correspondientes valores devueltos por **SQLGetInfo**. Esta información se puede recuperar pasando el lenguaje c. enumerado #defines a **SQLGetInfo** en el *fInfoType* argumento. Para obtener más información acerca de los valores devueltos por **SQLGetInfo**, consulte el *referencia del programador de ODBC*.  
  
> [!NOTE]  
>  Donde **SQLGetInfo** devuelve una máscara de bits de 32 bits, una barra vertical (&#124;) representa una operación OR bit a bit.  
  
|Tipo de información|Valor devuelto|  
|--------------|--------------------|  
|SQL_ACCESSIBLE_PROCEDURES|"Y"|  
|SQL_ACCESSIBLE_TABLES|"Y"|  
|SQL_ACTIVE_ENVIRONMENTS|0|  
|SQL_AGGREGATE_FUNCTIONS|Todo listo|  
|SQL_ALTER_DOMAIN|0|  
|SQL_ALTER_TABLE|0|  
|SQL_ASYNC_MODE|0|  
|SQL_BATCH_ROW_COUNT|0|  
|SQL_BATCH_SUPPORT|0|  
|SQL_BOOKMARK_PERSISTENCE|Varios valores|  
|SQL_CATALOG_LOCATION|SQL_QL_START|  
|SQL_CATALOG_NAME|"Y"|  
|SQL_CATALOG_NAME_SEPARATOR|"."|  
|SQL_CATALOG_TERM|"Base de datos"|  
|SQL_CATALOG_USAGE|Varios valores|  
|SQL_COLLATION_SEQ|""|  
|SQL_COLUMN_ALIAS|"Y"|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_CB_NON_NULL|  
|SQL_CONVERT_BIGINT|0|  
|SQL_CONVERT_BINARY|Varios valores|  
|SQL_CONVERT_BIT|0|  
|SQL_CONVERT_CHAR|Varios valores|  
|SQL_CONVERT_DATE|Varios valores|  
|SQL_CONVERT_DECIMAL|0|  
|SQL_CONVERT_DOUBLE|Varios valores|  
|SQL_CONVERT_FLOAT|Varios valores|  
|SQL_CONVERT_FUNCTIONS|SQL_FN_CVT_CONVERT|  
|SQL_CONVERT_INTEGER|Varios valores|  
|SQL_CONVERT_LONGVARBINARY|Varios valores|  
|SQL_CONVERT_LONGVARCHAR|Varios valores|  
|SQL_CONVERT_NUMERIC|Varios valores|  
|SQL_CONVERT_REAL|Varios valores|  
|SQL_CONVERT_SMALLINT|Varios valores|  
|SQL_CONVERT_TIME|Varios valores|  
|SQL_CONVERT_TIMESTAMP|Varios valores|  
|SQL_CONVERT_TINYINT|Varios valores|  
|SQL_CONVERT_VARBINARY|Varios valores|  
|SQL_CONVERT_VARCHAR|Varios valores|  
|SQL_CORRELATION_NAME|SQL_CN_ANY|  
|SQL_CREATE_ASSERTION|0|  
|SQL_CREATE_CHARACTER_SET|0|  
|SQL_CREATE_COLLATION|0|  
|SQL_CREATE_DOMAIN|0|  
|SQL_CREATE_SCHEMA|0|  
|SQL_CREATE_TABLE|SQL_CT_CREATE_TABLE|  
|SQL_CREATE_TRANSLATION|0|  
|SQL_CREATE_VIEW|SQL_CV_CREATE_VIEW|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_DATA_SOURCE_NAME|El DSN de Odbc.ini, o "" si se usa la palabra clave DRIVER en Odbc.ini|  
|SQL_DATA_SOURCE_READ_ONLY|"N"|  
|SQL_DATABASE_NAME|Nombre de archivo|  
|SQL_DATETIME_LITERALS|0|  
|SQL_DBMS_NAME|"ACCESO"|  
|SQL_DBMS_VER|Varios valores|  
|SQL_DDL_INDEX|Varios valores|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_TXN_READ_COMMITTED|  
|SQL_DESCRIBE_PARAMETER|0|  
|SQL_DRIVER_HDBC|Controlado por el Administrador de controladores.|  
|SQL_DRIVER_HENV|Controlado por el Administrador de controladores.|  
|SQL_DRIVER_HLIB|Controlado por el Administrador de controladores.|  
|SQL_DRIVER_HSTMT|Controlado por el Administrador de controladores.|  
|SQL_DRIVER_NAME|"OdbcJt32.dll"|  
|SQL_DRIVER_ODBC_VER|"3.51.0000"|  
|SQL_DRIVER_VER|"4.00.*nnnn*" ( *nnnn*  especifica la fecha de compilación)|  
|SQL_DROP_ASSERTION|0|  
|SQL_DROP_CHARACTER_SET|0|  
|SQL_DROP_COLLATION|0|  
|SQL_DROP_DOMAIN|0|  
|SQL_DROP_SCHEMA|0|  
|SQL_DROP_TABLE|SQL_DT_DROP_TABLE|  
|SQL_DROP_TRANSLATION|0|  
|SQL_DROP_VIEW|SQL_DV_DROP_VIEW|  
|SQL_EXPRESSIONS_IN_ORDERBY|"Y"|  
|SQL_FILE_USAGE|SQL_FILE_CATALOG|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT|  
|SQL_GETDATA_EXTENSIONS|Varios valores|  
|SQL_GROUP_BY|SQL_GB_GROUP_BY_CONTAINS_SELECT|  
|SQL_IDENTIFIER_CASE|SQL_IC_MIXED|  
|SQL_IDENTIFIER_QUOTE_CHAR|"'" (comilla inversa)|  
|SQL_KEYWORDS|Varios valores|  
|SQL_LIKE_ESCAPE_CLAUSE|"N"|  
|SQL_MAX_BINARY_LITERAL_LEN|255|  
|SQL_MAX_CATALOG_NAME_LEN|66|  
|SQL_MAX_CHAR_LITERAL_LEN|255|  
|SQL_MAX_COLUMN_NAME_LEN|64|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|10|  
|SQL_MAX_COLUMNS_IN_INDEX|32|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|10|  
|SQL_MAX_COLUMNS_IN_SELECT|255|  
|SQL_MAX_COLUMNS_IN_TABLE|255|  
|SQL_MAX_CONCURRENT_ACTIVITIES|0|  
|SQL_MAX_CURSOR_NAME_LEN|64|  
|SQL_MAX_DRIVER_CONNECTIONS|64|  
|SQL_MAX_INDEX_SIZE|255|  
|SQL_MAX_PROCEDURE_NAME_LEN|64|  
|SQL_MAX_ROW_SIZE|2096|  
|SQL_MAX_ROW_SIZE_INCLUDES_LONG|"N"|  
|SQL_MAX_SCHEMA_NAME_LEN|0|  
|SQL_MAX_STATEMENT_LEN|65000|  
|SQL_MAX_TABLE_NAME_LEN|64|  
|SQL_MAX_TABLES_IN_SELECT|16|  
|SQL_MAX_USER_NAME_LEN|0|  
|SQL_MULT_RESULT_SETS|"N"|  
|SQL_MULTIPLE_ACTIVE_TXN|"Y"|  
|SQL_NEED_LONG_DATA_LEN|"N"|  
|SQL_NON_NULLABLE_COLUMNS|SQL_NNC_NON_NULL|  
|SQL_NULL_COLLATION|SQL_NC_LOW|  
|SQL_NUMERIC_FUNCTIONS|Varios valores|  
|CONFORMIDAD DE SQL_ODBC_SAG_CLI_|SQL_OSCC_COMPLIANT|  
|SQL_ODBC_SQL_INTEGRITY|"N"|  
|SQL_ODBC_VER|Desde el Administrador de controladores|  
|SQL_OJ_CAPABILITIES|Varios valores|  
|SQL_ORDER_BY_COLUMNS_IN_SELECT|"N"|  
|SQL_OUTER_JOINS|"Y"|  
|SQL_PROCEDURE_TERM|"QUERY"|  
|SQL_PROCEDURES|"Y"|  
|SQL_QUOTED_IDENTIFIER_CASE|SQL_IC_MIXED|  
|SQL_ROW_UPDATES|"N"|  
|SQL_SCHEMA_TERM|""|  
|SQL_SCHEMA_USAGE|0|  
|SQL_SCROLL_OPTIONS|Varios valores|  
|SQL_SEARCH_PATTERN_ESCAPE|"\\"|  
|SQL_SERVER_NAME|"ACCESO"|  
|SQL_SPECIAL_CHARACTERS|"~`@#$%^&*_-+=\\}{"';:?/><,.!'[]&#124;"|  
|SQL_STRING_FUNCTIONS|Varios valores|  
|SQL_SUBQUERIES|Varios valores|  
|SQL_SYSTEM_FUNCTIONS|0|  
|SQL_TABLE_TERM|"TABLE"|  
|SQL_TIMEDATE_ADD_INTERVALS|0|  
|SQL_TIMEDATE_DIFF_INTERVALS|0|  
|SQL_TIMEDATE_FUNCTIONS|Varios valores|  
|SQL_TXN_CAPABLE|SQL_TC_ALL|  
|SQL_TXN_ISOLATION_OPTION|SQL_TXN_READ_COMMITTED|  
|SQL_UNION|Varios valores|  
|SQL_USER_NAME|"ADMIN"|

