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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44d31fc1f929ca60d34e49db135cefd1a8ae7ebc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831373"
---
# <a name="concurrency-control"></a>Control de simultaneidad
*Simultaneidad* es la capacidad de dos transacciones utilizan los mismos datos al mismo tiempo, y con transacciones mayor aislamiento normalmente viene una simultaneidad reducida. Esto es porque normalmente se implementa el aislamiento de transacción por bloqueo de filas y como se bloquean más filas, menos transacciones pueden realizarse sin que se bloquee temporalmente al menos una fila bloqueada. Mientras una simultaneidad reducida generalmente se acepta como Equilibrio de los mayores niveles de aislamiento de transacción necesarios para mantener la integridad de la base de datos, puede resultar un problema en las aplicaciones interactivas con actividad alta de lectura/escritura que usan los cursores.  
  
 Por ejemplo, suponga que una aplicación ejecuta la instrucción SQL **seleccione \* de pedidos**. Llama a **SQLFetchScroll** para desplazarse por el resultado establecido y permite al usuario actualizar, eliminar o insertar pedidos. Después de que el usuario actualiza, elimina o inserta un pedido, la aplicación confirma la transacción.  
  
 Si el nivel de aislamiento es Repeatable Read, es posible que la transacción, dependiendo de cómo se implementa, bloquea cada fila devuelta por **SQLFetchScroll**. Si el nivel de aislamiento es Serializable, la transacción puede bloquear toda la tabla de pedidos. En cualquier caso, la transacción libera sus bloqueos solo cuando se confirma o se revierte. Por lo que si el usuario necesita mucho tiempo en leer los pedidos y muy poco tiempo, la actualización, eliminación o insertarlos, la transacción puede bloquear fácilmente un gran número de filas, lo que no está disponible para otros usuarios.  
  
 Se trata de un problema incluso si el cursor es de solo lectura y la aplicación permite al usuario leer sólo los pedidos existentes. En este caso, la aplicación confirma la transacción y libera los bloqueos, cuando llama a **SQLCloseCursor** (en modo de confirmación automática) o **SQLEndTran** (en modo de confirmación manual).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de simultaneidad](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md)
