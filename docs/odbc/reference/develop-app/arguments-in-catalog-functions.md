---
description: Argumentos de las funciones de catálogo
title: Argumentos en funciones de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef53514f41d28e93648970b03fa53927529d8344
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483138"
---
# <a name="arguments-in-catalog-functions"></a>Argumentos de las funciones de catálogo
Todas las funciones de catálogo aceptan argumentos con los que una aplicación puede restringir el ámbito de los datos devueltos. Por ejemplo, la primera y la segunda llamada a **SQLTables** en el código siguiente devuelven un conjunto de resultados que contiene información sobre todas las tablas, mientras que la tercera llamada devuelve información acerca de la tabla Orders:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Los argumentos de cadena de función de catálogo se dividen en cuatro tipos diferentes: argumento normal (OA), argumento de valor de patrón (PV), argumento de identificador (ID.) y argumento de lista de valores (VL). La mayoría de los argumentos de cadena pueden ser de uno de dos tipos diferentes, según el valor del atributo de instrucción SQL_ATTR_METADATA_ID. En la tabla siguiente se enumeran los argumentos de cada función de catálogo y se describe el tipo de argumento de una SQL_TRUE o SQL_FALSE valor de SQL_ATTR_METADATA_ID.  
  
|Función|Argumento|Escriba cuando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Escriba cuando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*Nombrecatálogo* *SchemaName* *TableName* *columnName*|OA OA OA VP|ID. ID ID ID|  
|**SQLColumns**|*Nombrecatálogo* *SchemaName* *TableName* *columnName*|OA PV PV PV|ID. ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA OA|ID. ID ID ID ID ID|  
|**SQLPrimaryKeys**|*Nombrecatálogo* *SchemaName* *TableName*|OA OA OA|IDENTIFICADOR DE IDENTIFICADOR ID.|  
|**SQLProcedureColumns**|*Nombrecatálogo* *SchemaName* *NombreProc* *columnName*|OA PV PV PV|ID. ID ID ID|  
|**SQLProcedures**|*Nombrecatálogo* *SchemaName* *NombreProc*|OA PV PV|IDENTIFICADOR DE IDENTIFICADOR ID.|  
|**SQLSpecialColumns**|*Nombrecatálogo* *SchemaName* *TableName*|OA OA OA|IDENTIFICADOR DE IDENTIFICADOR ID.|  
|**SQLStatistics**|*Nombrecatálogo* *SchemaName* *TableName*|OA OA OA|IDENTIFICADOR DE IDENTIFICADOR ID.|  
|**SQLTablePrivileges**|*Nombrecatálogo* *SchemaName* *TableName*|OA PV PV|IDENTIFICADOR DE IDENTIFICADOR ID.|  
|**SQLTables**|*Nombrecatálogo* *SchemaName* *TableName* *TableType*|PV PV PV VL|ID. DE ID. DE IDENTIFICADOR VL|  
  
 Esta sección contiene los temas siguientes.  
  
-   [Argumentos normales](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argumentos de valor de patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argumentos de identificador](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argumentos de la lista de valores](../../../odbc/reference/develop-app/value-list-arguments.md)
