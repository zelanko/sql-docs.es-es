---
description: Lotes de instrucciones SQL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e342fd7eaef721f8fb0033a5ae022ca8de74cda1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465937"
---
# <a name="batches-of-sql-statements"></a>Lotes de instrucciones SQL
Un lote de instrucciones SQL es un grupo de dos o más instrucciones SQL o una única instrucción SQL que tiene el mismo efecto que un grupo de dos o más instrucciones SQL. En algunas implementaciones, se ejecuta toda la instrucción por lotes antes de que haya resultados disponibles. Esto suele ser más eficaz que el envío de instrucciones por separado, ya que el tráfico de red a menudo se puede reducir y el origen de datos a veces puede optimizar la ejecución de un lote de instrucciones SQL. En otras implementaciones, al llamar a **SQLMoreResults** se desencadena la ejecución de la siguiente instrucción en el lote. ODBC admite los siguientes tipos de lotes:  
  
-   **Lotes explícitos** Un *lote explícito* es dos o más instrucciones SQL separadas por punto y coma (;). Por ejemplo, el siguiente lote de instrucciones SQL abre un nuevo pedido de ventas. Esto requiere Insertar filas en las tablas Orders y Lines. Tenga en cuenta que no hay ningún punto y coma después de la última instrucción.  
  
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
  
-   **Procedimientos** de Si un procedimiento contiene más de una instrucción SQL, se considera que es un lote de instrucciones SQL. Por ejemplo, la siguiente instrucción específica de SQL Server crea un procedimiento que devuelve un conjunto de resultados que contiene información sobre un cliente y un conjunto de resultados que enumera todos los pedidos de venta abiertos para ese cliente:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     La instrucción **Create procedure** en sí no es un lote de instrucciones SQL. Sin embargo, el procedimiento que crea es un lote de instrucciones SQL. Sin puntos y comas separan las dos instrucciones **Select** porque la instrucción **Create procedure** es específica de SQL Server y SQL Server no requiere puntos y comas para separar varias instrucciones en una instrucción **Create procedure** .  
  
-   **Matrices de parámetros** Las matrices de parámetros se pueden usar con una instrucción SQL con parámetros como una forma eficaz de realizar operaciones masivas. Por ejemplo, se pueden usar matrices de parámetros con la siguiente instrucción **Insert** para insertar varias filas en la tabla Lines mientras se ejecuta una sola instrucción SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Si un origen de datos no admite matrices de parámetros, el controlador puede emularlas ejecutando la instrucción SQL una vez para cada conjunto de parámetros. Para obtener más información, vea [parámetros de instrucciones](../../../odbc/reference/develop-app/statement-parameters.md) y [matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md), más adelante en esta sección.  
  
 Los distintos tipos de lotes no se pueden combinar de forma interoperable. Es decir, la forma en que una aplicación determina el resultado de ejecutar un lote explícito que incluye llamadas a procedimientos, un lote explícito que usa matrices de parámetros y una llamada a procedimiento que utiliza matrices de parámetros es específica del controlador.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Instrucciones generan resultados y libre de resultado](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Ejecución de lotes](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Errores y los lotes](../../../odbc/reference/develop-app/errors-and-batches.md)
