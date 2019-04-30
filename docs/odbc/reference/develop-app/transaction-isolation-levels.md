---
title: Niveles de aislamiento de transacción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63e08aa2e75d560ce73c549d307418432ffe16af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149100"
---
# <a name="transaction-isolation-levels"></a>Niveles de aislamiento de transacción
*Niveles de aislamiento de transacción* son una medida de la extensión para la transacción de aislamiento se realizó correctamente. En concreto, se definen los niveles de aislamiento de transacción por la presencia o ausencia del fenómeno de la siguiente:  
  
-   **Dirty lecturas** A *lectura de datos sucios* se produce cuando una transacción lee los datos que no se ha confirmado. Por ejemplo, suponga que las actualizaciones de la transacción 1 una fila. La transacción 2 lee la fila actualizada antes de la actualización confirma la transacción 1. Si la transacción 1 revierte el cambio, la transacción 2 habrá leer datos que se consideran que nunca han existido.  
  
-   **Lecturas no repetibles** A *lectura irrepetible* se produce cuando una transacción lee la misma fila dos veces, pero obtiene datos diferentes cada vez. Por ejemplo, suponga una fila lecturas de la transacción 1. La transacción 2 se actualiza o elimina esa fila y confirma la actualización o eliminación. Si la transacción 1 vuelve a leer la fila, recupera los valores de fila diferente o detecta que se ha eliminado la fila.  
  
-   **Fantasmas** A *fantasma* es una fila que coincide con los criterios de búsqueda pero no se ve inicialmente. Por ejemplo, suponga que la transacción 1 lee un conjunto de filas que cumplen algunos criterios de búsqueda. La transacción 2 genera una nueva fila (a través de una actualización o una instrucción insert) que coincide con los criterios de búsqueda para la transacción 1. Si la transacción 1 reexecutes la instrucción que lee las filas, obtiene un conjunto diferente de filas.  
  
 Los cuatro niveles de aislamiento (como se define por SQL-92) se definen en términos de estos dos fenómenos. En la tabla siguiente, una "X" marca cada fenómeno que se puede producir.  
  
|nivel de aislamiento de transacción|Lecturas no actualizadas|Lecturas no repetibles|Fantasmas|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Lectura no confirmada|X|X|X|  
|Lectura confirmada|--|X|X|  
|Lectura repetible|--|--|X|  
|Serializable|--|--|--|  
  
 En la tabla siguiente se describe maneras sencillas que un DBMS podría implementar los niveles de aislamiento de transacción.  
  
> [!IMPORTANT]  
>  Mayoría de los DBMS utiliza esquemas más complejos de los anteriores para aumentar la simultaneidad. Estos ejemplos se proporcionan únicamente por motivos ilustrativos. En concreto, ODBC no prescribe DBMS determinados cómo aislar las transacciones entre sí.  
  
|aislamiento de transacción|Implementación posible|  
|---------------------------|-----------------------------|  
|Lectura no confirmada|Las transacciones no están aisladas entre sí. Si el DBMS es compatible con otros niveles de aislamiento de transacción, omite cualquier mecanismo usa para implementar esos niveles. Por lo que no afectan negativamente otras transacciones, transacciones que se ejecutan en el nivel Read Uncommitted son normalmente de solo lectura.|  
|Lectura confirmada|La transacción espera hasta que se desbloqueen; filas escritura bloqueadas por otras transacciones Esto evita que se pueda leer los datos de "sucios".<br /><br /> Contiene la transacción un bloqueo de lectura (si solo lee la fila) o de escritura de bloqueo (si actualiza o elimina la fila) en la fila actual para impedir que otras transacciones actualicen o eliminarlo. La transacción libera los bloqueos de lectura cuando se desplaza fuera de la fila actual. Contiene los bloqueos de escritura hasta que se confirma o revierte.|  
|Lectura repetible|La transacción espera hasta que se desbloqueen; filas escritura bloqueadas por otras transacciones Esto evita que se pueda leer los datos de "sucios".<br /><br /> La transacción mantiene bloqueos de lectura en todas las filas que devuelve a los bloqueos de aplicación y la escritura en todas las filas que inserciones, actualizaciones o se elimina. Por ejemplo, si la transacción incluye la instrucción SQL **seleccione \* de pedidos**, los bloqueos de lectura de transacciones filas como la aplicación captura ellos. Si la transacción incluye la instrucción SQL **eliminar de pedidos donde estado = 'Cerrado'**, los bloqueos de escritura de transacción filas como los elimina.<br /><br /> Dado que otras transacciones no se pueden actualizar o eliminar estas filas, la transacción actual evita las lecturas no repetibles. La transacción libera sus bloqueos cuando se confirma o revierte.|  
|Serializable|La transacción espera hasta que se desbloqueen; filas escritura bloqueadas por otras transacciones Esto evita que se pueda leer los datos de "sucios".<br /><br /> La transacción tiene un bloqueo de lectura (si solo lee filas) o bloqueo de escritura (si puede actualizar o eliminar filas) en el intervalo de filas afecta a. Por ejemplo, si la transacción incluye la instrucción SQL **seleccione \* de pedidos**, el intervalo es toda la tabla de pedidos; la lectura de bloqueos de transacciones la tabla y no no permitir nuevas filas va a insertar en él. Si la transacción incluye la instrucción SQL **eliminar de pedidos donde estado = 'Cerrado'**, el intervalo es de todas las filas con un estado de "CLOSED"; los bloqueos de escritura de transacción todas las filas de los pedidos de la tabla con el estado "CERRADA" y no no permitir que las filas que se inserten o se actualiza de forma que la fila resultante tiene un estado de "CLOSED".<br /><br /> Dado que otras transacciones no se pueden actualizar o eliminar las filas en el intervalo, la transacción actual evita las lecturas no repetibles. Dado que otras transacciones no pueden insertar filas en el intervalo, la transacción actual evita cualquier fantasmas. La transacción libera el bloqueo cuando se confirma o revierte.|  
  
 Es importante tener en cuenta que el nivel de aislamiento de transacción no afecta la capacidad de una transacción para ver los cambios en su propio; las transacciones siempre pueden ver los cambios que realicen. Por ejemplo, una transacción puede constar de dos **actualización** instrucciones, el primero de los cuales genera el pago de todos los empleados un 10 por ciento y el segundo de los cuales establece el pago de los empleados a través de cierta cantidad a dicha cantidad máxima. Esto se realiza como una sola transacción correctamente porque solo la segunda **actualización** instrucción puede ver los resultados de la primera.
