---
title: MSSQL_ENG014150 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014150 error
ms.assetid: c3dd3109-abf3-4b38-a4e9-ef48d0235656
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78a147080f33cb78b4a752d362d6f62c6123cdf9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674363"
---
# <a name="mssqleng014150"></a>MSSQL_ENG014150
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14150|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Replicación-%s: el agente %s se ejecutó correctamente. %s|  
  
## <a name="explanation"></a>Explicación  
 Este mensaje indica que un agente de replicación ha finalizado la ejecución correctamente. La replicación usa los siguientes agentes:  
  
-   Agente de instantáneas. Todas las publicaciones usan este agente.  
  
-   Agente de registro del LOG. Todas las publicaciones transaccionales usan este agente.  
  
-   Agente de lectura de cola. Todas las publicaciones transaccionales habilitadas para las suscripciones de actualización en cola usan este agente.  
  
-   Agente de distribución. Este agente sincroniza las suscripciones a publicaciones transaccionales y publicaciones de instantáneas.  
  
-   Agente de mezcla. Este agente sincroniza las suscripciones a publicaciones de combinación.  
  
-   Trabajos de mantenimiento de la replicación.  
  
## <a name="user-action"></a>Acción del usuario  
 El Agente de registro del LOG, el Agente de lectura de cola y el Agente de distribución se ejecutan normalmente de forma continua, mientras que el resto de agentes se ejecutan normalmente a petición o en función de una programación. Si no espera que un agente haya completado una ejecución, compruebe el estado del agente. Para más información, consulte [Monitor Replication Agents](../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
## <a name="see-also"></a>Ver también  
 [Administración del Agente de replicación](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de distribución de replicación](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente de registro del LOG de replicación](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de mezcla de replicación](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
