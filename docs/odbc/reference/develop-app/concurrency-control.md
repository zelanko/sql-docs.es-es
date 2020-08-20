---
description: Control de simultaneidad
title: Control de simultaneidad | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e47308cc0224ef73689a3b82d1ab4186fd0c823a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461557"
---
# <a name="concurrency-control"></a>Control de simultaneidad
La *simultaneidad* es la capacidad de dos transacciones para usar los mismos datos al mismo tiempo y, con un mayor aislamiento de transacción, normalmente se reduce la simultaneidad. Esto se debe a que el aislamiento de la transacción normalmente se implementa mediante el bloqueo de filas y, a medida que se bloquean más filas, se pueden completar menos transacciones sin que se bloquee al menos temporalmente mediante una fila bloqueada. Aunque la simultaneidad reducida se acepta generalmente como un equilibrio para los niveles de aislamiento de transacción más altos necesarios para mantener la integridad de la base de datos, puede convertirse en un problema en aplicaciones interactivas con una actividad de lectura y escritura elevada que use cursores.  
  
 Por ejemplo, supongamos que una aplicación ejecuta la instrucción SQL **SELECT \* FROM Orders**. Llama a **SQLFetchScroll** para desplazarse por el conjunto de resultados y permite al usuario actualizar, eliminar o insertar pedidos. Una vez que el usuario actualiza, elimina o inserta un pedido, la aplicación confirma la transacción.  
  
 Si el nivel de aislamiento es repetible, puede que la transacción, en función de cómo se implemente, bloquee cada fila devuelta por **SQLFetchScroll**. Si el nivel de aislamiento es serializable, la transacción podría bloquear toda la tabla Orders. En cualquier caso, la transacción libera sus bloqueos solo cuando se confirma o se revierte. Por tanto, si el usuario emplea mucho tiempo en leer los pedidos y muy poco tiempo actualizando, eliminando o insertando, la transacción podría bloquear fácilmente un gran número de filas, de forma que no estén disponibles para otros usuarios.  
  
 Se trata de un problema incluso si el cursor es de solo lectura y la aplicación permite al usuario leer solo los pedidos existentes. En este caso, la aplicación confirma la transacción y libera los bloqueos, cuando llama a **SQLCloseCursor** (en modo de confirmación automática) o **SQLEndTran** (en modo de confirmación manual).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de simultaneidad](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md)
