---
title: Ejecución de una Declaración ( Executing a Statement) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3ce09809c896a4d1d9333da00367f972655f96b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305746"
---
# <a name="executing-a-statement"></a>Ejecutar una instrucción
Hay cuatro maneras de ejecutar una instrucción, dependiendo de cuándo se compilan (preparan) por el motor de base de datos y quién las define:  
  
-   **Ejecución directa** La aplicación define la instrucción SQL. Se prepara y ejecuta en tiempo de ejecución en un solo paso.  
  
-   **Ejecución preparada** La aplicación define la instrucción SQL. Se prepara y ejecuta en tiempo de ejecución en pasos independientes. La instrucción se puede preparar una vez y ejecutar varias veces.  
  
-   **Procedimientos** La aplicación puede definir y compilar una o varias instrucciones SQL en tiempo de desarrollo y almacenar estas instrucciones en el origen de datos como un procedimiento. El procedimiento se ejecuta una o más veces en tiempo de ejecución. La aplicación puede enumerar los procedimientos almacenados disponibles mediante funciones de catálogo.  
  
-   **Funciones de catálogo** El escritor de controladores crea una función que devuelve un conjunto de resultados predefinido. Normalmente, esta función envía una instrucción SQL predefinida o llama a un procedimiento creado para este propósito. La función se ejecuta una o más veces en tiempo de ejecución.  
  
 Una instrucción determinada (como se identifica por su identificador de instrucción) se puede ejecutar cualquier número de veces. La instrucción se puede ejecutar con una variedad de instrucciones SQL diferentes, o se puede ejecutar repetidamente con la misma instrucción SQL. Por ejemplo, el código siguiente utiliza el mismo identificador de instrucción (*hstmt1*) para recuperar y mostrar las tablas en la base de datos Sales. A continuación, reutiliza este identificador para recuperar las columnas de una tabla seleccionada por el usuario.  
  
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
  
 Y el código siguiente muestra cómo se usa un único identificador para ejecutar repetidamente la misma instrucción para eliminar filas de una tabla.  
  
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
  
 Para muchos controladores, asignar instrucciones es una tarea costosa, por lo que reutilizar la misma instrucción de esta manera suele ser más eficaz que liberar instrucciones existentes y asignar otras nuevas. Las aplicaciones que crean conjuntos de resultados en una instrucción deben tener cuidado de cerrar el cursor sobre el conjunto de resultados antes de volver a ejecutar la instrucción; Para obtener más información, consulte [Cierre del cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 Reutilizar instrucciones también obliga a la aplicación a evitar una limitación en algunos controladores del número de instrucciones que pueden estar activas a la vez. La definición exacta de "activo" es específica del controlador, pero a menudo se refiere a cualquier instrucción que se haya preparado o ejecutado y que todavía tenga resultados disponibles. Por ejemplo, después de que se ha preparado una instrucción **INSERT,** generalmente se considera activa; después de que se ha ejecutado una instrucción **SELECT** y el cursor sigue abierto, generalmente se considera que está activo; después de ejecutar una instrucción **CREATE TABLE,** generalmente no se considera activa.  
  
 Una aplicación determina cuántas instrucciones pueden estar activas en una sola conexión a la vez llamando a **SQLGetInfo** con la opción SQL_MAX_CONCURRENT_ACTIVITIES. Una aplicación puede usar instrucciones más activas que este límite abriendo varias conexiones al origen de datos; debido a que las conexiones pueden ser costosas, sin embargo, se debe considerar el efecto en el rendimiento.  
  
 Las aplicaciones pueden limitar la cantidad de tiempo asignado para que una instrucción se ejecute con el atributo de instrucción SQL_ATTR_QUERY_TIMEOUT. Si el período de tiempo de espera expira antes de que el origen de datos devuelva el conjunto de resultados, la función que ejecuta la instrucción SQL devuelve SQLSTATE HYT00 (tiempo de espera caducado). No hay un tiempo de espera predeterminado.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Ejecución directa](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Procedimientos](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Lotes de instrucciones SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Ejecutar funciones de catálogo](../../../odbc/reference/develop-app/executing-catalog-functions.md)
