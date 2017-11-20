---
title: SQLGetInfo (controlador de acceso) | Documentos de Microsoft
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
- SQLGetInfo function [ODBC], Access Driver
- Access driver [ODBC], SQLGetInfo
ms.assetid: c226aba7-a2f4-4b32-b640-92654b40e5a7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 86fd194b5bdde4fad1daca185c18c9ed9fd742b5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-access-driver"></a>SQLGetInfo (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** es compatible con el tipo de información de SQL_FILE_USAGE. El valor devuelto es un entero de 16 bits con signo que indica cómo el controlador trata directamente los archivos en un origen de datos:  
  
-   SQL_FILE_NOT_SUPPORTED: El controlador no es un controlador de nivel único.  
  
-   SQL_FILE_TABLE: Un controlador de nivel único trata los archivos en un origen de datos como tablas.  
  
-   SQL_FILE_QUALIFIER: Un controlador de nivel único trata los archivos en un origen de datos como un calificador.  
  
 El controlador ODBC devuelve SQL_FILE_QUALIFIER porque cada archivo es una base de datos completa.  
  
## <a name="sqlbookmarkpersistence"></a>SQL_BOOKMARK_PERSISTENCE  
 SQL_BP_SCROLL &#124;  SQL_BP_UPDATE [1]  
  
 [1] marcadores se conservan después de una instrucción commit pero no se conservan después de una operación de deshacer.  
  
## <a name="sqlconvertbinary"></a>SQL_CONVERT_BINARY  
 SQL_CVT_DOUBLE &#124;  SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertchar"></a>SQL_CONVERT_CHAR  
 SQL_CVT_DOUBLE &#124;  SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertdate"></a>SQL_CONVERT_DATE  
 SQL_CVT_DOUBLE &#124;  SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertdouble"></a>SQL_CONVERT_DOUBLE  
 SQL_CVT_DOUBLE &#124;  SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertfloat"></a>SQL_CONVERT_FLOAT  
 SQL_CVT_DOUBLE &#124;  SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertinteger"></a>SQL_CONVERT_INTEGER  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertlongvarbinary"></a>SQL_CONVERT_LONGVARBINARY  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertlongvarchar"></a>SQL_CONVERT_LONGVARCHAR  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertnumeric"></a>SQL_CONVERT_NUMERIC  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertreal"></a>SQL_CONVERT_REAL  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertsmallint"></a>SQL_CONVERT_SMALLINT  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconverttime"></a>SQL_CONVERT_TIME  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconverttimestamp"></a>SQL_CONVERT_TIMESTAMP  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconverttinyint"></a>SQL_CONVERT_TINYINT  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertvarbinary"></a>SQL_CONVERT_VARBINARY  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlconvertvarchar"></a>SQL_CONVERT_VARCHAR  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124;  SQL_CVT_INTEGER &#124;  SQL_CVT_NUMERIC &#124;  SQL_CVT_REAL &#124;  SQL_CVT_SMALLINT &#124;  SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sqlunion"></a>SQL_UNION  
 SQL_U_UNION_ALL &#124; SQL_U_UNION  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|Versión|Formato de números de versión|  
|----------|-------------|-------------------------------|  
|Microsoft Access|2,0|02.00.0000|  
||3.0|03.00.0000|  
||3.5|03.50.0000|  
||4.0|04.00.0000|  
  
> [!NOTE]  
>  No se admiten las versiones 1.0 y 1.1. Además, no hay ninguna diferencia en el formato de datos en las versiones de Microsoft Access 3.0, 7.0 y 97.  
  
## <a name="sqlddlindex"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sqlgetdataextensions"></a>SQL_GETDATA_EXTENSIONS  
 SQL_GD_ANY_ORDER &#124; SQL_GD_ANY_COLUMN &#124; SQL_GD_BLOCK &#124; SQL_GD_BOUND  
  
