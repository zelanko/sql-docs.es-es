---
title: Configuración del nivel de aislamiento de la transacción ( Transaction Isolation Level) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80401b276355a47469355cb6921d768d168398ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299815"
---
# <a name="setting-the-transaction-isolation-level"></a>Establecer el nivel de aislamiento de la transacción
Para establecer el nivel de aislamiento de transacción, una aplicación utiliza el atributo de conexión SQL_ATTR_TXN_ISOLATION. Si el origen de datos no admite el nivel de aislamiento solicitado, el controlador o el origen de datos pueden establecer un nivel superior. Para determinar qué niveles de aislamiento de transacción admite un origen de datos y cuál es el nivel de aislamiento predeterminado, una aplicación llama a **SQLGetInfo** con las opciones SQL_TXN_ISOLATION_OPTION y SQL_DEFAULT_TXN_ISOLATION, respectivamente.  
  
 Los niveles más altos de aislamiento de transacciones ofrecen la mayor protección para la integridad de los datos de la base de datos. Se garantiza que las transacciones serializables no se verán afectadas por otras transacciones y, por lo tanto, se garantiza que se mantenga la integridad de la base de datos.  
  
 Sin embargo, un mayor nivel de aislamiento de transacción puede provocar un rendimiento más lento porque aumenta las posibilidades de que la aplicación tenga que esperar a que se liberen los bloqueos de los datos. Una aplicación puede especificar un nivel inferior de aislamiento para aumentar el rendimiento en los siguientes casos:  
  
-   Cuando se puede garantizar que no existen otras transacciones que puedan interferir con las transacciones de una aplicación. Esta situación se produce solo en circunstancias limitadas, como cuando una persona de una pequeña empresa mantiene archivos dBASE que contienen datos de personal en un equipo y no comparten estos archivos.  
  
-   Cuando la velocidad es más crítica que la precisión y es probable que los errores sean pequeños. Por ejemplo, supongamos que una empresa realiza muchas ventas pequeñas y que las ventas grandes son raras. Una transacción que estima el valor total de todas las ventas abiertas podría usar de forma segura el nivel de aislamiento Leer no confirmado. Aunque la transacción incluiría pedidos que se están abrir o cerrar y que posteriormente se revierten, generalmente se cancelarían entre sí y la transacción sería mucho más rápida porque no se bloquea cada vez que encuentra un pedido de este tipo.  
  
 Para obtener más información, vea [Simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).
