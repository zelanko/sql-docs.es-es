---
title: "Argumentos de las funciones de catálogo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f8939b2e1ae81c3eb171e78753e7fc3b6cc17ae
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="arguments-in-catalog-functions"></a>Argumentos de las funciones de catálogo
Todas las funciones de catálogo aceptan argumentos con el que una aplicación puede restringir el ámbito de los datos devueltos. Por ejemplo, la primeros y segunda llamadas a **SQLTables** en el código siguiente devuelve un conjunto que contiene información sobre todas las tablas, mientras que la tercera llamada devuelve información acerca de la tabla Orders de resultados:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Argumentos de cadena de función de catálogo se dividen en cuatro tipos diferentes: argumento normal (OA), el argumento de valor de patrón (PV), argumento de identificador (Id.) y argumento de la lista de valor (licencias por volumen). La mayoría de los argumentos de cadena pueden ser de uno de dos tipos diferentes, dependiendo del valor del atributo de instrucción SQL_ATTR_METADATA_ID. La tabla siguiente enumera los argumentos para cada función de catálogo y describe el tipo del argumento para un valor SQL_TRUE o SQL_FALSE de SQL_ATTR_METADATA_ID.  
  
|Función|Argumento|Cuando escriba SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID. = SQL_FALSE|Cuando escriba SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID. = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID. DE IDENTIFICADOR DE ID. DE ID.|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|ID. DE IDENTIFICADOR DE ID. DE ID.|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName*  *FKTableName*|OA OA OA OA OA OA|ID. DE IDENTIFICADOR DE ID. ID. ID. ID.|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID. DE IDENTIFICADOR DE ID.|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID. DE IDENTIFICADOR DE ID. DE ID.|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID. DE IDENTIFICADOR DE ID.|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID. DE IDENTIFICADOR DE ID.|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID. DE IDENTIFICADOR DE ID.|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID. DE IDENTIFICADOR DE ID.|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV LICENCIAS POR VOLUMEN|LICENCIAS DE ID. DE IDENTIFICADOR DE ID.|  
  
 Esta sección contiene los temas siguientes.  
  
-   [Argumentos normales](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argumentos de valor de patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argumentos de identificador](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argumentos de la lista de valores](../../../odbc/reference/develop-app/value-list-arguments.md)

