---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa80ff3359e3bbbed9e28044cce7514006c40f10
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663823"
---
# <a name="optimistic-concurrency"></a>Simultaneidad optimista
*Simultaneidad optimista* deriva su nombre de la suposición optimista que no se suele producir colisiones entre transacciones; una colisión por haberse producido cuando otra transacción actualiza o elimina una fila de datos entre el momento en se lee por la transacción actual y la hora se actualiza o elimina. Es el opuesto de *simultaneidad pesimista,* o bloqueo, en que el desarrollador de aplicaciones cree que dichos conflictos son un lugar común.  
  
 En la simultaneidad optimista, se deja una fila desbloquear hasta que llegue el momento para actualizar o elimínelo. En ese momento, es volver a leer la fila y se comprueba para ver si se ha cambiado desde que se leyó por última vez. Si la fila ha cambiado, la actualización o eliminación produce un error y debe intentar de nuevo.  
  
 Para determinar si se ha cambiado una fila, se comprueba su versión nueva con una versión en caché de la fila. Esta comprobación puede basarse en la versión de fila, como la columna de marca de tiempo en SQL Server o los valores de cada columna de la fila. Muchos DBMS son compatibles con las versiones de fila.  
  
 El origen de datos o la aplicación se puede implementar la simultaneidad optimista. En cualquier caso, la aplicación debe utilizar un nivel de aislamiento de transacción bajo como Read Committed; uso de un nivel más alto niega la mayor simultaneidad obtenida mediante el uso de simultaneidad optimista.  
  
 Si la simultaneidad optimista se implementa mediante el origen de datos, la aplicación establece el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES. Para actualizar o eliminar una fila, ejecuta una actualización por posición o la instrucción delete o llamadas **SQLSetPos** tal como lo haría con la simultaneidad pesimista; el controlador u origen de datos devuelve SQLSTATE 01001 (conflicto de operación de Cursor) si el actualización o eliminación produce un error debido a una colisión.  
  
 Si la propia aplicación implementa la simultaneidad optimista, Establece el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY para leer una fila. Si compara las versiones de fila y no sabe la columna de la versión de fila, llama a **SQLSpecialColumns** con la opción SQL_ROWVER para determinar el nombre de esta columna.  
  
 La aplicación se actualiza o elimina la fila si aumenta la simultaneidad SQL_CONCUR_LOCK (para obtener acceso de escritura a la fila) y ejecutar un **actualización** o **eliminar** instrucción con un **donde**  cláusula que especifica la versión o los valores de la fila tenía cuando la aplicación pueda leerlo. Si la fila ha cambiado desde entonces, se producirá un error en la instrucción. Si el **donde** cláusula no identifica la fila, la instrucción también puede actualizar o eliminar las demás filas; las versiones de fila siempre identifican de filas, pero los valores de fila identifican filas sólo si se incluyen la clave principal.
