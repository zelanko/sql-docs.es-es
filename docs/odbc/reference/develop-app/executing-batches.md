---
description: Ejecución de lotes
title: Ejecutar lotes | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3bb923f95dfcfb731d472aad8ead7ff35053171
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424647"
---
# <a name="executing-batches"></a>Ejecución de lotes
Antes de que una aplicación ejecute un lote de instrucciones, primero debe comprobar si se admiten. Para ello, la aplicación llama a **SQLGetInfo** con las opciones SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS. La primera opción devuelve si las instrucciones de generación de recuento de filas y de generación de conjuntos de resultados se admiten en lotes y procedimientos explícitos, mientras que las dos últimas opciones devuelven información sobre la disponibilidad de los recuentos de filas y conjuntos de resultados en la ejecución parametrizada.  
  
 Los lotes de instrucciones se ejecutan a través de **SQLExecute** o **SQLExecDirect**. Por ejemplo, la siguiente llamada ejecuta un lote explícito de instrucciones para abrir un nuevo pedido de ventas.  
  
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
  
 Cuando se ejecuta un lote de instrucciones que generan resultados, devuelve uno o más recuentos de filas o conjuntos de resultados. Para obtener información sobre cómo recuperarlos, vea [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Si un lote de instrucciones incluye marcadores de parámetros, se numeran al aumentar el orden de los parámetros, ya que se encuentran en cualquier otra instrucción. Por ejemplo, el siguiente lote de instrucciones tiene parámetros numerados del 1 al 21; los de la primera instrucción **Insert** se numeran del 1 al 5 y los de la última instrucción **Insert** se numeran del 18 al 21.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 Para obtener más información sobre los parámetros, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.
