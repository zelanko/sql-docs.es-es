---
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
ms.openlocfilehash: 8afba3b3b8c8fee1307473c790186d509b37d982
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294855"
---
# <a name="concurrency-control"></a>Control de simultaneidad
*La simultaneidad* es la capacidad de dos transacciones para usar los mismos datos al mismo tiempo, y con el aumento del aislamiento de transacciones suele tener una simultaneidad reducida. Esto se debe a que el aislamiento de transacciones normalmente se implementa bloqueando filas y, a medida que se bloquean más filas, se pueden completar menos transacciones sin que una fila bloqueada bloquee al menos temporalmente temporalmente. Aunque la simultaneidad reducida se acepta generalmente como compensación para los niveles de aislamiento de transacción más altos necesarios para mantener la integridad de la base de datos, puede convertirse en un problema en aplicaciones interactivas con alta actividad de lectura y escritura que usan cursores.  
  
 Por ejemplo, supongamos que una aplicación ejecuta la instrucción SQL **SELECT \* FROM Orders**. Llama a **SQLFetchScroll** para desplazarse por el conjunto de resultados y permite al usuario actualizar, eliminar o insertar pedidos. Después de que el usuario actualiza, elimina o inserta un pedido, la aplicación confirma la transacción.  
  
 Si el nivel de aislamiento es Repeatable Read, la transacción podría bloquear cada fila devuelta por **SQLFetchScroll,** dependiendo de cómo se implemente. Si el nivel de aislamiento es Serializable, la transacción podría bloquear toda la tabla Orders. En cualquier caso, la transacción libera sus bloqueos solo cuando se confirma o se revierte. Por lo tanto, si el usuario pasa mucho tiempo leyendo pedidos y muy poco tiempo actualizándolos, eliminando o insertándolos, la transacción podría bloquear fácilmente un gran número de filas, haciéndolos no disponibles para otros usuarios.  
  
 Esto es un problema incluso si el cursor es de solo lectura y la aplicación permite al usuario leer solo los pedidos existentes. En este caso, la aplicación confirma la transacción y libera bloqueos cuando llama a **SQLCloseCursor** (en modo de confirmación automática) o **SQLEndTran** (en modo de confirmación manual).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de simultaneidad](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md)
