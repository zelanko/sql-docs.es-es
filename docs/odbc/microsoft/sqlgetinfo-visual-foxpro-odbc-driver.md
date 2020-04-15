---
title: SQLGetInfo (Controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d4b976083b46bf632c4890c7fce3b0f13a9a761
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295195"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: Nivel 1  
  
 Devuelve información general sobre el controlador ODBC de Visual FoxPro y el origen de datos asociado a un identificador de conexión, *hdbc*. En la lista siguiente se muestra el valor devuelto por el controlador ODBC de Visual FoxPro para cada *fInfoType* argumento y comentarios con respecto a los valores devueltos.  
  
 Para obtener más información, vea [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) en la *referencia del programador ODBC*.  
  
## <a name="a"></a>Un  
 SQL_ACCESSIBLE_PROCEDURES devuelve 'N'.  
  
 SQL_ACCESSIBLE_TABLES devuelve 'Y'.  
  
 SQL_ACTIVE_CONNECTIONS devuelve 0.  
  
 SQL_ACTIVE_STATEMENTS devuelve 0.  
  
 SQL_ALTER_TABLE devuelve SQL_AT_ADD_COLUMN o SQL_AT_DROP_COLUMN.  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE devuelve SQL_BP_SCROLL.  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS devuelve 'Y'.  
  
 SQL_CONCAT_NULL_BEHAVIOR devuelve SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINT devuelve 0. El controlador ODBC de Visual FoxPro no admite *BigInt*.  
  
 SQL_CONVERT_BINARY devuelve 0.  
  
 SQL_CONVERT_BIT devuelve 0.  
  
 SQL_CONVERT_CHAR devuelve 0.  
  
 SQL_CONVERT_DATE devuelve 0.  
  
 SQL_CONVERT_DECIMAL devuelve 0.  
  
 SQL_CONVERT_DOUBLE devuelve 0.  
  
 SQL_CONVERT_FLOAT devuelve 0.  
  
 SQL_CONVERT_INTEGER devuelve 0.  
  
 SQL_CONVERT_LONGVARBINARY devuelve 0.  
  
 SQL_CONVERT_LONGVARCHAR devuelve 0.  
  
 SQL_CONVERT_NUMERIC devuelve 0.  
  
 SQL_CONVERT_REAL devuelve 0.  
  
 SQL_CONVERT_SMALLINT devuelve 0.  
  
 SQL_CONVERT_TIME devuelve 0.  
  
 SQL_CONVERT_TIMESTAMP devuelve 0.  
  
 SQL_CONVERT_TINYINT devuelve 0.  
  
 SQL_CONVERT_VARBINARY devuelve 0.  
  
 SQL_CONVERT_VARCHAR devuelve 0.  
  
 SQL_CONVERT_FUNCTIONS devuelve 0.  
  
 SQL_CORRELATION_NAME SQL_CN_ANY de devoluciones.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR devuelve SQL_CB_PRESERVE.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR devuelve SQL_CB_PRESERVE.  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME devuelve el valor pasado como DSN a [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)o [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md); devuelve una cadena vacía si no se especifica ningún DSN.  
  
 SQL_DATA_SOURCE_READ_ONLY devuelve 'N'.  
  
 SQL_DATABASE_NAME devuelve una ruta de acceso UNC completa a la base de datos actual si el origen de datos es una base de [datos.](../../odbc/microsoft/visual-foxpro-terminology.md) Si el origen de datos se conecta a un directorio de [tablas,](../../odbc/microsoft/visual-foxpro-terminology.md)la función devuelve la ruta de acceso al directorio.  
  
 SQL_DBMS_NAME devuelve "Visual FoxPro".  
  
 SQL_DBMS_VER devuelve "03.00.0000".  
  
 SQL_DEFAULT_TXN_ISOLATION devuelve SQL_TXN_READ_COMMITTED. Las lecturas sucias no son posibles, pero las lecturas y fantasmas no repetibles son posibles.  
  
 SQL_DRIVER_HDBC implementa el Administrador de controladores.  
  
 SQL_DRIVER_HENV implementa el Administrador de controladores.  
  
 SQL_DRIVER_HLIB implementa el Administrador de controladores.  
  
 SQL_DRIVER_HSTMT implementa el Administrador de controladores.  
  
 SQL_DRIVER_NAME devuelve "vfpodbc.dll".  
  
 SQL_DRIVER_ODBC_VER devuelve "02.50" (SQL_SPEC_MAJOR, SQL_SPEC_MINOR).  
  
 SQL_DRIVER_VER devuelve "01.00.0000".  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY devuelve 'N'.  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION devoluciones:  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK.  
  
 SQL_FILE_USAGE devuelve SQL_FILE_QUALIFIER para los orígenes de datos de base de datos (archivo .dbc) como para la tabla gratuita (archivo .dbf).  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS devoluciones:  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY devuelve SQL_GB_NO_RELATION.  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE devuelve SQL_IC_MIXED.  
  
 SQL_IDENTIFIER_QUOTE_CHAR devuelve '.  
  
## <a name="k"></a>K  
 SQL_KEYWORDS devuelve "".  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE devuelve 'N'.  
  
 SQL_LOCK_TYPES devuelve SQL_LCK_NO_CHANGE.  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN devuelve 0.  
  
 SQL_MAX_CHAR_LITERAL_LEN devuelve 254.  
  
 SQL_MAX_COLUMN_NAME_LEN devuelve 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY devuelve 16.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY devuelve 16.  
  
 SQL_MAX_COLUMNS_IN_INDEX devuelve 0.  
  
 SQL_MAX_COLUMNS_IN_SELECT devuelve 254.  
  
 SQL_MAX_COLUMNS_IN_TABLE devuelve 254.  
  
 SQL_MAX_CURSOR_NAME_LEN devuelve 254.  
  
 SQL_MAX_INDEX_SIZE devuelve 0.  
  
 SQL_MAX_OWNER_NAME_LEN devuelve 0.  
  
 SQL_MAX_PROCEDURE_NAME_LEN devuelve 0. El controlador ODBC de Visual FoxPro no permite el acceso directo a los procedimientos almacenados de Visual FoxPro.  
  
 SQL_MAX_QUALIFIER_NAME_LEN devuelve la longitud máxima de la ruta del sistema operativo.  
  
 SQL_MAX_ROW_SIZE devuelve 254x2.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG devuelve 'N'.  
  
 SQL_MAX_STATEMENT_LEN devuelve 8192.  
  
 SQL_MAX_TABLE_NAME_LEN devuelve 128.  
  
 SQL_MAX_TABLES_IN_SELECT devuelve 16.  
  
 SQL_MAX_USER_NAME_LEN devuelve 0.  
  
 SQL_MULT_RESULT_SETS devuelve 'Y'.  
  
 SQL_MULTIPLE_ACTIVE_TXN devuelve 'Y'. Varias conexiones pueden tener varias transacciones abiertas a la vez.  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN devuelve 'N'.  
  
 SQL_NON_NULLABLE_COLUMNS devuelve SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION devuelve SQL_NC_LOW.  
  
 SQL_NUMERIC_FUNCTIONS devuelve todas las funciones excepto SQL_FN_NUM_POWER, que no es compatible con el controlador ODBC de Visual FoxPro. Se admiten las siguientes funciones:  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE devuelve SQL_OAC_LEVEL1.  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE devuelve SQL_OSCC_COMPLIANT.  
  
 SQL_ODBC_SQL_CONFORMANCE devuelve SQL_OSC_MINIMUM. Se admite la sintaxis SQL mínima.  
  
 SQL_ODBC_SQL_OPT_IEF devuelve "N".  
  
 SQL_ODBC_VER implementa el Administrador de controladores.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT devuelve "N".  
  
 SQL_OUTER_JOINS devuelve "N".  
  
 SQL_OWNER_TERM devuelve "". El controlador ODBC de Visual FoxPro no admite propietarios para sus objetos.  
  
 SQL_OWNER_USAGE devuelve 0. El controlador ODBC de Visual FoxPro no admite propietarios para sus objetos.  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS devuelve SQL_POS_POSITION.  
  
 SQL_POSITIONED_STATEMENTS devuelve 0.  
  
 SQL_PROCEDURE_TERM devuelve "".  
  
 SQL_PROCEDURES devuelve 'N'.  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION devuelve SQL_QL_START.  
  
 SQL_QUALIFIER_NAME_SEPARATOR devuelve '!'\\o ''. El separador entre la base de datos y la tabla\\es '!' para los orígenes de datos conectados a bases de [datos](../../odbc/microsoft/visual-foxpro-terminology.md)y ' ' para los orígenes de datos que son directorios de [tablas libres.](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
 SQL_QUALIFIER_TERM devuelve "base de datos" o "directorio". El calificador es "base de datos" para orígenes de datos conectados a bases de [datos](../../odbc/microsoft/visual-foxpro-terminology.md)y "directorio" para orígenes de datos que son directorios de [tablas libres.](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
 SQL_QUALIFIER_USAGE no admite SQL_QU_PRIVILEGE_DEFINITION; devuelve SQL_QU_DML_STATEMENT o SQL_QU_TABLE_DEFINITION.  
  
 SQL_QUOTED_IDENTIFIER_CASE SQL_IC_MIXED de devoluciones.  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES devuelve "N". El controlador ODBC de Visual FoxPro solo admite cursores estáticos y directos.  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY devuelve SQL_SCCO_READ_ONLY.  
  
 SQL_SCROLL_OPTIONS devuelve SQL_SO_STATIC o SQL_SO_READONLY.  
  
 SQL_SEARCH_PATTERN_ESCAPE devuelve\\" ".  
  
 SQL_SERVER_NAME devuelve "".  
  
 SQL_SPECIAL_CHARACTERS devuelve el valor de "a$%".  
  
 SQL_STATIC_SENSITIVITY devuelve 0. El controlador ODBC de Visual FoxPro no admite actualizaciones posicionales.  
  
 SQL_STRING_FUNCTIONS no admite SQL_FN_STR_INSERT, SQL_FN_STR_LOCATE, SQL_FN_STR_LOCATE_2 ni SQL_FN_STR_SOUNDEX.  
  
 Se devuelve lo siguiente:  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE.  
  
 SQL_SUBQUERIES devoluciones:  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED.  
  
 SQL_SYSTEM_FUNCTIONS devoluciones:  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 pero no:  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM devuelve "tabla".  
  
 SQL_TIMEDATE_ADD_INTERVALS devoluciones:  
  
-   SQL_FN_TSI_ SEGUNDO  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 pero no:  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS devoluciones:  
  
-   SQL_FN_TSI_ SEGUNDO  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS no admite SQL_FN_TD_QUARTER, SQL_FN_TD_TIMESTAMPADD, SQL_FN_TD_DAYOFYEAR ni SQL_FN_TD_WEEK.  
  
 Se devuelve lo siguiente:  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR .  
  
 SQL_TXN_CAPABLE devuelve SQL_TC_DML.  
  
 SQL_TXN_ISOLATION_OPTION SQL_TXN_READ_COMMITTED de devoluciones.  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION devuelve SQL_U_UNION o SQL_U_UNION_ALL.  
  
 SQL_USER_NAME \<devuelve> en blanco.
