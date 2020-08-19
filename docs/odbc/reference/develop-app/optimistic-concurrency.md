---
description: Simultaneidad optimista
title: Simultaneidad optimista | Microsoft Docs
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
ms.openlocfilehash: dce1982edbb8f5a417404c6e24e8a40d25b58e0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429137"
---
# <a name="optimistic-concurrency"></a>Simultaneidad optimista
La *simultaneidad optimista* deriva su nombre de la suposición optimista de que las colisiones entre las transacciones se producen con poca frecuencia; se dice que se ha producido un conflicto cuando otra transacción actualiza o elimina una fila de datos entre el momento en que la transacción actual lo lee y el momento en que se actualiza o elimina. Es lo contrario de la *simultaneidad pesimista,* o bloqueo, en el que el desarrollador de la aplicación considera que dichas colisiones son habituales.  
  
 En la simultaneidad optimista, una fila se deja desbloqueada hasta que el tiempo llega a actualizarse o eliminarse. En ese momento, la fila se vuelve a leer y se comprueba para ver si se ha cambiado desde la última vez que se leyó. Si la fila ha cambiado, se produce un error en la actualización o en la eliminación y se debe volver a intentar.  
  
 Para determinar si una fila ha cambiado, se comprueba su nueva versión en una versión almacenada en caché de la fila. Esta comprobación se puede basar en la versión de fila, como la columna TIMESTAMP en SQL Server, o los valores de cada columna de la fila. Muchos DBMS no admiten las versiones de fila.  
  
 La simultaneidad optimista puede ser implementada por el origen de datos o la aplicación. En cualquier caso, la aplicación debe usar un nivel de aislamiento de transacción bajo, como Read Committed; el uso de un nivel superior niega la mayor simultaneidad obtenida mediante el uso de la simultaneidad optimista.  
  
 Si el origen de datos implementa la simultaneidad optimista, la aplicación establece el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES. Para actualizar o eliminar una fila, ejecuta una instrucción UPDATE o DELETE posicionada o llama a **SQLSetPos** tal como lo haría con la simultaneidad pesimista; el controlador o el origen de datos devuelve SQLSTATE 01001 (conflicto de la operación de cursor) si se produce un error en la actualización o eliminación debido a una colisión.  
  
 Si la propia aplicación implementa simultaneidad optimista, establece el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY para leer una fila. Si compara las versiones de fila y no conoce la columna de versión de fila, llama a **SQLSpecialColumns** con la opción SQL_ROWVER para determinar el nombre de esta columna.  
  
 La aplicación actualiza o elimina la fila al aumentar la simultaneidad a SQL_CONCUR_LOCK (para obtener acceso de escritura a la fila) y ejecutar una instrucción **Update** o **Delete** con una cláusula **Where** que especifica la versión o los valores que la fila tenía cuando la aplicación la leyó. Si la fila ha cambiado desde entonces, se producirá un error en la instrucción. Si la cláusula **Where** no identifica de forma única la fila, la instrucción también podría actualizar o eliminar otras filas; las versiones de fila siempre identifican de forma única las filas, pero los valores de fila solo identifican las filas si incluyen la clave principal.
