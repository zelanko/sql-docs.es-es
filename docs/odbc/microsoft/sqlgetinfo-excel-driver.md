---
title: SQLGetInfo (controlador de Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Excel Driver
ms.assetid: fed4aea2-6d3d-4199-a5db-3d033eb63927
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba2e23bf4b3c464c5483897c0a9dd3e6c9dea626
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003280"
---
# <a name="sqlgetinfo-excel-driver"></a>SQLGetInfo (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** admite el tipo de información SQL_FILE_USAGE. El valor devuelto es un entero de 16 bits que indica cómo el controlador trata directamente los archivos de un origen de datos:  
  
-   SQL_FILE_NOT_SUPPORTED: el controlador no es un controlador de un solo nivel.  
  
-   SQL_FILE_TABLE: un controlador de un solo nivel trata los archivos de un origen de datos como tablas.  
  
-   SQL_FILE_QUALIFIER: un controlador de un solo nivel trata los archivos de un origen de datos como un calificador.  
  
 El controlador ODBC devuelve SQL_FILE_TABLE para Microsoft Exceldriver porque cada archivo es una tabla.  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|Versión|Formato de los números de versión|  
|----------|-------------|-------------------------------|  
|Microsoft Excel|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0/7.0|05.00.0000|  
||97/2000|08.00.0000|  
  
## <a name="sql_file_usage"></a>SQL_FILE_USAGE  
 SQL_FILE_TABLE (Excel 3.0/4.0)  
  
 SQL_FILE_CATALOG (Excel 5.0/7.0)  
  
## <a name="sql_max_char_literal_len"></a>SQL_MAX_CHAR_LITERAL_LEN  
 255 (Excel 3.0/4.0/5.0/7.0)  
  
 65535 (Excel 97)  
  
## <a name="sql_max_column_name_len"></a>SQL_MAX_COLUMN_NAME_LEN  
 30 (Excel 3.0/4.0)  
  
 64 (Excel 5.0/7.0/97)  
  
## <a name="sql_max_table_name_len"></a>SQL_MAX_TABLE_NAME_LEN  
 12 (Excel 3.0/4.0)  
  
 31 (Excel 5.0/7.0/97)  
  
## <a name="sql_catalog_name_separator"></a>SQL_CATALOG_NAME_SEPARATOR  
 "\\" (Excel 3.0/4.0)  
  
 "." (Excel 5.0/7.0/97)  
  
## <a name="sql_catalog_term"></a>SQL_CATALOG_TERM  
 "Directorio" (Excel 3.0/4.0)  
  
 "Libro" (Excel 5.0/7.0/97)  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
