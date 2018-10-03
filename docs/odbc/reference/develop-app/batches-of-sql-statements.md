---
title: Lotes de instrucciones SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb6d91fef3e12a26d7082defa5b579e00dbae4ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775112"
---
# <a name="batches-of-sql-statements"></a>Lotes de instrucciones SQL
Un lote de instrucciones SQL es un grupo de dos o más instrucciones SQL o una única instrucción SQL que tiene el mismo efecto que un grupo de dos o más instrucciones SQL. En algunas implementaciones, se ejecuta la instrucción del lote completo para que los resultados estén disponibles. Esto suele ser más eficaz que enviar las instrucciones por separado, porque a menudo se puede reducir el tráfico de red y el origen de datos a veces puede optimizar la ejecución de un lote de instrucciones SQL. En otras implementaciones, una llamada a **SQLMoreResults** desencadena la ejecución de la siguiente instrucción del lote. ODBC admite los siguientes tipos de lotes:  
  
-   **Lotes explícitos** una *explícito de lotes* es dos o más instrucciones SQL separadas por punto y coma (;). Por ejemplo, el siguiente lote de instrucciones SQL abre un nuevo pedido de ventas. Para ello, insertar filas en las tablas Orders y líneas. Tenga en cuenta que no hay ningún punto y coma después de la última instrucción.  
  
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
  
-   **Procedimientos** si un procedimiento contiene más de una instrucción SQL, y se considera un lote de instrucciones SQL. Por ejemplo, la siguiente instrucción específicos de SQL Server crea un procedimiento que devuelve un conjunto que contiene información sobre un cliente y un listado de todos los pedidos de venta abiertos para que el cliente de conjunto de resultados de resultados:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     El **CREATE PROCEDURE** propia instrucción no es un lote de instrucciones SQL. Sin embargo, el procedimiento que crea es un lote de instrucciones SQL. Punto y coma no separar los dos **seleccione** instrucciones porque el **CREATE PROCEDURE** instrucción es específica de SQL Server y SQL Server no requiere el punto y coma para separar varias instrucciones en un  **CREATE PROCEDURE** instrucción.  
  
-   **Matrices de parámetros** matrices de parámetros se pueden usar con una instrucción SQL con parámetros como una forma eficaz para realizar operaciones masivas. Por ejemplo, se pueden usar matrices de parámetros con los siguientes **insertar** instrucción para insertar varias filas en la tabla de líneas al ejecutar una única instrucción SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Si un origen de datos no es compatible con matrices de parámetros, el controlador puede emular al ejecutar la instrucción SQL una vez para cada conjunto de parámetros. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md) y [matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md), más adelante en esta sección.  
  
 No se pueden mezclar los distintos tipos de lotes de una manera interoperable. Es decir, cómo una aplicación determina el resultado de ejecutar un lote explícito que incluye el procedimiento llama, un lote explícito que usa matrices de parámetros, y una llamada a procedimiento que usa matrices de parámetros es específica del controlador.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Instrucciones generan resultados y libre de resultado](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Ejecución de lotes](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Errores y los lotes](../../../odbc/reference/develop-app/errors-and-batches.md)