## <a name="sqlkeywords"></a>SQL_KEYWORDS  
 ALFANUMÉRICO  
  
 INCREMENTO AUTOMÁTICO  
  
 BINARY  
  
 BOOLEAN  
  
 BYTE  
  
 CONTADOR  
  
 Moneda  
  
 DATABASE  
  
 DATABASENAME  
  
 DATETIME  
  
 NO PERMITIR  
  
 DISTINCTROW  
  
 DOUBLEFLOAT  
  
 FLOAT4  
  
 FLOAT8  
  
 GENERAL  
  
 IEEEDOUBLE  
  
 IEEESINGLE  
  
 IGNORE  
  
 IMAGE  
  
 INTEGER1  
  
 INTEGER2  
  
 INTEGER4  
  
 LÓGICO  
  
 VALOR_LÓGICO1  
  
 LONG  
  
 LONGBINARY  
  
 LONGCHAR  
  
 LONGTEXT  
  
 MEMORANDO  
  
 MONEY  
  
 TENGA EN CUENTA  
  
 NUMBER  
  
 OLEOBJECT  
  
 OWNERACCESS  
  
 PARAMETERS  
  
 PERCENT  
  
 PIVOT  
  
 CORTO  
  
 ÚNICO  
  
 SINGLEFLOAT  
  
 STDEV  
  
 STDEVP  
  
 CADENA  
  
 TABLEID  
  
 TEXT  
  
 ARRIBA  
  
 TRANSFORMAR  
  
 UNSIGNEDBYTE  
  
 VAR  
  
 VARBINARY  
  
 VARP  
  
 YESNO  
  
## <a name="sqlnumericfunctions"></a>SQL_NUMERIC_FUNCTIONS  
 SQL_FN_NUM_ABS &#124; SQL_FN_NUM_ATAN &#124; SQL_FN_NUM_CEILING &#124; SQL_FN_NUM_COS &#124; SQL_FN_NUM_EXP &#124; SQL_FN_NUM_FLOOR &#124; SQL_FN_NUM_LOG &#124; SQL_FN_NUM_MOD &#124; SQL_FN_NUM_POWER &#124; SQL_FN_NUM_RAND &#124; SQL_FN_NUM_SIGN &#124; SQL_FN_NUM_SIN &#124; SQL_FN_NUM_SQRT &#124; SQL_FN_NUM_TAN  
  
## <a name="sqlojcapabilities"></a>SQL_OJ_CAPABILITIES  
 SQL_OJ_LEFT SQL_OJ_RIGHT SQL_OJ_NOT_ORDERED SQL_OJ_INNER SQL_OJ_ALL_COMPARISON_OPS  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION &#124; SQL_QU_INDEX_DEFINITION &#124; SQL_QU_PROCEDURE_INVOCATION  
  
## <a name="sqlscrolloptions"></a>SQL_SCROLL_OPTIONS  
 SQL_SO_FORWARD_ONLY &#124; SQL_SO_STATIC &#124; SQL_SO_KEYSET_DRIVEN  
  
## <a name="sqlstringfunctions"></a>SQL_STRING_FUNCTIONS  
 SQL_FN_STR_ASCII &#124; SQL_FN_STR_CHAR &#124; SQL_FN_STR_CONCAT &#124;  SQL_FN_STR_LCASE &#124;  SQL_FN_STR_LEFT &#124;  SQL_FN_STR_LENGTH &#124;  SQL_FN_STR_LOCATE &#124; SQL_FN_STR_LOCATE_2 SQL_FN_STR_LTRIM &#124;  SQL_FN_STR_RIGHT &#124;  SQL_FN_STR_RTRIM &#124;  SQL_FN_STR_SPACE &#124; SQL_FN_STR_SUBSTRING &#124;  SQL_FN_STR_UCASE  
  
## <a name="sqlsubqueries"></a>SQL_SUBQUERIES  
 SQL_SQ_COMPARISON &#124; SQL_SQ_EXISTS &#124; SQL_SQ_IN &#124; SQL_SQ_QUANTIFIED &#124; SQL_SQ_CORRELATED_SUBQUERIES  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124;  SQL_FN_TD_CURTIME &#124;  SQL_FN_TD_DAYOFMONTH &#124;  SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124;  SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124;  SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR

