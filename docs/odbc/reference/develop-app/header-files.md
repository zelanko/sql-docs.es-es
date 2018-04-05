---
title: Archivos de encabezado | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 197c7ef28124fb1b1c52facbec541913330c69c5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="header-files"></a>Archivos de encabezado
El archivo de encabezado Sql.h contiene prototipos para las funciones y características en el nivel de conformidad de interfaz de ODBC básica. El archivo de encabezado Sqlext.h contiene prototipos para las funciones y características en el nivel 1 y niveles de compatibilidad de API de nivel 2. El archivo de encabezado Sqltypes.h contiene las definiciones de tipo e indicadores para los tipos de datos SQL.  
  
 Los archivos de encabezado contienen un **#define**, ODBCVER, que puede establecer una aplicación o un controlador de compilación para las diferentes versiones de ODBC.  
  
 Para alinear con el ISO CLI y la CLI de grupo abierto, los archivos de encabezado contienen alias para los tipos de información que se utilizan en las llamadas a **SQLGetInfo**. En la tabla siguiente, la columna "Nombre ODBC" indica el nombre ODBC para el tipo de información en [referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md). La columna "Alias en el archivo de encabezado" indica el nombre que se utiliza en ISO CLI y la CLI de grupo abierto. El valor numérico real de estos nombres de manifiesto es el mismo en ODBC y la CLI estándares. Estos alias permiten que una aplicación compatible con los estándares o el controlador para compilar con ODBC 3*.x* archivos de encabezado.  
  
 Estos alias incluyen expansiones de abreviaturas de los nombres de ODBC para que los nombres sean más comprensibles. "Máximo" se expande hasta "Máximo", "Longitud" a "Longitud", "MULT" a "Varios", "DO" a "OUTER_JOIN" y "TXN" a "Transacción".  
  
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
