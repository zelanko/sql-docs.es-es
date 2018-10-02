---
title: Iniciar y detener un agente de replicación (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], stopping
- agents [SQL Server replication], starting
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 846024d9e7a25b1200028872f461a7f5888ac49b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822603"
---
# <a name="start-and-stop-a-replication-agent-sql-server-management-studio"></a>Iniciar y detener un agente de replicación (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede iniciar y detener agentes desde las carpetas **Trabajos** y **Replicación** de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] and from Replicación Monitor. Inicie y detenga los siguientes agentes y trabajos:  
  
-   El Agente de instantáneas, utilizado por todas las publicaciones.  
  
-   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.  
  
-   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
-   El Agente de distribución, que sincroniza las suscripciones con las publicaciones transaccionales y de instantáneas.  
  
-   El Agente de mezcla, que sincroniza las suscripciones con las publicaciones de combinación.  
  
-   Trabajos de mantenimiento de la replicación.  
  
 Para más información sobre cómo iniciar el Agente de mezcla y el Agente de distribución, vea [Sincronizar una suscripción de inserción](../../../relational-databases/replication/synchronize-a-push-subscription.md) y [Sincronizar una suscripción de extracción](../../../relational-databases/replication/synchronize-a-pull-subscription.md). Para más información acerca de los trabajos de mantenimiento, vea [Ejecutar trabajos de mantenimiento de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md).  
  
 Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-start-and-stop-a-snapshot-agent-or-log-reader-agent-from-management-studio"></a>Para iniciar y detener un agente de instantáneas o un agente de registro del LOG desde Management Studio  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor y la carpeta **Replicación** .  
  
2.  Expanda la carpeta **Publicaciones locales** y haga clic con el botón secundario en una publicación.  
  
3.  Haga clic en **Ver estado del Agente de instantáneas** o **Ver estado del Agente de registro del LOG**.  
  
4.  Haga clic en **Iniciar** o **Detener**.  
  
### <a name="to-start-and-stop-a-queue-reader-agent-from-management-studio"></a>Para iniciar y detener un Agente de lectura de cola desde Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic con el botón secundario en el trabajo del agente y, a continuación, haga clic en **Iniciar trabajo** o **Detener trabajo**. El nombre del trabajo del Agente de lectura de cola tiene la forma **[\<Distribuidor>].\<entero>**.  
  
### <a name="to-start-and-stop-a-snapshot-agent-log-reader-agent-or-queue-reader-agent-from-replication-monitor"></a>Para iniciar y detener un agente de instantáneas, un Agente de registro del LOG o un Agente de lectura de cola desde el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic con el botón secundario en un agente y, a continuación, haga clic en **Iniciar agente** o **Detener agente**.  
  
## <a name="see-also"></a>Ver también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replication Agents Overview](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
