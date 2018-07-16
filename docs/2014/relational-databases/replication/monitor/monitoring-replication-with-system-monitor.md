---
title: Supervisión de la replicación con el Monitor de sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
caps.latest.revision: 29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 396b42a8666ec6c4d775cf06c5a873a012b887ff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37311475"
---
# <a name="monitoring-replication-with-system-monitor"></a>Supervisar la replicación con el Monitor de sistema
  El Monitor de sistema de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows le permite utilizar gráficos, diagramas e informes para medir la eficacia del equipo, identificar y solucionar posibles problemas (como el uso desequilibrado de recursos, hardware insuficiente o diseño deficiente de programas), y planear necesidades de hardware adicionales. Para obtener más información, vea [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 El Monitor de sistema utiliza objetos y contadores de rendimiento que proporcionan información sobre el rendimiento de diversos procesos. Puede medir el rendimiento de la replicación a través de contadores asociados con los agentes de replicación:  
  
|Agente|Objeto de rendimiento|Contador|Descripción|  
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
  
## <a name="see-also"></a>Vea también  
 [Supervisar &#40;replicación&#41;](../monitoring-replication.md)  
  
  
