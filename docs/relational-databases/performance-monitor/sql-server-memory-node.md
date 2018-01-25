---
title: SQL Server, nodo de memoria | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8e499aec26a962e6d4e70afcdd81bf021b6e0ec
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-memory-node"></a>SQL Server, Nodo de memoria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] El objeto **Memory Node** de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar el uso de memoria de servidor en los nodos NUMA.  
  
## <a name="memory-node-counters"></a>Contadores del Nodo de memoria  
 En esta tabla se describen los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Nodo de memoria** .  
  
|Contadores de Memory Manager de SQL Server|Description|  
|----------------------------------------|-----------------|  
|**Memoria del nodo de base de datos (KB)**|Especifica la cantidad de memoria que el servidor usa actualmente en este nodo para las páginas de base de datos.|  
|**Memoria disponible del nodo libre (KB)**|Especifica la cantidad de memoria que el servidor no utiliza en este nodo.|  
|**Memoria del nodo externa (KB)**|Especifica la cantidad de memoria local que no es NUMA en este nodo.|  
|**Nodo de memoria robada (KB)**|Especifica la cantidad de memoria que el servidor usa en este nodo para otro fin distinto a las páginas de base de datos.|  
|**Memoria del nodo de destino**|Especifica la cantidad de memoria ideal para este nodo.|  
|**Memoria total del nodo**|Indica la cantidad de memoria total que el servidor ha confirmado en este nodo.|  
  
## <a name="see-also"></a>Ver también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Buffer Manager (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
