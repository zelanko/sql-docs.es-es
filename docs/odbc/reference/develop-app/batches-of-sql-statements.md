---
title: Lotes de instrucciones SQL ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d68ea1c13655ca7c57ba076823f461a4b2e22055
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283515"
---
# <a name="batches-of-sql-statements"></a>Lotes de instrucciones SQL
Un lote de instrucciones SQL es un grupo de dos o más instrucciones SQL o una sola instrucción SQL que tiene el mismo efecto que un grupo de dos o más instrucciones SQL. En algunas implementaciones, toda la instrucción por lotes se ejecuta antes de que los resultados estén disponibles. Esto suele ser más eficaz que enviar instrucciones por separado, ya que el tráfico de red a menudo se puede reducir y el origen de datos a veces puede optimizar la ejecución de un lote de instrucciones SQL. En otras implementaciones, llamar a **SQLMoreResults** desencadena la ejecución de la siguiente instrucción en el lote. ODBC admite los siguientes tipos de lotes:  
  
-   **Lotes explícitos** Un *lote explícito* es dos o más instrucciones SQL separadas por punto y coma (;). Por ejemplo, el siguiente lote de instrucciones SQL abre un nuevo pedido de ventas. Esto requiere insertar filas en las tablas Orders y Lines. Tenga en cuenta que no hay punto y coma después de la última instrucción.  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **Procedimientos** Si un procedimiento contiene más de una instrucción SQL, se considera un lote de instrucciones SQL. Por ejemplo, la siguiente instrucción específica de SQL Server crea un procedimiento que devuelve un conjunto de resultados que contiene información sobre un cliente y un conjunto de resultados que enumera todos los pedidos de ventas abiertos para ese cliente:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     La instrucción **CREATE PROCEDURE** en sí no es un lote de instrucciones SQL. Sin embargo, el procedimiento que crea es un lote de instrucciones SQL. No hay punto y coma separar las dos instrucciones **SELECT** porque la instrucción **CREATE PROCEDURE** es específica de SQL ServerY SQL ServerSQL Server no requiere punto y coma para separar varias instrucciones en una instrucción **CREATE PROCEDURE.**  
  
-   **Matrices de parámetros** Las matrices de parámetros se pueden utilizar con una instrucción SQL parametrizada como una forma eficaz de realizar operaciones masivas. Por ejemplo, las matrices de parámetros se pueden utilizar con la siguiente instrucción **INSERT** para insertar varias filas en la tabla Lines mientras se ejecuta una sola instrucción SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Si un origen de datos no admite matrices de parámetros, el controlador puede emularlos ejecutando la instrucción SQL una vez para cada conjunto de parámetros. Para obtener más información, consulte [Parámetros](../../../odbc/reference/develop-app/statement-parameters.md) de instrucción y [matrices de](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)valores de parámetro , más adelante en esta sección.  
  
 Los diferentes tipos de lotes no se pueden mezclar de forma interoperable. Es decir, cómo una aplicación determina el resultado de ejecutar un lote explícito que incluye llamadas a procedimientos, un lote explícito que usa matrices de parámetros y una llamada a procedimiento que usa matrices de parámetros es específica del controlador.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Instrucciones generan resultados y libre de resultado](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Ejecución de lotes](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Errores y los lotes](../../../odbc/reference/develop-app/errors-and-batches.md)
