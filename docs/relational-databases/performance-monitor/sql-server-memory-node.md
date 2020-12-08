---
title: SQL Server, nodo de memoria | Microsoft Docs
description: Obtenga información sobre el objeto Memory Node, que proporciona contadores para supervisar el uso de memoria de servidor en los nodos NUMA en SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 7f1c3f161d59e3bbf08036cc4c15d3380f2484dd
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505634"
---
# <a name="sql-server-memory-node"></a>SQL Server, Nodo de memoria
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El objeto **Nodo de memoria** de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar la utilización de la memoria de servidor en los nodos NUMA.  
  
## <a name="memory-node-counters"></a>Contadores del Nodo de memoria  
 En esta tabla se describen los contadores de **Nodo de memoria** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores de Memory Manager de SQL Server|Descripción|  
|----------------------------------------|-----------------|  
|**Memoria del nodo de base de datos (KB)**|Especifica la cantidad de memoria que el servidor usa actualmente en este nodo para las páginas de base de datos.|  
|**Memoria disponible del nodo libre (KB)**|Especifica la cantidad de memoria que el servidor no utiliza en este nodo.|  
|**Memoria del nodo externa (KB)**|Especifica la cantidad de memoria local que no es NUMA en este nodo.|  
|**Nodo de memoria robada (KB)**|Especifica la cantidad de memoria que el servidor usa en este nodo para otro fin distinto a las páginas de base de datos.|  
|**Memoria del nodo de destino**|Especifica la cantidad de memoria ideal para este nodo.|  
|**Memoria total del nodo**|Indica la cantidad de memoria total que el servidor ha confirmado en este nodo.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Buffer Manager (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
