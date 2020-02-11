---
title: Errores y lotes | Microsoft Docs
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
ms.openlocfilehash: 6902b82c74e953d6009d7e5352608477d92122d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68051131"
---
# <a name="errors-and-batches"></a>Errores y los lotes
Cuando se produce un error al ejecutar un lote de instrucciones SQL, es posible que se produzca uno de los cuatro resultados siguientes. (Cada resultado posible es específico del origen de datos y puede incluso depender de las instrucciones incluidas en el lote).  
  
-   No se ejecuta ninguna instrucción en el lote.  
  
-   No se ejecutan instrucciones en el lote y la transacción se revierte.  
  
-   Todas las instrucciones anteriores a la instrucción error se ejecutan.  
  
-   Se ejecutan todas las instrucciones excepto la instrucción error.  
  
 En los dos primeros casos, **SQLExecute** y **SQLExecDirect** devuelven SQL_ERROR. En los dos últimos casos, pueden devolver SQL_SUCCESS_WITH_INFO o SQL_SUCCESS, en función de la implementación. En todos los casos, se puede recuperar más información de error con **SQLGetDiagField**, **SQLGetDiagRec**o **SQLError**. Sin embargo, la naturaleza y la profundidad de esta información son específicas del origen de datos. Además, es poco probable que esta información Identifique exactamente la instrucción con errores.
