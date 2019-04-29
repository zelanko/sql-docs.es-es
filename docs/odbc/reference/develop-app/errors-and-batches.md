---
title: Errores y los lotes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 97179574407dca56026f9d5216e4978069cffc1e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62942988"
---
# <a name="errors-and-batches"></a>Errores y los lotes
Cuando se produce un error al ejecutar un lote de instrucciones SQL, uno de los siguientes cuatro resultados son posibles. (Cada resultado posible es específica del origen de datos e incluso podría depender de las instrucciones incluidas en el lote).  
  
-   Se ejecuta ninguna instrucción del lote.  
  
-   Se ejecuta ninguna instrucción del lote y se revierte la transacción.  
  
-   Se ejecutan todas las instrucciones antes de la instrucción de error.  
  
-   Se ejecutan todas las instrucciones excepto la instrucción de error.  
  
 En los dos primeros casos, **SQLExecute** y **SQLExecDirect** devolverá SQL_ERROR. En los dos últimos casos, que es posible que devuelvan SQL_SUCCESS_WITH_INFO o SQL_SUCCESS, dependiendo de la implementación. En todos los casos, aún más información de error se puede recuperar con **SQLGetDiagField**, **SQLGetDiagRec**, o **SQLError**. Sin embargo, la naturaleza y la profundidad de esta información es específica del origen de datos. Además, esta información es probable que identificar exactamente de la instrucción de error.
