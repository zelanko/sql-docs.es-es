---
title: Niveles de aislamiento de transacciones (ODBC) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298038"
---
# <a name="transaction-isolation-levels-odbc"></a>Niveles de aislamiento de transacción (ODBC)
Los niveles de aislamiento de *transacciones* son una medida de la medida en que el aislamiento de transacciones se realiza correctamente. En particular, los niveles de aislamiento de transacción se definen por la presencia o ausencia de los siguientes fenómenos:  
  
-   **Lecturas sucias** Una *lectura desfasida* se produce cuando una transacción lee datos que aún no se han confirmado. Por ejemplo, supongamos que la transacción 1 actualiza una fila. La transacción 2 lee la fila actualizada antes de que la transacción 1 confirme la actualización. Si la transacción 1 revierte el cambio, la transacción 2 tendrá datos leídos que se considera que nunca han existido.  
  
-   **Lecturas no repetibles** Una *lectura no repetible* se produce cuando una transacción lee la misma fila dos veces, pero obtiene datos diferentes cada vez. Por ejemplo, supongamos que la transacción 1 lee una fila. La transacción 2 actualiza o elimina esa fila y confirma la actualización o eliminación. Si la transacción 1 vuelve a leer la fila, recupera valores de fila diferentes o detecta que la fila se ha eliminado.  
  
-   **Phantoms** Un *fantasma* es una fila que coincide con los criterios de búsqueda pero no se ve inicialmente. Por ejemplo, supongamos que la transacción 1 lee un conjunto de filas que cumplen algunos criterios de búsqueda. La transacción 2 genera una nueva fila (mediante una actualización o una inserción) que coincide con los criterios de búsqueda para la transacción 1. Si la transacción 1 vuelve a ejecutar la instrucción que lee las filas, obtiene un conjunto diferente de filas.  
  
 Los cuatro niveles de aislamiento de transacción (según lo definido por SQL-92) se definen en términos de estos fenómenos. En la tabla siguiente, una "X" marca cada fenómeno que puede ocurrir.  
  
|Nivel de aislamiento de transacción|Lecturas sucias|Lecturas no repetibles|Fantasmas|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Lectura no confirmada|X|X|X|  
|Lectura confirmada|--|X|X|  
|Lectura repetible|--|--|X|  
|Serializable|--|--|--|  
  
 En la tabla siguiente se describen formas sencillas de implementar un DBMS los niveles de aislamiento de transacciones.  
  
> [!IMPORTANT]  
>  La mayoría de los DBMS utilizan esquemas más complejos que estos para aumentar la simultaneidad. Estos ejemplos se proporcionan únicamente con fines ilustrativos. En particular, ODBC no prescribe cómo determinados DBMS aíslan las transacciones entre sí.  
  
|Aislamiento de transacciones|Posible implementación|  
|---------------------------|-----------------------------|  
|Lectura no confirmada|Las transacciones no están aisladas entre sí. Si el DBMS admite otros niveles de aislamiento de transacciones, omite cualquier mecanismo que utilice para implementar esos niveles. Para que no afecten negativamente a otras transacciones, las transacciones que se ejecutan en el nivel Leer no confirmado suelen ser de solo lectura.|  
|Lectura confirmada|La transacción espera hasta que se desbloquean las filas bloqueadas por escritura por otras transacciones; esto le impide leer cualquier dato "sucio".<br /><br /> La transacción contiene un bloqueo de lectura (si solo lee la fila) o un bloqueo de escritura (si actualiza o elimina la fila) en la fila actual para evitar que otras transacciones la actualicen o eliminen. La transacción libera bloqueos de lectura cuando se mueve fuera de la fila actual. Mantiene los bloqueos de escritura hasta que se confirma o se revierte.|  
|Lectura repetible|La transacción espera hasta que se desbloquean las filas bloqueadas por escritura por otras transacciones; esto le impide leer cualquier dato "sucio".<br /><br /> La transacción contiene bloqueos de lectura en todas las filas que devuelve a la aplicación y bloqueos de escritura en todas las filas que inserta, actualiza o elimina. Por ejemplo, si la transacción incluye la instrucción SQL **SELECT \* FROM Orders**, la transacción bloquea las filas a medida que la aplicación las recupera. Si la transacción incluye la instrucción SQL **DELETE FROM Orders WHERE Status ,** la transacción bloquea las filas a medida que las elimina.<br /><br /> Dado que otras transacciones no pueden actualizar o eliminar estas filas, la transacción actual evita las lecturas no repetibles. La transacción libera sus bloqueos cuando se confirma o se revierte.|  
|Serializable|La transacción espera hasta que se desbloquean las filas bloqueadas por escritura por otras transacciones; esto le impide leer cualquier dato "sucio".<br /><br /> La transacción contiene un bloqueo de lectura (si solo lee filas) o un bloqueo de escritura (si puede actualizar o eliminar filas) en el intervalo de filas al que afecta. Por ejemplo, si la transacción incluye la instrucción SQL **SELECT \* FROM Orders**, el intervalo es toda la tabla Orders; la transacción lee la tabla y no permite que se inserten filas nuevas en ella. Si la transacción incluye la instrucción SQL **DELETE FROM Orders WHERE Status ,** el intervalo es todas las filas con el estado "CLOSED"; la transacción de escritura bloquea todas las filas de la tabla Orders con un estado de "CLOSED" y no permite que se inserte ni actualice ninguna fila de modo que la fila resultante tenga un estado de "CERRADO".<br /><br /> Dado que otras transacciones no pueden actualizar o eliminar las filas del intervalo, la transacción actual evita las lecturas no repetibles. Dado que otras transacciones no pueden insertar ninguna fila en el intervalo, la transacción actual evita los fantasmas. La transacción libera su bloqueo cuando se confirma o se revierte.|  
  
 Es importante tener en cuenta que el nivel de aislamiento de transacción no afecta a la capacidad de una transacción para ver sus propios cambios; las transacciones siempre pueden ver los cambios que realicen. Por ejemplo, una transacción puede consistir en dos sentencias **UPDATE,** la primera de las cuales eleva el salario de todos los empleados en un 10 por ciento y la segunda establece el salario de los empleados por encima de algún importe máximo en ese importe. Esto se realiza como una sola transacción solo porque la segunda instrucción **UPDATE** puede ver los resultados de la primera.
