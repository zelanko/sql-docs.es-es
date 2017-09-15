---
title: Simultaneidad optimista | Documentos de Microsoft
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
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3ae017de17892595dac94a0dd4bbb843d6d5f658
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="optimistic-concurrency"></a>Simultaneidad optimista
*Simultaneidad optimista* deriva su nombre de la suposición optimista que no se suele producir colisiones entre transacciones; una colisión han producido durante la otra transacción actualiza o elimina una fila de datos entre el momento en se leyó por la transacción actual y la hora se actualiza o elimina. Es lo contrario de *simultaneidad pesimista,* o bloqueo, en que el programador de aplicaciones cree que tales conflictos son comunes.  
  
 En la simultaneidad optimista, se deja una fila desbloquear hasta que llegue el momento de actualizar o eliminar. En ese momento, la fila se vuelve a leer directamente y comprueban para ver si se ha cambiado desde que se leyó por última vez. Si la fila ha cambiado, la actualización o eliminación tienen errores y debe intentar de nuevo.  
  
 Para determinar si se ha cambiado una fila, su nueva versión se compara con una versión almacenada en caché de la fila. Esta comprobación puede basarse en la versión de fila, como la columna de marca de tiempo en SQL Server o los valores de cada columna de la fila. Muchos DBMS son compatibles con las versiones de fila.  
  
 Simultaneidad optimista se puede implementar con el origen de datos o la aplicación. En cualquier caso, la aplicación debe utilizar un nivel de aislamiento de transacción baja como Read Committed; utilizar un nivel superior niega el mayor simultaneidad obtenida gracias al uso de simultaneidad optimista.  
  
 Si el origen de datos implementa la simultaneidad optimista, la aplicación establece el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES. Para actualizar o eliminar una fila, ejecuta una actualización por posición o instrucción delete o llamadas **SQLSetPos** tal como lo haría con la simultaneidad pesimista; el controlador u origen de datos devuelve SQLSTATE 01001 (conflictos de operación de Cursor) si el actualización o eliminación produce un error debido a una colisión.  
  
 Si la propia aplicación implementa simultaneidad optimista, Establece el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY para leer una fila. Si compara las versiones de fila y no sabe la columna de versión de fila, llama a **SQLSpecialColumns** con la opción SQL_ROWVER para determinar el nombre de esta columna.  
  
 La aplicación actualiza o elimina la fila aumentando la simultaneidad SQL_CONCUR_LOCK (para obtener acceso de escritura a la fila) y ejecutar un **actualización** o **eliminar** instrucción con un **donde ** cláusula que especifica la versión o los valores de la fila tenía cuando la aplicación que lo lee. Si la fila ha cambiado desde entonces, se producirá un error en la instrucción. Si el **donde** cláusula no identifica la fila, la instrucción también puede actualizar o eliminar otras filas; las versiones de fila siempre identifican de filas, pero los valores de fila identifican filas solo si se incluyen la clave principal.
