---
title: Archivos de encabezado | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e6d0806a7c3eabd1c6f4cd1836308eba99a6d5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724370"
---
# <a name="header-files"></a>Archivos de encabezado
El archivo de encabezado Sql.h contiene prototipos para las funciones y características en el nivel de conformidad de interfaz de ODBC Core. El archivo de encabezado Sqlext.h contiene prototipos para las funciones y características en el nivel 1 y niveles de compatibilidad de API de nivel 2. El archivo de encabezado Sqltypes.h contiene las definiciones de tipo e indicadores para los tipos de datos SQL.  
  
 Los archivos de encabezado que contienen un **#define**, ODBCVER, que puede establecer una aplicación o un controlador para compilarse para diferentes versiones de ODBC.  
  
 Para alinearse con la CLI de ISO y abra CLI de grupo, los archivos de encabezado contienen un alias para los tipos de información que se usa en llamadas a **SQLGetInfo**. En la tabla siguiente, la columna "Nombre de ODBC" indica el nombre ODBC para el tipo de información en [referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md). La columna "Alias en el archivo de encabezado" indica el nombre que se usa en la CLI de ISO y la CLI de grupo abierto. El valor numérico real de estos nombres de manifiesto es el mismo en ODBC y la CLI estándar. Estos alias habilitar una aplicación compatible con los estándares o un controlador para compilar con ODBC 3 *.x* archivos de encabezado.  
  
 Estos alias incluyen las expansiones de abreviaturas en los nombres de ODBC para que los nombres sean más comprensibles. "MAX" se expande a "Máximo", "Largo" a "LENGTH", "MULT" a "Varios", "DO" a "OUTER_JOIN" y "Transacción" a "Transacción".  
  
|Nombre de ODBC|Alias en el archivo de encabezado|  
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
