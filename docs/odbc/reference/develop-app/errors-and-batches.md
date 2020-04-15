---
title: Errores y lotes ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36a402686a695a08748df24a7b40a228d7a2ca7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300435"
---
# <a name="errors-and-batches"></a>Errores y los lotes
Cuando se produce un error al ejecutar un lote de instrucciones SQL, es posible uno de los cuatro resultados siguientes. (Cada resultado posible es específico del origen de datos e incluso puede depender de las instrucciones incluidas en el lote.)  
  
-   No se ejecuta ninguna instrucción en el lote.  
  
-   No se ejecuta ninguna instrucción en el lote y se revierte la transacción.  
  
-   Se ejecutan todas las instrucciones antes de la instrucción de error.  
  
-   Se ejecutan todas las instrucciones excepto la instrucción de error.  
  
 En los dos primeros casos, **SQLExecute** y **SQLExecDirect** devuelven SQL_ERROR. En estos dos últimos casos, pueden devolver SQL_SUCCESS_WITH_INFO o SQL_SUCCESS, dependiendo de la aplicación. En todos los casos, se puede recuperar más información de error con **SQLGetDiagField**, **SQLGetDiagRec**o **SQLError**. Sin embargo, la naturaleza y la profundidad de esta información son específicas del origen de datos. Además, es poco probable que esta información identifique exactamente la declaración por error.
