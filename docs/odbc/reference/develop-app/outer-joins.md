---
description: Combinaciones externas
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9be14c2b7c0dd6cdebc458fd22dc090862eb9dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429127"
---
# <a name="outer-joins"></a>Combinaciones externas
ODBC admite la sintaxis de combinación externa izquierda, derecha y completa de SQL-92. La secuencia de escape para las combinaciones externas es  
  
 **{do** _outer join_**}**  
  
 donde *outer-join* es  
  
 *referencia de tabla* {**LEFT &#124; Right &#124; Full} combinación externa** {*referencia de tabla* &#124; *outer-join*} **en** _la condición de búsqueda_  
  
 *TABLE-Reference* especifica un nombre de tabla, y la *condición de búsqueda* especifica la condición de combinación entre las *referencias de tabla*.  
  
 Una solicitud de combinación externa debe aparecer después de la palabra clave **from** y antes de la cláusula **Where** (si existe). Para obtener información sobre la sintaxis completa, vea [secuencia de escape de combinación externa](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) en el Apéndice C: gramática de SQL.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados que muestra todos los clientes y muestra los pedidos abiertos. La primera instrucción usa la sintaxis de secuencia de escape. La segunda instrucción usa la sintaxis nativa para Oracle y no es interoperable.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Para determinar los tipos de combinaciones externas que admite un origen de datos y un controlador, una aplicación llama a **SQLGetInfo** con la marca SQL_OJ_CAPABILITIES. Los tipos de combinaciones externas que se pueden admitir son Left, Right, Full o outer join anidadas. combinaciones externas en las que los nombres de columna de la cláusula **on** no tienen el mismo orden que sus respectivos nombres de tabla en la cláusula **outer join** ; combinaciones internas junto con combinaciones externas; y combinaciones externas con cualquier operador de comparación de ODBC. Si el tipo de información SQL_OJ_CAPABILITIES devuelve 0, no se admite ninguna cláusula outer join.
