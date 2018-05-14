---
title: Supervisión de la replicación con el Monitor de sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
caps.latest.revision: 30
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 071539a24627f7bb7ce7cd74580b206ef5cd64a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="monitoring-replication-with-system-monitor"></a>Supervisar la replicación con el Monitor de sistema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Monitor de sistema de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows le permite utilizar gráficos, diagramas e informes para medir la eficacia del equipo, identificar y solucionar posibles problemas (como el uso desequilibrado de recursos, hardware insuficiente o diseño deficiente de programas), y planear necesidades de hardware adicionales. Para obtener más información, vea [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 El Monitor de sistema utiliza objetos y contadores de rendimiento que proporcionan información sobre el rendimiento de diversos procesos. Puede medir el rendimiento de la replicación a través de contadores asociados con los agentes de replicación:  
  
|Agente|Objeto de rendimiento|Contador|Description|  
|-----------|------------------------|-------------|-----------------|  
|Todos los agentes|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Agents|En ejecución|Número de agentes de replicación en ejecución actualmente.|  
|Agente de instantáneas|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Snapshot|Instantánea:Comandos entregados/seg.|Número de comandos por segundo entregados al distribuidor.|  
|Agente de instantáneas|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Snapshot|Instantánea:Transacciones entregadas/seg.|Número de transacciones por segundo entregadas al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Lector del registro:Comandos entregados/seg.|Número de comandos por segundo entregados al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Lector del registro:Transacciones entregadas/seg.|Número de transacciones por segundo entregadas al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Lector del registro:Latencia de entrega|Tiempo, en milisegundos, que transcurre desde que se aplican las transacciones en el publicador hasta que se entregan al distribuidor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist:Comandos entregados/seg.|Número de comandos por segundo entregados al suscriptor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist:Transacciones entregadas/seg.|Número de transacciones por segundo entregadas al suscriptor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist:Latencia de entrega|Tiempo, en milisegundos, transcurrido desde que las transacciones se entregan al distribuidor hasta que se aplican en el suscriptor.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Merge|Conflictos/seg.|Número de conflictos por segundo que ocurren durante el proceso de combinación.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Merge|Cambios descargados/seg.|Número de filas replicadas por segundo del publicador al suscriptor.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Merge|Cambios cargados/seg.|Número de filas replicadas por segundo del suscriptor al publicador.|  
  
## <a name="see-also"></a>Ver también  
 [Supervisar &#40;replicación&#41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
