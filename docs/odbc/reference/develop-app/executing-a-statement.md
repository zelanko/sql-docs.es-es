---
title: Ejecutar una instrucción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5660cfe2f264e0971d30cd2eaf1aadf68581321e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032812"
---
# <a name="executing-a-statement"></a>Ejecutar una instrucción
Hay cuatro maneras de ejecutar una instrucción, dependiendo de cuando se compilan (preparado) por el motor de base de datos y que los define:  
  
-   **Ejecución directa** la aplicación define la instrucción SQL. Se prepara y ejecuta en tiempo de ejecución en un solo paso.  
  
-   **La ejecución preparada** la aplicación define la instrucción SQL. Se prepara y ejecuta en tiempo de ejecución en pasos independientes. La instrucción se puede preparar una vez y ejecuta varias veces.  
  
-   **Procedimientos** la aplicación puede definir y compilar uno o más instrucciones SQL en el desarrollo de tiempo y almacenan estas instrucciones en el origen de datos como un procedimiento. El procedimiento se ejecuta una o varias veces en tiempo de ejecución. La aplicación puede enumerar los procedimientos almacenados disponibles mediante las funciones de catálogo.  
  
-   **Funciones de catálogo** el escritor de controlador crea una función que devuelve un conjunto de resultados predefinidos. Normalmente, esta función envía una instrucción SQL predefinida o llama a un procedimiento creado para este propósito. La función se ejecuta una o varias veces en tiempo de ejecución.  
  
 Una instrucción determinada (como identificado por su identificador de instrucción) se puede ejecutar cualquier número de veces. Se puede ejecutar la instrucción con una variedad de diferentes instrucciones SQL o se puede ejecutar varias veces con la misma instrucción SQL. Por ejemplo, el código siguiente usa el mismo identificador de instrucción (*hstmt1*) para recuperar y mostrar las tablas en la base de datos de ventas. A continuación, vuelve a utilizar este identificador para recuperar las columnas de una tabla seleccionada por el usuario.  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 Y el código siguiente muestra cómo se usa un identificador único para ejecutar repetidamente la misma instrucción para eliminar filas de una tabla.  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 Para muchos de los controladores, las instrucciones de asignación es una tarea costosa, por lo que reutilizar la misma instrucción de esta manera es normalmente más eficaz que liberar instrucciones existentes y asignar otros nuevos. Las aplicaciones que crean conjuntos de resultados en una instrucción deben tener cuidadas cerrar el cursor sobre el conjunto de resultados antes deteniéndose la instrucción; Para obtener más información, consulte [cierre el Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 Volver a usar las instrucciones también se obliga a la aplicación para evitar una limitación en algunos controladores del número de instrucciones que pueden estar activas al mismo tiempo. La definición exacta de "activo" es específico del controlador, pero a menudo hace referencia a cualquier instrucción que se ha preparado o ejecuta y aún tiene resultados disponibles. Por ejemplo, después de un **insertar** se ha preparado la instrucción, por lo general se considera activo; después de un **seleccione** se ha ejecutado la instrucción y el cursor está abierto todavía, generalmente se considera a estar activos; Después de un **CREATE TABLE** se ha ejecutado la instrucción, por lo general no se considera activo.  
  
 Una aplicación determina cuántas instrucciones pueden estar activas en una sola conexión a la vez mediante una llamada a **SQLGetInfo** con la opción SQL_MAX_CONCURRENT_ACTIVITIES. Una aplicación puede usar instrucciones más activas que este límite al abrir varias conexiones con el origen de datos Dado que las conexiones pueden ser costosas, sin embargo, se debe considerar el efecto en el rendimiento.  
  
 Las aplicaciones pueden limitar la cantidad de tiempo asignado para que una instrucción que se ejecutará con el atributo de instrucción SQL_ATTR_QUERY_TIMEOUT. Si el período de tiempo de espera expira antes de que el origen de datos devuelve el conjunto de resultados, la función que se ejecuta la instrucción SQL devuelve SQLSTATE HYT00 (tiempo de espera agotado). De forma predeterminada, no hay ningún tiempo de espera.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Ejecución directa](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Procedimientos](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Lotes de instrucciones SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Ejecutar funciones de catálogo](../../../odbc/reference/develop-app/executing-catalog-functions.md)
