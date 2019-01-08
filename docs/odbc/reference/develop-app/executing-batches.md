---
title: Ejecución de lotes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 53e1afcc780ff06d1d453f94deac984163099444
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541224"
---
# <a name="executing-batches"></a>Ejecución de lotes
Antes de que una aplicación ejecuta un lote de instrucciones, en primer lugar debe comprobar si son compatibles. Para ello, la aplicación llama a **SQLGetInfo** con las opciones SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS. La primera opción devuelve si generadora de recuento de filas y resultado de la generación de conjunto de instrucciones son compatibles con lotes explícitos y procedimientos, mientras que las dos últimas opciones devuelven información acerca de la disponibilidad de los recuentos de filas y el resultado se establece en parámetros ejecución.  
  
 Lotes de instrucciones se ejecutan a través de **SQLExecute** o **SQLExecDirect**. Por ejemplo, la llamada siguiente ejecuta un lote de instrucciones para abrir un nuevo pedido de ventas explícito.  
  
```  
SQLCHAR *BatchStmt =  
   "INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)"  
      "VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 1, 1234, 10);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 2, 987, 8);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 3, 566, 17);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 4, 412, 500)";  
  
SQLExecDirect(hstmt, BatchStmt, SQL_NTS);  
```  
  
 Cuando un lote de generan instrucciones se ejecuta, devuelve uno o más recuentos de filas o conjuntos de resultados. Para obtener información acerca de cómo recuperar estas, consulte [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Si un lote de instrucciones incluye marcadores de parámetros, estos se numeran en sentido ascendente de parámetro estén en cualquier otra instrucción. Por ejemplo, el siguiente lote de instrucciones tiene parámetros que se numeran del 1 al 21; los de la primera **insertar** instrucción están numerados 1 a 5 y aquellos en los últimos **insertar** instrucción están numerados 18 al 21.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.
