---
title: Establecer el nivel de aislamiento de la transacción | Documentos de Microsoft
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
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8ada820d501d49298cf245cbc88e8fbdfdba331
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setting-the-transaction-isolation-level"></a>Establecer el nivel de aislamiento de la transacción
Para establecer el nivel de aislamiento de transacción, una aplicación usa el atributo de conexión SQL_ATTR_TXN_ISOLATION. Si el origen de datos no admite el nivel de aislamiento solicitado, el controlador o el origen de datos puede establecer un nivel más alto. Para determinar qué aislamiento de transacción de los niveles de un origen de datos admite y cuál es el nivel de aislamiento predeterminado es, llama a una aplicación **SQLGetInfo** con las opciones SQL_TXN_ISOLATION_OPTION y SQL_DEFAULT_TXN_ISOLATION, respectivamente.  
  
 Mayores niveles de aislamiento de transacción ofrecen la máxima protección para la integridad de la base de datos. Las transacciones serializables se garantiza que se ve afectada por otras transacciones y garantiza que, por tanto, para mantener la integridad de la base de datos.  
  
 Sin embargo, un mayor nivel de aislamiento de transacción puede provocar un rendimiento más lento porque aumenta las posibilidades de que la aplicación tendrá que esperar bloqueos en los datos que se liberen. Una aplicación puede especificar un nivel inferior de aislamiento para aumentar el rendimiento en los casos siguientes:  
  
-   Cuando se pueda garantizar que ninguna otra transacción existe puede interferir con las transacciones de la aplicación. Esta situación se produce solo en contadas circunstancias, por ejemplo, cuando una persona en una pequeña empresa mantiene archivos dBASE que contienen datos del personal en un equipo y no comparte estos archivos.  
  
-   Cuando la velocidad es más importante que la precisión y los errores suelen ser pequeños. Por ejemplo, suponga que una compañía pone a su número de ventas pequeño y que sales grandes son poco frecuentes. Una transacción que calcula el valor total de todas las ventas podría utilizar de forma segura el nivel de aislamiento Read Uncommitted. Aunque la transacción incluiría pedidos que sean se abre o se cierra y posteriormente revierte, estos se generalmente se cancelan entre sí y la transacción sería mucho más rápida porque no se bloquea cada vez que TI encuentra un pedido de este tipo.  
  
 Para obtener más información, consulte [simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).
