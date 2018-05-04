---
title: Errores y lotes | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f9ad11a7f9f0f89e2aa1320b221ce43ac04573e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="errors-and-batches"></a>Errores y los lotes
Cuando se produce un error al ejecutar un lote de instrucciones SQL, uno de los resultados de cuatro siguientes son posibles. (Cada resultado posible es específico del origen de datos e incluso podría depender de las instrucciones incluidas en el lote).  
  
-   Se ejecuta ninguna instrucción del lote.  
  
-   Se ejecuta ninguna instrucción del lote y se revierte la transacción.  
  
-   Se ejecutan todas las instrucciones antes de la instrucción de error.  
  
-   Se ejecutan todas las instrucciones excepto el error (instrucción).  
  
 En los dos primeros casos, **SQLExecute** y **SQLExecDirect** devolverá SQL_ERROR. En los dos últimos casos, pueden devolver SQL_SUCCESS_WITH_INFO o SQL_SUCCESS, dependiendo de la implementación. En todos los casos, obtener más información de error se puede recuperar con **SQLGetDiagField**, **SQLGetDiagRec**, o **SQLError**. Sin embargo, la naturaleza y la profundidad de esta información es específico del origen de datos. Además, esta información es probable que identificar exactamente la instrucción de error.
