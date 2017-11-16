---
title: Identificar los cuellos de botella | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- resource bottlenecks [SQL Server]
- database monitoring [SQL Server], bottlenecks
- performance [SQL Server], bottlenecks
- tuning databases [SQL Server], bottlenecks
- monitoring server performance [SQL Server], bottlenecks
- monitoring performance [SQL Server], bottlenecks
- database performance [SQL Server], bottlenecks
- server performance [SQL Server], bottlenecks
- bottlenecks [SQL Server]
- identifying bottlenecks [SQL Server]
ms.assetid: db079e65-ee80-4105-aec9-f8230d0d6635
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 959d0eb8b722005ae12395ab33730bf478333a42
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="identify-bottlenecks"></a>Identificar los cuellos de botella
  El acceso simultáneo a recursos compartidos causa cuellos de botella. En general, los cuellos de botella están presentes en todos los sistemas de software y son inevitables. Sin embargo, la demanda excesiva de recursos compartidos causa un tiempo de respuesta largo, y debe identificarse y corregirse.  
  
 Entre las causas de estos cuellos de botella se incluyen:  
  
-   Recursos insuficientes que requieren componentes adicionales o actualizados.  
  
-   Recursos del mismo tipo que no distribuyen de forma equilibrada las cargas de trabajo; por ejemplo, cuando un recurso monopoliza un disco.  
  
-   Recursos que funcionan incorrectamente.  
  
-   Recursos mal configurados.  
  
## <a name="analyzing-bottlenecks"></a>Analizar cuellos de botella  
 La duración excesiva de varios eventos es un indicador de cuello de botella que puede corregirse.  
  
 Por ejemplo:  
  
-   Otros componentes pueden evitar que la carga alcance este componente, lo que aumenta el tiempo que se tarda en completar la carga.  
  
-   Las solicitudes de cliente pueden tardar más tiempo debido a una congestión de la red.  
  
 A continuación se indican cinco áreas clave que hay que supervisar para realizar un seguimiento del rendimiento del servidor e identificar cuellos de botella.  
  
|Posible área del cuello de botella|Efectos en el servidor|  
|------------------------------|---------------------------|  
|Uso de la memoria|Si no se asignó o no hay disponible suficiente memoria para Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el rendimiento disminuirá. Los datos se deben leer en el disco, y no directamente en la caché de datos. Los sistemas operativos Microsoft Windows realizan una paginación excesiva intercambiando datos con el disco cuando son necesarias las páginas.|  
|Uso de la CPU|Un uso excesivo continuo de la CPU puede indicar que las consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] deben optimizarse o que es necesaria una actualización de la CPU.|  
|Entrada/salida (E/S) de disco|[!INCLUDE[tsql](../../includes/tsql-md.md)] consultas se pueden optimizar para reducir la E/S innecesaria; por ejemplo, mediante el uso de índices.|  
|Conexiones de usuario|Puede haber demasiados usuarios obteniendo acceso al servidor de forma simultánea, lo que disminuye el rendimiento.|  
|Bloqueos de cierre|Las aplicaciones diseñadas incorrectamente pueden causar simultaneidad de obstáculos y bloqueos, lo que genera tiempos de respuesta más largos y un menor rendimiento de las transacciones.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de la CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md)   
 [Supervisar el uso del disco](../../relational-databases/performance-monitor/monitor-disk-usage.md)   
 [Supervisar el uso de la memoria](../../relational-databases/performance-monitor/monitor-memory-usage.md)   
 [General Statistics (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)   
 [Locks (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-locks-object.md)  
  
  
