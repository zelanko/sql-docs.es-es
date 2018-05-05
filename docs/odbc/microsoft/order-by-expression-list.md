---
title: ORDER BY expression-list | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e531a26f0436c598fa04acc11e9735bb80faed44
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="order-by-expression-list"></a>ORDER BY-lista de expresiones
Pueden utilizarse expresiones en la cláusula ORDER BY. Por ejemplo, en las cláusulas siguientes en la tabla está ordenada por tres expresiones claves: a + b, c + d y e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Ninguna ordenación se permite en funciones de conjunto o una expresión que contiene una función de conjunto.
