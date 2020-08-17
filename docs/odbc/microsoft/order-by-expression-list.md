---
description: ORDER BY-lista de expresiones
title: ORDENAR por expresión-lista | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd084a1012d445c89cacba168f21267238bc250f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340621"
---
# <a name="order-by-expression-list"></a>ORDER BY-lista de expresiones
Las expresiones se pueden usar en la cláusula ORDER BY. Por ejemplo, en las cláusulas siguientes, la tabla se ordena por tres expresiones clave: a + b, c + d y e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 No se permite ningún orden en las funciones set o en una expresión que contenga una función set.
