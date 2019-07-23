---
title: Supervisión (replicación) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f58fb09416bb6cc800c31dffa47e359d361ccaf7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082970"
---
# <a name="monitoring-replication"></a>Supervisar (replicación)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Supervisar una topología de replicación es un aspecto importante en la implementación de la replicación. Debido a que la actividad de replicación se distribuye, es fundamental realizar un seguimiento de la actividad y el estado de todos los equipos que participan en la replicación. Con el uso de diversas herramientas de supervisión, puede responder a preguntas habituales como: 

-   ¿Es correcto el sistema de replicación?
-   ¿Qué suscripciones son lentas?
-   ¿Cuál es el retraso de la suscripción transaccional?
-   ¿Cuánto tardará una transacción confirmada ahora en llegar al suscriptor en la replicación transaccional?
-   ¿Por qué es lenta la suscripción de mezcla?
-   ¿Por qué no se ejecuta un agente?  
  

Para supervisar la replicación se pueden utilizar las siguientes herramientas:  
  
-   **El Monitor de replicación de SQL Server** es la herramienta más importante para supervisar la replicación, ya que presenta una vista de la actividad de la replicación centrada en el publicador. Para más información, consulte [Monitoring Replication](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md). 
-   **SQL Server Management Studio**: proporciona acceso al Monitor de replicación. También permite ver el estado actual y el último mensaje registrado por los siguientes agentes, además de permitir iniciar y detener cada agente: Agente de registro del LOG, Agente de instantáneas, Agente de mezcla y Agente de distribución. Para más información, consulte [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
-   **Transact-SQL (T-SQL) y Replication Management Objects (RMO)** : las dos interfaces permiten supervisar todos los tipos de replicación del distribuidor. La replicación de mezcla también ofrece la posibilidad de supervisar la replicación desde el suscriptor.  
  
-   **Alertas para los eventos de agente de replicación**: la replicación proporciona una serie de alertas predefinidas para los eventos de los agentes de replicación y se pueden crear alertas adicionales si es necesario. Las alertas se pueden utilizar para desencadenar una respuesta automática a un evento y para notificar a un administrador. Para obtener más información, vea [Usar alertas para eventos del Agente de replicación](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
-   **Monitor de sistema**: puede resultar útil para supervisar el rendimiento, ya que proporciona una serie de contadores para la replicación. Para más información, consulte [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  

## <a name="see-also"></a>Consulte también  
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   

  
  
