---
title: Identificar los cuellos de botella | Microsoft Docs
description: Obtenga información sobre las causas de los cuellos de botella, como recursos insuficientes, mal configurados o con un funcionamiento incorrecto en SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 271a005709dc4087ca8d22c7b54f21eebbbfc525
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457677"
---
# <a name="identify-bottlenecks"></a>Identificar los cuellos de botella
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
|Uso de CPU|Un uso excesivo continuo de la CPU puede indicar que las consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] deben optimizarse o que es necesaria una actualización de la CPU.|  
|Entrada/salida (E/S) de disco|[!INCLUDE[tsql](../../includes/tsql-md.md)] consultas se pueden optimizar para reducir la E/S innecesaria; por ejemplo, mediante el uso de índices.|  
|Conexiones de usuario|Puede haber demasiados usuarios obteniendo acceso al servidor de forma simultánea, lo que disminuye el rendimiento.|  
|Bloqueos de cierre|Las aplicaciones diseñadas incorrectamente pueden causar simultaneidad de obstáculos y bloqueos, lo que genera tiempos de respuesta más largos y un menor rendimiento de las transacciones.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de la CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md)   
 [Supervisar el uso del disco](../../relational-databases/performance-monitor/monitor-disk-usage.md)   
 [Supervisar el uso de la memoria](../../relational-databases/performance-monitor/monitor-memory-usage.md)   
 [General Statistics (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)   
 [Locks (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-locks-object.md)  
  
  
