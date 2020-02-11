---
title: SQL Server, nodo de memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 32a2296fdb68e640ce8ebfc8dd9cdb351666b337
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250579"
---
# <a name="sql-server-memory-node"></a>SQL Server, Nodo de memoria
  El objeto de **nodo** de memoria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Microsoft proporciona contadores para supervisar el uso de memoria del servidor en los nodos Numa.  
  
## <a name="memory-node-counters"></a>Contadores del Nodo de memoria  
 En esta tabla se describen los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Nodo de memoria** .  
  
|Contadores de Memory Manager de SQL Server|Descripción|  
|----------------------------------------|-----------------|  
|**Memoria de nodo de base de datos (KB)**|Especifica la cantidad de memoria que el servidor usa actualmente en este nodo para las páginas de base de datos.|  
|**Memoria de nodo libre (KB)**|Especifica la cantidad de memoria que el servidor no utiliza en este nodo.|  
|**Memoria de nodo externo (KB)**|Especifica la cantidad de memoria local que no es NUMA en este nodo.|  
|**Nodo de memoria robada (KB)**|Especifica la cantidad de memoria que el servidor usa en este nodo para otro fin distinto a las páginas de base de datos.|  
|**Memoria de nodo de destino**|Especifica la cantidad de memoria ideal para este nodo.|  
|**Memoria total del nodo**|Indica la cantidad de memoria total que el servidor ha confirmado en este nodo.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [Buffer Manager (objeto de SQL Server)](sql-server-buffer-manager-object.md)   
 [Sys. dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
