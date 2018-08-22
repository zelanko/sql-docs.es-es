---
title: Recolección de elementos no utilizados de OLTP en memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 940140a7-4785-46fc-8bf4-151435dccd3c
caps.latest.revision: 4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 72a6236e7fed91aeaf7ee946bf3393fb767dd496
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394735"
---
# <a name="in-memory-oltp-garbage-collection"></a>Recolección de elementos no utilizados de OLTP en memoria
  Una fila de datos se considera obsoleta si la eliminó una transacción que ya no está activa. Una fila obsoleta es válida para la recolección de elementos no utilizados. A continuación se indican las características de la recolección de elementos no utilizados de [!INCLUDE[hek_2](../../includes/hek-2-md.md)]:  
  
-   No bloqueante. La recolección de elementos no utilizados se reparte uniformemente en el tiempo y tiene un impacto mínimo sobre la carga de trabajo.  
  
-   Cooperativa. Las transacciones de usuario participan en la recolección de elementos no utilizados con el subproceso principal de recolección de elementos no utilizados.  
  
-   Eficiente. Las transacciones de usuario desvinculan las filas obsoletas de la ruta de acceso (es decir, el índice) que se usa. Esto reduce el trabajo necesario cuando se quita finalmente la fila.  
  
-   Responde. La presión de memoria conduce a una recolección de elementos no utilizados dinámica.  
  
-   Escalable. Tras la confirmación, las transacciones de usuario hacen parte del trabajo de recolección de elementos no utilizados. Cuanta más actividad transaccional hay, más transacciones desvinculan las filas obsoletas.  
  
 La recolección de elementos no utilizados se controla mediante el subproceso principal de recolección de elementos no utilizados. El subproceso principal de recolección de elementos no utilizados se ejecuta cada minuto, o cuando el número de transacciones confirmadas supera un umbral interno. La tarea del recolector de elementos no utilizados es:  
  
-   Identificar las transacciones que han eliminado o actualizado un conjunto de filas y se han confirmado antes que la transacción activa más antigua.  
  
-   Identificar las versiones de fila creadas por estas transacciones antiguas.  
  
-   Agrupar las filas antiguas en una o varias unidades de 16 filas cada una. Esto se hace para distribuir el trabajo del recolector de elementos no utilizados en unidades menores.  
  
-   Mover estas unidades de trabajo a la cola de recolección de elementos no utilizados, una para cada programador. Consulte las vistas de administración dinámica del recolector de elementos no utilizados para obtener detalles: [sys.dm_xtp_gc_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql), [sys.dm_db_xtp_gc_cycle_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql) y [sys.dm_xtp_gc_queue_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql).  
  
 Cuando una transacción de usuario se confirma, identifica todos los elementos en cola asociados al programador en el que se ejecutó y después libera la memoria. Si la cola de recolección de elementos no utilizados del programador está vacía, busca cualquier cola que no esté vacía en el nodo NUMA actual. Si hay poca actividad transaccional y hay presión de memoria, el subproceso principal de recolector de elementos no utilizados puede acceder a las filas de cualquier cola. Si no hay ninguna actividad transaccional después de (por ejemplo) eliminar un gran número de filas y no hay presión de memoria, las filas eliminadas no se recopilarán hasta que no se reanude la actividad transaccional o hasta que haya presión de memoria.  
  
## <a name="see-also"></a>Vea también  
 [Administrar memoria para OLTP en memoria](../../database-engine/managing-memory-for-in-memory-oltp.md)  
  
  
