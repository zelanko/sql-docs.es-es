---
title: "Niveles de aislamiento de transacción | Documentos de Microsoft"
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
- dirty reads [ODBC]
- isolation levels [ODBC]
- nonrepeatable reads [ODBC]
- read uncommitted [ODBC]
- read committed [ODBC]
- serializable reads [ODBC]
- phantoms [ODBC]
- transaction isolation [ODBC]
- repeatable reads [ODBC]
- transactions [ODBC], isolation
ms.assetid: 0d638d55-ffd0-48fb-834b-406f466214d4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 13997d3c8d4bb3c4ea5ff47ec6e8d4c95b303d21
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="transaction-isolation-levels"></a>Niveles de aislamiento de transacción
*Niveles de aislamiento de transacción* son una medida de la extensión para las transacciones aislamiento se realizó correctamente. En concreto, los niveles de aislamiento de transacción se definen por la presencia o ausencia fenómenos siguientes:  
  
-   **Desfasadas lecturas** A *lectura de datos sucios* se produce cuando una transacción lee los datos que aún no se ha confirmado. Por ejemplo, suponga que las actualizaciones de la transacción 1 una fila. La transacción 2 lee la fila actualizada antes de que la actualización confirma la transacción 1. Si la transacción 1 revierte el cambio, la transacción 2 habrá leer datos que se consideran que nunca han existido.  
  
-   **Lecturas no repetibles** A *lectura irrepetible* se produce cuando una transacción lee la misma fila dos veces, pero obtiene datos diferentes cada vez. Por ejemplo, suponga una fila lecturas de la transacción 1. La transacción 2 se actualiza o elimina esa fila y confirma la actualización o eliminación. Si la transacción 1 vuelve a leer la fila, recupera los valores de fila diferente o detecta que se ha eliminado la fila.  
  
-   **Fantasmas** A *fantasma* es una fila que coincide con los criterios de búsqueda pero no se ve inicialmente. Por ejemplo, suponga que la transacción 1 lee un conjunto de filas que cumplen algunos criterios de búsqueda. La transacción 2 genera una nueva fila (mediante una actualización o en una instrucción insert) que coincide con los criterios de búsqueda para la transacción 1. Si la transacción 1 reexecutes la instrucción que lee las filas, obtiene un conjunto diferente de filas.  
  
 Los niveles de aislamiento de cuatro transacción (tal y como se define por SQL-92) se definen en función de estos dos fenómenos. En la tabla siguiente, una "X" marca cada fenómeno que se puede producir.  
  
|Nivel de aislamiento de transacción|Las lecturas no actualizadas|Lecturas no repetibles|Fantasmas|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Lectura no confirmada|X|X|X|  
|Lectura confirmada|--|X|X|  
|Lectura repetible|--|--|X|  
|Serializable|--|--|--|  
  
 La tabla siguiente describen varias maneras sencillas que un DBMS podría implementar los niveles de aislamiento de transacción.  
  
> [!IMPORTANT]  
>  Mayoría de los DBMS use combinaciones más complejas de los anteriores para aumentar la simultaneidad. Estos ejemplos se proporcionan únicamente con fines ilustrativos. En concreto, ODBC no prescribir DBMS determinados cómo aislar las transacciones entre sí.  
  
|Aislamiento de transacción|Posible implementación|  
|---------------------------|-----------------------------|  
|Lectura no confirmada|Las transacciones no están aisladas entre sí. Si el DBMS admite otros niveles de aislamiento de transacción, omite cualquier mecanismo que se usa para implementar esos niveles. Para que no afecten negativamente otras transacciones, transacciones que se ejecutan en el nivel Read Uncommitted son normalmente de solo lectura.|  
|Lectura confirmada|La transacción espera hasta que se ha desbloqueado; filas escritura bloqueadas por otras transacciones Esto evita que se pueda leer los datos de "sucios".<br /><br /> Las suspensiones de transacción un bloqueo de lectura (si solo lee la fila) o de escritura de bloqueo (si actualiza o elimina la fila) en la fila actual para impedir que otras transacciones actualicen o eliminarlo. La transacción libera los bloqueos de lectura cuando se desplaza fuera de la fila actual. Contiene los bloqueos de escritura hasta que se confirma o revierte.|  
|Lectura repetible|La transacción espera hasta que se ha desbloqueado; filas escritura bloqueadas por otras transacciones Esto evita que se pueda leer los datos de "sucios".<br /><br /> La transacción mantiene bloqueos de lectura en todas las filas que devuelve a los bloqueos de aplicación y escribir en todas las filas que inserciones, actualizaciones o se elimina. Por ejemplo, si la transacción incluye la instrucción SQL **seleccione \* FROM Orders**, los bloqueos de lectura de transacciones filas como la aplicación obtiene de ellos. Si la transacción incluye la instrucción SQL **eliminar de pedidos donde estado = 'Cerrado'**, los bloqueos de escritura de transacciones filas como los elimina.<br /><br /> Puesto que otras transacciones no se pueden actualizar o eliminar estas filas, la transacción actual evita las lecturas no repetibles. La transacción libera sus bloqueos cuando se confirma o revierte.|  
|Serializable|La transacción espera hasta que se ha desbloqueado; filas escritura bloqueadas por otras transacciones Esto evita que se pueda leer los datos de "sucios".<br /><br /> La transacción mantiene un bloqueo de lectura (si solo lee filas) o bloqueo de escritura (si puede actualizar o eliminar filas) en el intervalo de filas afecta a. Por ejemplo, si la transacción incluye la instrucción SQL **seleccione \* FROM Orders**, el intervalo es toda la tabla Orders; la transacción lectura bloqueos de la tabla y no no permitir nuevas filas va a insertar en él. Si la transacción incluye la instrucción SQL **eliminar de pedidos donde estado = 'Cerrado'**, el intervalo es todas las filas con un estado de "Cerrado"; los bloqueos de escritura de transacciones todas las filas de los pedidos de la tabla con un estado de "Cerrado" y no no permitir que ninguna fila para insertar o actualizar de forma que la fila resultante tiene un estado de "Cerrado".<br /><br /> Dado que otras transacciones no se pueden actualizar o eliminar las filas en el intervalo, la transacción actual evita las lecturas no repetibles. Dado que otras transacciones no pueden insertar las filas en el intervalo, la transacción actual evita cualquier fantasmas. La transacción libera el bloqueo cuando se confirma o revierte.|  
  
 Es importante tener en cuenta que el nivel de aislamiento de transacción no afecta la capacidad de una transacción para ver sus propios cambios; las transacciones siempre pueden ver los cambios realizados. Por ejemplo, una transacción puede constar de dos **actualización** instrucciones, el primero de los cuales genera el pago de todos los empleados 10 por ciento y el segundo de los cuales establece el sueldo de los empleados sobre algunos cantidad máxima de esa cantidad. Esto se realiza como una sola transacción correctamente solo porque el segundo **actualización** instrucción puede ver los resultados de la primera.
