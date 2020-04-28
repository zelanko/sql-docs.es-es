---
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
ms.openlocfilehash: 272fa0be844569d322679d444807f8c332b4837b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81291225"
---
# <a name="order-by-expression-list"></a>ORDER BY-lista de expresiones
Las expresiones se pueden usar en la cláusula ORDER BY. Por ejemplo, en las cláusulas siguientes, la tabla se ordena por tres expresiones clave: a + b, c + d y e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 No se permite ningún orden en las funciones set o en una expresión que contenga una función set.
