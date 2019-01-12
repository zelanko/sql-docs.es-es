---
title: Supervisión de la replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e2b3441d98bc9226abce3a49fd28820df6ec99ab
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134305"
---
# <a name="monitoring-replication"></a>Supervisar (replicación)
  Supervisar una topología de replicación es un aspecto importante en la implementación de la replicación. Debido a que la actividad de replicación se distribuye, es fundamental realizar un seguimiento de la actividad y el estado de todos los equipos que participan en la replicación. Para supervisar la replicación se pueden utilizar las siguientes herramientas:  
  
-   Monitor de replicación de[!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]   
  
     El Monitor de replicación es la herramienta más importante para supervisar la replicación, ya que presenta una vista de la actividad de la replicación centrada en el publicador. Para obtener más información, consulte [supervisar el rendimiento con el Monitor de replicación](monitor/monitor-performance-with-replication-monitor.md).  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssManStudioFull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] proporciona acceso al Monitor de replicación. También le permite ver el estado actual y último mensaje registrado por los siguientes agentes y permite iniciar y detener a cada agente: Registro del log, agente de instantáneas, agente de mezcla y agente de distribución. Para más información, consulte [Monitor Replication Agents](monitor/monitor-replication-agents.md).  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] y Replication Management Objects (RMO)  
  
     Ambas interfaces le permiten supervisar todos los tipos de replicación desde el distribuidor. La replicación de mezcla también ofrece la posibilidad de supervisar la replicación desde el suscriptor.  
  
-   Alertas para eventos de agentes de replicación  
  
     La replicación proporciona una serie de alertas predefinidas para los eventos de los agentes de replicación y se pueden crear alertas adicionales si es necesario. Las alertas se pueden utilizar para desencadenar una respuesta automática a un evento y para notificar a un administrador. Para obtener más información, vea [Usar alertas para eventos del Agente de replicación](agents/use-alerts-for-replication-agent-events.md).  
  
-   Monitor de sistema  
  
     El Monitor de sistema puede resultar útil para supervisar el rendimiento, ya que proporciona una serie de contadores para la replicación. Para más información, consulte [Monitoring Replication with System Monitor](monitor/monitoring-replication-with-system-monitor.md).  
  
## <a name="see-also"></a>Vea también  
 [Preguntas más frecuentes sobre la administración de replicación](administration/frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](administration/best-practices-for-replication-administration.md)   

  
  
