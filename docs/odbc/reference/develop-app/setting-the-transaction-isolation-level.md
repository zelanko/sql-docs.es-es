---
title: Establecimiento del nivel de aislamiento de la transacción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37b575f9e208b5a1b7fa03b170b74633da149c67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63237877"
---
# <a name="setting-the-transaction-isolation-level"></a>Establecer el nivel de aislamiento de la transacción
Para establecer el nivel de aislamiento de transacción, una aplicación usa el atributo de conexión SQL_ATTR_TXN_ISOLATION. Si el origen de datos no admite el nivel de aislamiento solicitado, el controlador o el origen de datos puede establecer un nivel más alto. Para determinar qué aislamiento de transacción de los niveles de un origen de datos admite y es lo que el nivel de aislamiento de forma predeterminada, una aplicación llama a **SQLGetInfo** con las opciones SQL_TXN_ISOLATION_OPTION y SQL_DEFAULT_TXN_ISOLATION, respectivamente.  
  
 Mayores niveles de aislamiento de transacción ofrecen la máxima protección para la integridad de la base de datos. Las transacciones serializables se garantice se verá afectado por otras transacciones y, por tanto, para mantener la integridad de la base de datos.  
  
 Sin embargo, un mayor nivel de aislamiento de transacción puede provocar un rendimiento más lento porque aumenta las posibilidades de que la aplicación tendrá que esperar bloqueos en los datos que se libere. Una aplicación puede especificar un nivel inferior de aislamiento para aumentar el rendimiento en los casos siguientes:  
  
-   Cuando se pueda garantizar que ninguna otra transacción existe que podría interferir con las transacciones de la aplicación. Esta situación se produce solo en contadas circunstancias, por ejemplo, cuando una persona en una empresa pequeña mantiene archivos dBASE que contienen datos del personal en un equipo y no comparte estos archivos.  
  
-   Cuando la velocidad es más importante que la precisión y los errores suelen ser pequeños. Por ejemplo, supongamos que una compañía pone a su número de ventas pequeño y que las grandes ventas son poco frecuentes. Una transacción que calcula el valor total de todas las ventas podría utilizar sin ningún riesgo el nivel de aislamiento Read Uncommitted. Aunque la transacción incluiría los pedidos que sean los que se abre o se cierra y posteriormente revertido, estos podrían generalmente se cancelan entre sí y la transacción sería mucho más rápida porque no está bloqueado cada vez que TI detecta este tipo de un pedido.  
  
 Para obtener más información, consulte [simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).
