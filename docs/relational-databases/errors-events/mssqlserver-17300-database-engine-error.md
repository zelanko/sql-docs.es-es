---
title: MSSQLSERVER_17300 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3df70ddeff20cc79efd3736b3507a285c2d0b8b6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver17300"></a>MSSQLSERVER_17300
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17300|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PROC_OUT_OF_SYSTASK_SESSIONS|  
|Texto del mensaje|SQL Server no pudo ejecutar una nueva tarea de sistema porque la memoria no es suficiente o porque el número de sesiones configuradas supera el máximo permitido en el servidor. Compruebe que el servidor tiene la memoria necesaria. Utilice sp_configure con la opción 'user connections' para comprobar el número máximo de conexiones de usuario permitido. Utilice sys.dm_exec_sessions para comprobar el número de sesiones actual, incluidos los procesos de usuario.|  
  
## <a name="explanation"></a>Explicación  
Se ha producido un error en un intento de ejecutar una nueva tarea de sistema porque la memoria no es suficiente o porque se ha superado el número de sesiones configuradas en el servidor.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe que el servidor tiene memoria suficiente. Compruebe el número actual de tareas de sistema utilizando sys.dm_exec_sessions, y compruebe el valor configurado de conexiones de usuario máximas utilizando sp_configure.  
  
Realice las siguientes tareas, según corresponda:  
  
-   Agregue más memoria al servidor.  
  
-   Finalice una o más sesiones.  
  
-   Aumente el número máximo de conexiones de usuario permitido en el servidor.  
  
## <a name="see-also"></a>Ver también  
[sp_configure &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
[Opciones de configuración de servidor &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[Establecer la opción de configuración del servidor Conexiones de usuario](~/database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
[KILL &#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md)  
  
