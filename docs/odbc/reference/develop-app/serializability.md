---
description: La posibilidad de serializar
title: Serializabilidad | Microsoft Docs
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
ms.openlocfilehash: b627d24b16e0bae4a117dba38de8cc1755feadac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476447"
---
# <a name="serializability"></a>La posibilidad de serializar
Idealmente, las transacciones deben ser *serializables*. Se dice que las transacciones son serializables si los resultados de ejecutar transacciones simultáneamente son los mismos que los resultados de ejecutarlas en serie, es decir, una tras otra. No es importante que la transacción se ejecute en primer lugar, solo que el resultado no refleja ninguna combinación de las transacciones.  
  
 Por ejemplo, supongamos que la transacción A multiplica los valores de datos por 2 y la transacción B suma 1 a los valores de datos. Supongamos ahora que hay dos valores de datos: 0 y 10. Si estas transacciones se ejecutan una tras otra, los nuevos valores serán 1 y 21 si la transacción A se ejecuta primero, o 2 y 22 si la transacción B se ejecuta primero. Pero, ¿qué ocurre si el orden en el que se ejecutan las dos transacciones es diferente para cada valor? Si la transacción A se ejecuta primero en el primer valor y la transacción B se ejecuta primero en el segundo valor, los nuevos valores son 1 y 22. Si se revierte este orden, los nuevos valores son 2 y 21. Las transacciones son serializables si 1, 21 y 2, 22 son los únicos resultados posibles. Las transacciones no se pueden serializar si 1, 22 o 2, 21 es un resultado posible.  
  
 ¿Por qué es conveniente la serialización? En otras palabras, ¿por qué es importante que parezca que una transacción finaliza antes de que se inicie la siguiente transacción? Tenga en cuenta el siguiente problema. Un vendedor está introduciendo pedidos al mismo tiempo que un funcionario envía facturas. Supongamos que el vendedor introduce un pedido de la empresa X pero no lo confirma; el vendedor todavía está hablando con el representante de la empresa X. El funcionario solicita una lista de todos los pedidos abiertos y detecta el pedido de la empresa X y les envía una factura. Ahora, el representante de la empresa X decide que desea cambiar su orden, por lo que el responsable de ventas lo cambia antes de confirmar la transacción. La empresa X obtiene una factura incorrecta.  
  
 Si las transacciones del vendedor y del funcionario fueran serializables, este problema nunca se habría producido. La transacción del vendedor habría finalizado antes de que se iniciara la transacción del funcionario, en cuyo caso el funcionario habría enviado la factura correcta o la transacción del funcionario hubiera finalizado antes de que se iniciara la transacción del vendedor, en cuyo caso el funcionario no habría enviado ninguna factura a la empresa X.
