---
title: Simultaneidad optimista ? Microsoft Docs
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
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30eba3ea03b4c798a74a8cb928014b582846607b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282500"
---
# <a name="optimistic-concurrency"></a>Simultaneidad optimista
*La simultaneidad optimista* deriva su nombre de la suposición optimista de que rara vez se producirán colisiones entre transacciones; se dice que se ha producido una colisión cuando otra transacción actualiza o elimina una fila de datos entre el momento en que la transacción actual la lee y el momento en que se actualiza o elimina. Es lo contrario de *la simultaneidad pesimista,* o el bloqueo, en el que el desarrollador de la aplicación cree que tales colisiones son comunes.  
  
 En la simultaneidad optimista, una fila se deja desbloqueada hasta que llega el momento de actualizarla o eliminarla. En ese momento, la fila se vuelve a leer y se comprueba para ver si se ha cambiado desde la última lectura. Si la fila ha cambiado, se produce un error en la actualización o eliminación y se debe volver a intentar.  
  
 Para determinar si se ha cambiado una fila, su nueva versión se comprueba con una versión almacenada en caché de la fila. Esta comprobación se puede basar en la versión de fila, como la columna de marca de tiempo en SQL ServerSQL Server o los valores de cada columna de la fila. Muchos DBMS no admiten versiones de fila.  
  
 La simultaneidad optimista se puede implementar mediante el origen de datos o la aplicación. En cualquier caso, la aplicación debe usar un nivel de aislamiento de transacción bajo, como Lectura confirmada; el uso de un nivel superior niega el aumento de la simultaneidad obtenida mediante el uso de simultaneidad optimista.  
  
 Si el origen de datos implementa la simultaneidad optimista, la aplicación establece el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES. Para actualizar o eliminar una fila, ejecuta una instrucción update o delete posicionada o llama a **SQLSetPos** tal como lo haría con la simultaneidad pesimista; el controlador o el origen de datos devuelve SQLSTATE 01001 (conflicto de operación de cursor) si se produce un error en la actualización o eliminación debido a una colisión.  
  
 Si la propia aplicación implementa la simultaneidad optimista, establece el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY para leer una fila. Si comparará versiones de fila y no conoce la columna de versión de fila, llama a **SQLSpecialColumns** con la opción SQL_ROWVER para determinar el nombre de esta columna.  
  
 La aplicación actualiza o elimina la fila aumentando la simultaneidad para SQL_CONCUR_LOCK (para obtener acceso de escritura a la fila) y ejecutando una instrucción **UPDATE** o **DELETE** con una cláusula **WHERE** que especifica la versión o los valores que tenía la fila cuando la aplicación la leyó. Si la fila ha cambiado desde entonces, se producirá un error en la instrucción. Si la cláusula **WHERE** no identifica de forma exclusiva la fila, la instrucción también puede actualizar o eliminar otras filas; las versiones de fila siempre identifican filas de forma única, pero los valores de fila identifican de forma única las filas solo si incluyen la clave principal.
