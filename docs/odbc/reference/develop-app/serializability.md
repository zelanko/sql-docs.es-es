---
title: Serializabilidad ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0557e011578d313765614c05a2a9cf1b975bbc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304166"
---
# <a name="serializability"></a>La posibilidad de serializar
Idealmente, las transacciones deben ser *serializables.* Se dice que las transacciones son serializables si los resultados de las transacciones en ejecución simultáneamente son los mismos que los resultados de ejecutarlas en serie, es decir, una tras otra. No es importante qué transacción se ejecuta primero, solo que el resultado no refleja ninguna mezcla de las transacciones.  
  
 Por ejemplo, supongamos que la transacción A multiplica los valores de datos por 2 y la transacción B agrega 1 a los valores de datos. Ahora supongamos que hay dos valores de datos: 0 y 10. Si estas transacciones se ejecutan una tras otra, los nuevos valores serán 1 y 21 si la transacción A se ejecuta primero, o 2 y 22 si la transacción B se ejecuta primero. Pero, ¿qué pasa si el orden en el que se ejecutan las dos transacciones es diferente para cada valor? Si la transacción A se ejecuta primero en el primer valor y la transacción B se ejecuta primero en el segundo valor, los nuevos valores son 1 y 22. Si se invierte este orden, los nuevos valores son 2 y 21. Las transacciones son serializables si 1, 21 y 2, 22 son los únicos resultados posibles. Las transacciones no son serializables si 1, 22 o 2, 21 es un resultado posible.  
  
 Entonces, ¿por qué es deseable la serializabilidad? En otras palabras, ¿por qué es importante que parezca que una transacción finaliza antes de que se inicie la siguiente transacción? Considere el siguiente problema. Un vendedor está introduciendo pedidos al mismo tiempo que un empleado envía facturas. Supongamos que el vendedor introduce un pedido de la Empresa X pero no lo confirma; el vendedor sigue hablando con el representante de la Compañía X. El secretario solicita una lista de todas las órdenes abiertas y descubre el pedido para la Empresa X y les envía una factura. Ahora el representante de la Empresa X decide que desea cambiar su pedido, por lo que el vendedor lo cambia antes de confirmar la transacción. La Compañía X recibe una factura incorrecta.  
  
 Si las transacciones del vendedor y del empleado fueran serializables, este problema nunca habría ocurrido. O bien la transacción del vendedor habría terminado antes de que comenzara la transacción del secretario, en cuyo caso el secretario habría enviado la factura correcta, o la transacción del secretario habría terminado antes de que comenzara la transacción del vendedor, en cuyo caso el secretario no habría enviado una factura a la Compañía X en absoluto.
