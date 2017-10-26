---
title: Control de simultaneidad | Documentos de Microsoft
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
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a10dc30810a1ea71bd4e2c9d823ed010f7f611d4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="concurrency-control"></a>Control de simultaneidad
*Simultaneidad* es la capacidad de dos transacciones utilizan los mismos datos al mismo tiempo, y transacciones mayor aislamiento normalmente conlleva una simultaneidad reducida. Esto es porque el aislamiento de transacciones normalmente se implementa mediante el bloqueo de filas, y porque están bloqueados más filas, menos transacciones pueden realizarse sin que se bloquee temporalmente al menos una fila bloqueada. Mientras una simultaneidad reducida suele aceptarse como una solución de compromiso de los mayores niveles de aislamiento de transacción necesarios para mantener la integridad de la base de datos, puede convertirse en un problema en las aplicaciones interactivas con actividad alta de lectura/escritura que usan los cursores.  
  
 Por ejemplo, suponga que una aplicación ejecuta la instrucción SQL **seleccione \* FROM Orders**. Llama **SQLFetchScroll** para desplazarse por el resultado configurada y permite al usuario actualizar, eliminar o insertar pedidos. Después de que el usuario actualiza, elimina o inserta un pedido, la aplicación confirma la transacción.  
  
 Si el nivel de aislamiento es Repeatable Read, es posible que la transacción, dependiendo de cómo se implementa: bloquear cada fila devuelta por **SQLFetchScroll**. Si el nivel de aislamiento es Serializable, la transacción puede bloquear toda la tabla de pedidos. En cualquier caso, la transacción libera sus bloqueos solo cuando se confirma o se revierte. Por lo que si el usuario necesita mucho tiempo en leer los pedidos y muy poco tiempo, la actualización, eliminación o insertándolos, la transacción puede bloquear fácilmente un gran número de filas, lo que no está disponible para otros usuarios.  
  
 Se trata de un problema incluso si el cursor es de solo lectura y la aplicación permite al usuario leer solo los pedidos existentes. En este caso, la aplicación confirma la transacción y libera los bloqueos, cuando llama a **SQLCloseCursor** (en modo de confirmación automática) o **SQLEndTran** (en modo de confirmación manual).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de simultaneidad](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md)

