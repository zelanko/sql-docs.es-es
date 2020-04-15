---
title: Las Uniones Exteriores (Outer Joins) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81988d34dca38d5c041ff9f87e9674d7c97d76cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282455"
---
# <a name="outer-joins"></a>Combinaciones externas
ODBC admite la sintaxis de combinación externa izquierda, derecha y completa de SQL-92. La secuencia de escape para las uniones externas es  
  
 **•oj** _outer-join_**?**  
  
 donde la *unión externa* es  
  
 *referencia de tabla:* **izquierda &#124; derecha &#124; FULL- OUTER JOIN** - referencia de*tabla* &#124; *de unión externa*- **ON** _search-condition_  
  
 *referencia de tabla* especifica un nombre de tabla y *search-condition* especifica la condición de combinación entre las *referencias de tabla*.  
  
 Una solicitud de combinación externa debe aparecer después de la palabra clave **FROM** y antes de la cláusula **WHERE** (si existe). Para obtener información completa sobre la sintaxis, consulte Secuencia de escape de [unión externa](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) en apéndice C: gramática SQL.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados que enumera todos los clientes y muestra los pedidos abiertos. La primera instrucción utiliza la sintaxis de secuencia de escape. La segunda instrucción utiliza la sintaxis nativa para Oracle y no es interoperable.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Para determinar los tipos de combinaciones externas que admiten un origen de datos y un controlador, una aplicación llama a **SQLGetInfo** con el SQL_OJ_CAPABILITIES marca. Los tipos de combinaciones externas que se pueden admitir son las combinaciones externas izquierda, derecha, completa o anidada; combinaciones externas en las que los nombres de columna de la cláusula **ON** no tienen el mismo orden que sus respectivos nombres de tabla en la cláusula **OUTER JOIN;** uniones internas junto con uniones externas; y combinaciones externas mediante cualquier operador de comparación ODBC. Si el tipo de información SQL_OJ_CAPABILITIES devuelve 0, no se admite ninguna cláusula de combinación externa.
