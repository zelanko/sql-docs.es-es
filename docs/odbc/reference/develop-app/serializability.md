---
title: La posibilidad de serializar | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 81d23b5bc94f2982becca5e76ab28269d6c233c1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="serializability"></a>La posibilidad de serializar
Idealmente, deberían ser las transacciones *serializable*. Se dice que las transacciones que sean serializables si los resultados de ejecutar al mismo tiempo las transacciones son los mismos que los resultados de su ejecución en serie, es decir, una detrás de otra. No es importante qué transacción se ejecuta en primer lugar, solo que el resultado no refleja cualquier combinación de las transacciones.  
  
 Por ejemplo, suponga que la transacción A multiplica los valores de datos por 2 y la transacción B suma 1 a valores de datos. Ahora suponga que hay dos valores de datos: 0 y 10. Si estas transacciones se ejecutan una detrás de otra, los nuevos valores será 1 y 21 Si una transacción se ejecuta en primer lugar, o 2 y 22 si la transacción B se ejecuta primera. Pero ¿qué ocurre si el orden en el que se ejecutan las dos transacciones es diferente para cada valor? Si la transacción a que se ejecuta primero en el primer valor de y B se ejecución primeros en el segundo valor, los nuevos valores son 1 y 22. Si se invierte este orden, los nuevos valores son 2 y 21. Las transacciones son serializables si 1, 21 y 2, 22 son los resultados solo es posibles. Las transacciones no son serializable si 22, 1 o 2, 21 es un resultado posible.  
  
 ¿Por qué la posibilidad de serializar es deseable? En otras palabras, ¿por qué es importante que parece que una transacción finalice antes de que comience la siguiente transacción? Tenga en cuenta el siguiente problema. Un vendedor es realizar pedidos al mismo tiempo que un empleado envía las facturas. Suponga que el vendedor entra en un pedido de la compañía X, pero no confirma el vendedor todavía está hablando con el representante de la empresa X. El distribuidor y solicita una lista de todos los pedidos abiertos detecta el orden de la compañía X y los envía una factura. Ahora el representante de la compañía X decide que desean cambiar su orden, por lo que el vendedor cambia antes de confirmar la transacción. Empresa X Obtiene una factura incorrecta.  
  
 Si las transacciones del vendedor y del distribuidor son serializables, nunca habría producido este problema. Transacción del vendedor habría terminado antes de inicia la transacción del distribuidor, en cuyo caso el distribuidor habría envía la factura correcta o habría terminado de transacción del distribuidor antes de iniciar transacciones del vendedor, en cuyo caso el distribuidor no habría envía una factura a la empresa X en absoluto.

