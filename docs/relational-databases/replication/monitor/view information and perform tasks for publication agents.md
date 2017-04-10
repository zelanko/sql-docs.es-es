---
title: "Ver informaci&#243;n y realizar tareas para los agentes asociados a una publicaci&#243;n (Monitor de replicaci&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "agentes [replicación de SQL Server], ver información"
  - "ver información de agente de replicación"
  - "agentes [replicación de SQL Server], tareas del Monitor de replicación"
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Ver informaci&#243;n y realizar tareas para los agentes asociados a una publicaci&#243;n (Monitor de replicaci&#243;n)
  El Monitor de replicación proporciona la pestaña **Agentes** , que incluye información sobre los agentes asociados con la publicación seleccionada. El agente de distribución y el agente de mezcla están asociados con suscripciones; Para obtener más información, consulte [Ver información y realizar tareas para los agentes asociados a una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
 Esta pestaña muestra información de los siguientes agentes:  
  
-   El Agente de instantáneas, utilizado por todas las publicaciones.  
  
-   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.  
  
-   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
 Para ver más información acerca de las opciones de esta pestaña, haga clic en **Ayuda** en la barra de menús. Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para ver información y realizar tareas para los agentes asociados con una publicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Para ver información sobre los agentes, haga clic en la pestaña **Agentes** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:  
  
    -   Para ver información detallada sobre un agente (por ejemplo, mensajes informativos y mensajes de error), haga clic en el agente y, a continuación, haga clic en **Ver detalles**.  
  
    -   Para ver información detallada sobre el trabajo que se ejecuta el agente (por ejemplo, la programación, detalles del paso de trabajo etc.), haga clic en el agente y, a continuación, haga clic en **propiedades**.  
  
    -   Para administrar perfiles para el agente, haga clic en el agente y, a continuación, haga clic en **perfil del agente**. Para obtener más información, consulte [trabajar con perfiles de agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
    -   Para iniciar un agente que no se está ejecutando, haga clic en el agente y, a continuación, haga clic en **Iniciar agente**.  
  
    -   Para detener un agente que se ejecuta, haga clic en el agente y, a continuación, haga clic en **Detener agente**.  
  
## Vea también  
 [Establecer umbrales y advertencias en el Monitor de replicación](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [Ver la información y realizar tareas para una publicación & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  