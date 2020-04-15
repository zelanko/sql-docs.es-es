---
title: Archivos de encabezado ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62364d828e7b1f1ed8c70cae7ae1fc7dc3bc33fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300195"
---
# <a name="header-files"></a>Archivos de encabezado
El archivo de encabezado Sql.h contiene prototipos para las funciones y características en el nivel de conformidad de la interfaz ODBC principal. El archivo de encabezado Sqlext.h contiene prototipos para las funciones y características de los niveles de conformidad de la API de nivel 1 y nivel 2. El archivo de encabezado Sqltypes.h contiene definiciones de tipo e indicadores para los tipos de datos SQL.  
  
 Todos los archivos de encabezado contienen un **#define**, ODBCVER, que una aplicación o controlador se puede establecer para compilarse para diferentes versiones de ODBC.  
  
 Para alinearse con la CLI de ISO y la CLI de grupo abierto, los archivos de encabezado contienen alias para los tipos de información utilizados en las llamadas a **SQLGetInfo**. En la tabla siguiente, la columna "Nombre ODBC" indica el nombre ODBC para el tipo de información en Referencia de [la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md). La columna "Alias en el archivo de encabezado" indica el nombre que se utiliza en la CLI ISO y la CLI del grupo abierto. El valor numérico real de estos nombres de manifiesto es el mismo tanto en ODBC como en las CLI estándar. Estos alias permiten que una aplicación o controlador compatible con estándares se compile con los archivos de encabezado ODBC *3.x.*  
  
 Estos alias incluyen expansiones de abreviaturas en los nombres ODBC para que los nombres sean más comprensibles. "MAX" se expande a "MAXIMUM", "LEN" a "LENGTH", "MULT" a "MULTIPLE", "OJ" a "OUTER_JOIN" y "TXN" a "TRANSACTION."  
  
|Nombre ODBC|Alias en el archivo de encabezado|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|
