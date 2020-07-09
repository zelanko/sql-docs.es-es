---
title: Supervisión de la replicación con el Monitor de sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fdeda1e81df8914dee4bdb6303c2dec778bb2ab1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882254"
---
# <a name="monitoring-replication-with-system-monitor"></a>Supervisar la replicación con el Monitor de sistema
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  El Monitor de sistema de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows le permite utilizar gráficos, diagramas e informes para medir la eficacia del equipo, identificar y solucionar posibles problemas (como el uso desequilibrado de recursos, hardware insuficiente o diseño deficiente de programas), y planear necesidades de hardware adicionales. Para obtener más información, vea [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 El Monitor de sistema utiliza objetos y contadores de rendimiento que proporcionan información sobre el rendimiento de diversos procesos. Puede medir el rendimiento de la replicación a través de contadores asociados con los agentes de replicación:  
  
|Agente|Objeto de rendimiento|Contador|Descripción|  
|-----------|------------------------|-------------|-----------------|  
|Todos los agentes|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agentes de replicación|En ejecución|Número de agentes de replicación en ejecución actualmente.|  
|Agente de instantáneas|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantánea de replicación|Instantánea: Comandos entregados/seg.|Número de comandos por segundo entregados al distribuidor.|  
|Agente de instantáneas|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantánea de replicación|Instantánea: Transacciones entregadas/seg.|Número de transacciones por segundo entregadas al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Lector del registro de replicación|Lector del registro: Comandos entregados/seg.|Número de comandos por segundo entregados al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Lector del registro de replicación|Lector del registro: Transacciones entregadas/seg.|Número de transacciones por segundo entregadas al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Lector del registro de replicación|Lector del registro: Latencia de entrega|Tiempo, en milisegundos, que transcurre desde que se aplican las transacciones en el publicador hasta que se entregan al distribuidor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distr. de replicación|Distr.: Comandos entregados/seg.|Número de comandos por segundo entregados al suscriptor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distr. de replicación|Distr.: Transacciones entregadas/seg.|Número de transacciones por segundo entregadas al suscriptor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distr. de replicación|Distr.: Latencia de entrega|Tiempo, en milisegundos, transcurrido desde que las transacciones se entregan al distribuidor hasta que se aplican en el suscriptor.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mezcla de replicación|Conflictos/seg.|Número de conflictos por segundo que ocurren durante el proceso de combinación.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mezcla de replicación|Cambios descargados/seg.|Número de filas replicadas por segundo del publicador al suscriptor.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mezcla de replicación|Cambios cargados/seg.|Número de filas replicadas por segundo del suscriptor al publicador.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar (replicación)](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
