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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cd88673c4b5309b7463256b85df4f92d6d360b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100792"
---
# <a name="order-by-expression-list"></a>ORDER BY-lista de expresiones
Las expresiones se pueden usar en la cláusula ORDER BY. Por ejemplo, en las cláusulas siguientes, la tabla se ordena por tres expresiones clave: a + b, c + d y e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 No se permite ningún orden en las funciones set o en una expresión que contenga una función set.
