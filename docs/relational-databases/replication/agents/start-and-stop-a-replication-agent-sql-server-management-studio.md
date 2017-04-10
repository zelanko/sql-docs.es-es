---
title: "Iniciar y detener un agente de replicaci&#243;n (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "agentes [replicación de SQL Server], detener"
  - "agentes [replicación de SQL Server], iniciar"
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Iniciar y detener un agente de replicaci&#243;n (SQL Server Management Studio)
  Puede iniciar y detener agentes desde las carpetas **Trabajos** y **Replicación** de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] and from Replicación Monitor. Inicie y detenga los siguientes agentes y trabajos:  
  
-   El Agente de instantáneas, utilizado por todas las publicaciones.  
  
-   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.  
  
-   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
-   El Agente de distribución, que sincroniza las suscripciones con las publicaciones transaccionales y de instantáneas.  
  
-   El Agente de mezcla, que sincroniza las suscripciones con las publicaciones de combinación.  
  
-   Trabajos de mantenimiento de la replicación.  
  
 Para obtener más información acerca de cómo iniciar el agente de mezcla y el agente de distribución, consulte [sincronizar una suscripción de inserción](../../../relational-databases/replication/synchronize-a-push-subscription.md) y [sincronizar una suscripción de extracción](../../../relational-databases/replication/synchronize-a-pull-subscription.md). Para obtener más información acerca de los trabajos de mantenimiento, consulte [Ejecutar trabajos de mantenimiento de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md).  
  
 Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para iniciar y detener un agente de instantáneas o un agente de registro del LOG desde Management Studio  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor y la carpeta **Replicación** .  
  
2.  Expanda el **publicaciones locales** carpeta y, a continuación, haga una publicación.  
  
3.  Haga clic en **Ver estado del Agente de instantáneas** o **Ver estado del Agente de registro del LOG**.  
  
4.  Haga clic en **Iniciar** o **Detener**.  
  
### Para iniciar y detener un Agente de lectura de cola desde Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic en el trabajo del agente y, a continuación, haga clic en **Iniciar trabajo** o **Detener trabajo**. Es el nombre del trabajo para el agente de lector de cola en el formulario **[\< distribuidor>]. \< entero>**.  
  
### Para iniciar y detener un agente de instantáneas, un Agente de registro del LOG o un Agente de lectura de cola desde el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic en un agente y, a continuación, haga clic en **Iniciar agente** o **Detener agente**.  
  
## Vea también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Información general sobre los agentes de replicación](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  