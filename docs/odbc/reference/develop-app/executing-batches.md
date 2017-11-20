---
title: "Ejecución de lotes | Documentos de Microsoft"
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
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b3235040d910f2dd9b5bdbf4a81765d25dcd8be1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="executing-batches"></a>Ejecución de lotes
Antes de que una aplicación ejecuta un lote de instrucciones, debe comprobar primero si son compatibles. Para ello, la aplicación llama **SQLGetInfo** con las opciones de SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS. La primera opción devuelve si generación de recuento de filas y el resultado de conjunto: generar instrucciones son compatibles con lotes explícitos y procedimientos, mientras las dos últimas opciones devuelven información acerca de la disponibilidad de recuentos de filas y el resultado se establece en parámetros ejecución.  
  
 Lotes de instrucciones se ejecutan a través de **SQLExecute** o **SQLExecDirect**. Por ejemplo, la siguiente llamada ejecuta un lote de instrucciones para abrir un nuevo pedido de venta explícito.  
  
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
  
 Cuando un lote de la generación de resultados se ejecutan las instrucciones, devuelve uno o más recuentos de filas o conjuntos de resultados. Para obtener información sobre cómo recuperar estas, consulte [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Si un lote de instrucciones incluye marcadores de parámetros, estos se numeran de forma ascendente, orden de los parámetros tal como están en cualquier otra instrucción. Por ejemplo, el siguiente lote de instrucciones tiene parámetros que se numeran del 1 al 21; los de la primera **insertar** instrucción están numeradas 1 a 5 y aquellos en los últimos **insertar** instrucción están numeradas 18 al 21.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.

