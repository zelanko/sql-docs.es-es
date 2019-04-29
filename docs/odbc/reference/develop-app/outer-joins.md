---
title: Combinaciones externas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 827dd531eda338f4fd297a4420ed144d46a613ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62998929"
---
# <a name="outer-joins"></a>Combinaciones externas
ODBC admite el SQL-92 dejado, sintaxis de combinación externa completa y correcta. Es la secuencia de escape para las combinaciones externas  
  
 **{oj** _outer-join_**}**  
  
 donde *combinación externa* es  
  
 *referencia de tabla* {**izquierda &#124; derecha &#124; completa} OUTER JOIN** {*referencia de tabla* &#124; *combinación externa*} **ON**  _condición de búsqueda_  
  
 *referencia de tabla* especifica un nombre de tabla y *condición de búsqueda* especifica la condición de combinación entre la *referencias de tabla*.  
  
 Una solicitud de combinación externa debe aparecer después de la **FROM** palabra clave y antes de la **donde** cláusula (si existe). Para obtener información de la sintaxis completa, consulte [secuencia de Escape de combinación externa](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) en el apéndice C: Gramática de SQL.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados que muestra a todos los clientes e indica que tiene pedidos pendientes. La primera instrucción usa la sintaxis de la secuencia de escape. La segunda instrucción utiliza la sintaxis nativa para Oracle y no es interoperable.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Para determinar los tipos de combinaciones externas que admiten un origen de datos y el controlador, una aplicación llama a **SQLGetInfo** con el SQL_OJ_CAPABILITIES indicador. Los tipos de combinaciones externas que pudieran ser compatibles son izquierdos, derecha, completo o combinaciones externas; anidadas combinaciones externas en que los nombres de columna en la **ON** cláusula no tiene el mismo orden que sus nombres de tabla correspondiente en el **OUTER JOIN** cláusula; las combinaciones internas, junto con las combinaciones externas; y combinaciones externas mediante cualquier operador de comparación ODBC. Si el tipo de información SQL_OJ_CAPABILITIES devuelve 0, no se admite ninguna cláusula de combinación externa.
