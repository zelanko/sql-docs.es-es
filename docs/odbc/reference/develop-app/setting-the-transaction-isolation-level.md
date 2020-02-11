---
title: Establecer el nivel de aislamiento de transacción | Microsoft Docs
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
ms.openlocfilehash: e59db823f8b84edfb5c92f2d142c8238449e3323
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107577"
---
# <a name="setting-the-transaction-isolation-level"></a>Establecer el nivel de aislamiento de la transacción
Para establecer el nivel de aislamiento de transacción, una aplicación utiliza el atributo de conexión SQL_ATTR_TXN_ISOLATION. Si el origen de datos no admite el nivel de aislamiento solicitado, el controlador o el origen de datos puede establecer un nivel superior. Para determinar qué niveles de aislamiento de transacción admite un origen de datos y cuál es el nivel de aislamiento predeterminado, una aplicación llama a **SQLGetInfo** con las opciones SQL_TXN_ISOLATION_OPTION y SQL_DEFAULT_TXN_ISOLATION, respectivamente.  
  
 Los niveles más altos de aislamiento de transacción ofrecen la máxima protección para la integridad de los datos de la base de datos. Se garantiza que las transacciones serializables no se ven afectadas por otras transacciones y, por tanto, se garantiza que se mantiene la integridad de la base de datos.  
  
 Sin embargo, un mayor nivel de aislamiento de transacción puede provocar un rendimiento más lento, ya que aumenta las posibilidades de que la aplicación tenga que esperar a que se liberen los bloqueos en los datos. Una aplicación puede especificar un nivel de aislamiento inferior para aumentar el rendimiento en los casos siguientes:  
  
-   Cuando se pueda garantizar que no existan otras transacciones que puedan interferir con las transacciones de una aplicación. Esta situación solo se produce en circunstancias limitadas, por ejemplo, cuando una persona de una empresa pequeña mantiene archivos dBASE que contienen datos personales en un equipo y no los comparten.  
  
-   Cuando la velocidad es más crítica que la precisión y es probable que los errores sean pequeños. Por ejemplo, supongamos que una empresa realiza muchas ventas pequeñas y que las grandes ventas son poco frecuentes. Una transacción que calcula el valor total de todas las ventas abiertas puede usar de forma segura el nivel de aislamiento READ UNCOMMITTED. Aunque la transacción incluiría pedidos que se están abriendo o cerrando y que se revierten posteriormente, normalmente se cancelarían entre sí y la transacción sería mucho más rápida porque no se bloqueó cada vez que encuentra un pedido.  
  
 Para obtener más información, consulte [simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).
