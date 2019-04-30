---
title: Seriabilidad | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7972fb72607edca8c1599c2d028b073c184642
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251455"
---
# <a name="serializability"></a>La posibilidad de serializar
Idealmente, deberían ser transacciones *serializable*. Las transacciones se dice que ser serializable si los resultados de ejecutar al mismo tiempo las transacciones son los mismos que los resultados de su ejecución en serie: es decir, una tras otra. No es importante qué transacción se ejecuta en primer lugar, solo que el resultado no refleja cualquier combinación de las transacciones.  
  
 Por ejemplo, suponga que la transacción A multiplica los valores de datos por 2 y la transacción B agrega 1 a valores de datos. Ahora suponga que hay dos valores de datos: 0 y 10. Si estas transacciones se ejecutan una tras otra, los nuevos valores será 1 y 21 Si una transacción se ejecuta en primer lugar, o 2 y 22 si la transacción B se ejecuta primera. Pero ¿qué ocurre si el orden en que se ejecutan las dos transacciones es diferente para cada valor? Si la transacción A se ejecuta primera en el primer valor y la transacción B se ejecutan primeros en el segundo valor, los nuevos valores son 1 y 22. Si se invierte este orden, los nuevos valores son 2 y 21. Las transacciones son serializables si 1, 21 y 2, 22 se muestran los resultados solo es posibles. Las transacciones no son serializable si 22, 1 o 2, 21 es un resultado.  
  
 Entonces, ¿por qué seriabilidad es deseable? En otras palabras, ¿por qué es importante que aparece una transacción finaliza antes de que comience la siguiente transacción? Considere el siguiente problema. Un vendedor está entrando en pedidos al mismo tiempo que un empleado envía las facturas. Suponga que el vendedor entra en un orden de la compañía X, pero no confirma todavía está hablando con al representante del vendedor de la empresa X. El distribuidor y solicita una lista de todos los pedidos abiertos detecta el orden de la compañía X y los envía una factura. Ahora el representante de la compañía X decide que desean cambiar su orden, por lo que cambia el vendedor, antes de confirmar la transacción. X de la compañía obtiene una factura incorrecta.  
  
 Si las transacciones del vendedor y del distribuidor son serializables, nunca habría producido este problema. Transacción del vendedor habría terminado antes de inicia la transacción del distribuidor, en cuyo caso habría enviado el distribuidor de la factura correcta o habría terminado de transacciones del distribuidor antes de iniciar transacciones del vendedor, en cuyo caso el distribuidor no habría envía una factura a la compañía X en absoluto.
