---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5dd36e82b71ff862a543bfa38cda4b4a660738a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287751"
---
# <a name="arguments-in-catalog-functions"></a>Argumentos de las funciones de catálogo
Todas las funciones de catálogo aceptan argumentos con el que una aplicación puede restringir el ámbito de los datos devueltos. Por ejemplo, el primeros y segunda las llamadas a **SQLTables** en el código siguiente devuelve un conjunto que contiene información sobre todas las tablas, mientras que la tercera llamada devuelve información acerca de la tabla Orders de resultados:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Argumentos de cadena de función de catálogo se dividen en cuatro tipos diferentes: argumento normal (OA), el argumento de valor de patrón (PV), el argumento de identificador (ID) y argumento de valor de lista (VL). La mayoría de los argumentos de cadena pueden ser de uno de los dos tipos diferentes, dependiendo del valor del atributo de instrucción SQL_ATTR_METADATA_ID. En la tabla siguiente se enumera los argumentos para cada función de catálogo y describe el tipo del argumento para un valor de SQL_TRUE o SQL_FALSE de SQL_ATTR_METADATA_ID.  
  
|Función|Argumento|Cuando escriba SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Cuando escriba SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID. = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID. ID. DE IDENTIFICADOR DE ID.|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|ID. ID. DE IDENTIFICADOR DE ID.|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|ID. ID. ID. ID. ID. ID.|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID. DEL IDENTIFICADOR DE ID.|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID. ID. DE IDENTIFICADOR DE ID.|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID. DEL IDENTIFICADOR DE ID.|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID. DEL IDENTIFICADOR DE ID.|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID. DEL IDENTIFICADOR DE ID.|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID. DEL IDENTIFICADOR DE ID.|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV VL|LICENCIAS POR VOLUMEN DE ID. ID. ID.|  
  
 Esta sección contiene los temas siguientes.  
  
-   [Argumentos normales](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argumentos de valor de patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argumentos de identificador](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argumentos de la lista de valores](../../../odbc/reference/develop-app/value-list-arguments.md)
