---
title: Niveles de aislamiento de transacción (ODBC) | Microsoft Docs
ms.custom: seo-dt-2019
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 622b4cd7f0db259b5ecfd5be63b27df64be965e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298038"
---
# <a name="transaction-isolation-levels-odbc"></a>Niveles de aislamiento de transacción (ODBC)
Los *niveles de aislamiento de transacción* son una medida de la medida en que el aislamiento de la transacción se realiza correctamente. En concreto, los niveles de aislamiento de transacción se definen por la presencia o ausencia de los siguientes fenómenos:  
  
-   **Lecturas desfasadas** Una *lectura desfasada* se produce cuando una transacción lee datos que todavía no se han confirmado. Por ejemplo, supongamos que la transacción 1 actualiza una fila. La transacción 2 lee la fila actualizada antes de que la transacción 1 confirme la actualización. Si la transacción 1 revierte el cambio, la transacción 2 tendrá datos de lectura que se considera que nunca existían.  
  
-   **Lecturas no repetibles** Una *lectura no repetible* se produce cuando una transacción lee la misma fila dos veces, pero obtiene datos diferentes cada vez. Por ejemplo, supongamos que la transacción 1 Lee una fila. La transacción 2 actualiza o elimina esa fila y confirma la actualización o la eliminación. Si la transacción 1 relee la fila, recupera valores de fila diferentes o detecta que se ha eliminado la fila.  
  
-   **Fantasmas** Un *fantasma* es una fila que coincide con los criterios de búsqueda pero que no se ve inicialmente. Por ejemplo, supongamos que la transacción 1 Lee un conjunto de filas que cumplen algunos criterios de búsqueda. La transacción 2 genera una nueva fila (a través de una actualización o una inserción) que coincide con los criterios de búsqueda de la transacción 1. Si la transacción 1 reejecuta la instrucción que lee las filas, obtiene un conjunto de filas diferente.  
  
 Los cuatro niveles de aislamiento de transacción (tal y como se definen en SQL-92) se definen en términos de estos fenómenos. En la tabla siguiente, una "X" marca cada fenómeno que se puede producir.  
  
|Nivel de aislamiento de transacción|Lecturas desfasadas|Lecturas no repetibles|Fantasmas|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Lectura no confirmada|X|X|X|  
|Lectura confirmada|--|X|X|  
|Lectura repetible|--|--|X|  
|Serializable|--|--|--|  
  
 En la tabla siguiente se describen las formas sencillas en que un DBMS puede implementar los niveles de aislamiento de transacción.  
  
> [!IMPORTANT]  
>  La mayoría de los DBMS usan esquemas más complejos que estos para aumentar la simultaneidad. Estos ejemplos se proporcionan únicamente con fines ilustrativos. En concreto, ODBC no prescribe el modo en que los DBMS determinados aíslan las transacciones entre sí.  
  
|Aislamiento de transacción|Posible implementación|  
|---------------------------|-----------------------------|  
|Lectura no confirmada|Las transacciones no están aisladas entre sí. Si el DBMS admite otros niveles de aislamiento de transacción, omite cualquier mecanismo que use para implementar esos niveles. Para que no afecten negativamente a otras transacciones, las transacciones que se ejecutan en el nivel de lectura sin confirmar suelen ser de solo lectura.|  
|Lectura confirmada|La transacción espera hasta que se desbloquean las filas de escritura bloqueadas por otras transacciones. Esto evita que lea los datos "sucios".<br /><br /> La transacción contiene un bloqueo de lectura (si solo lee la fila) o el bloqueo de escritura (si actualiza o elimina la fila) en la fila actual para evitar que otras transacciones la actualicen o eliminen. La transacción libera los bloqueos de lectura cuando se desplaza fuera de la fila actual. Mantiene bloqueos de escritura hasta que se confirma o se revierte.|  
|Lectura repetible|La transacción espera hasta que se desbloquean las filas de escritura bloqueadas por otras transacciones. Esto evita que lea los datos "sucios".<br /><br /> La transacción mantiene bloqueos de lectura en todas las filas que devuelve a la aplicación y escribe bloqueos en todas las filas que inserta, actualiza o elimina. Por ejemplo, si la transacción incluye la instrucción SQL **SELECT \* FROM Orders**, la transacción de lectura bloquea las filas a medida que la aplicación las recopila. Si la transacción incluye la instrucción SQL **Delete de los pedidos en los que status = ' Closed '**, la transacción bloquea las filas cuando se eliminan.<br /><br /> Dado que otras transacciones no pueden actualizar o eliminar estas filas, la transacción actual evita las lecturas no repetibles. La transacción libera sus bloqueos cuando se confirma o se revierte.|  
|Serializable|La transacción espera hasta que se desbloquean las filas de escritura bloqueadas por otras transacciones. Esto evita que lea los datos "sucios".<br /><br /> La transacción contiene un bloqueo de lectura (si solo Lee filas) o el bloqueo de escritura (si puede actualizar o eliminar filas) en el intervalo de filas al que afecta. Por ejemplo, si la transacción incluye la instrucción SQL **SELECT \* FROM Orders**, el intervalo es toda la tabla Orders; la transacción de lectura bloquea la tabla y no permite que se inserten nuevas filas en ella. Si la transacción incluye la instrucción SQL **Delete de los pedidos en los que status = ' Closed '**, el intervalo es todas las filas con el estado ' Closed '; la transacción de escritura bloquea todas las filas de la tabla Orders con el estado "CLOSED" y no permite que las filas se inserten o actualicen de modo que la fila resultante tenga el estado "CLOSED".<br /><br /> Dado que otras transacciones no pueden actualizar o eliminar las filas del intervalo, la transacción actual evita las lecturas no repetibles. Dado que otras transacciones no pueden insertar filas en el intervalo, la transacción actual evita los fantasmas. La transacción libera su bloqueo cuando se confirma o se revierte.|  
  
 Es importante tener en cuenta que el nivel de aislamiento de transacción no afecta a la capacidad de una transacción para ver sus propios cambios; las transacciones siempre pueden ver los cambios que realicen. Por ejemplo, una transacción puede constar de dos instrucciones **Update** , la primera de las cuales eleva el pago de todos los empleados en un 10 por ciento y la segunda de las cuales establece el pago de los empleados a lo largo de una cantidad máxima. Esto se realiza correctamente como una sola transacción, ya que la segunda instrucción **Update** puede ver los resultados de la primera.
