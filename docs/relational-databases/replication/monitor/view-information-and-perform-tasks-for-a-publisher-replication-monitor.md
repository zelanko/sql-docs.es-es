---
title: "Ver informaci&#243;n y realizar tareas para un publicador (Monitor de replicaci&#243;n) | Microsoft Docs"
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
  - "Publicadores [replicación de SQL Server], tareas del Monitor de replicación"
  - "ver información de publicador"
  - "Publicadores [replicación de SQL Server], ver información"
ms.assetid: 1e777e95-377a-4de3-b965-867464aadaaf
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Ver informaci&#243;n y realizar tareas para un publicador (Monitor de replicaci&#243;n)
  El Monitor de replicación proporciona las siguientes pestañas que muestran información sobre el publicador seleccionado:  
  
-   **Publicaciones**  
  
     En esta pestaña se muestra información sobre todas las publicaciones en el publicador seleccionado.  
  
-   **Lista de supervisión de suscripciones**  
  
     En esta pestaña se muestra información acerca de las suscripciones de todas las publicaciones disponibles en el publicador seleccionado que tienen errores, advertencias o un rendimiento insuficiente. Esta pestaña no se muestra en los distribuidores que se ejecutan en versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   Pestaña**Agentes**   
  
     Esta pestaña muestra información detallada sobre los agentes y trabajos utilizados por todos los tipos de replicación. La pestaña también le permite iniciar y detener cada agente y trabajo.  
  
 Para obtener más información acerca de las opciones de esta pestaña, haga clic en el panel derecho y , a continuación, haga clic en **Ayuda** en la barra de menús. Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para ver información y realizar tareas en un publicador  
  
1.  Expanda un grupo de publicador en el panel izquierdo y, a continuación, haga clic en un publicador.  
  
2.  Para ver información sobre todas las publicaciones, haga clic en la pestaña **Publicaciones** .  
  
3.  Para ver información acerca de las suscripciones, haga clic en la pestaña **Lista de supervisión de suscripciones** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:  
  
    -   Para ver información detallada sobre el agente asociado a una suscripción, haga clic en la suscripción y, a continuación, haga clic en **Ver detalles**.  
  
    -   Para ver las propiedades de una suscripción, haga clic en la suscripción y, a continuación, haga clic en **propiedades**.  
  
    -   Para sincronizar una suscripción de inserción, haga clic en la suscripción y, a continuación, haga clic en **Iniciar sincronización**.  
  
    -   Para reinicializar una suscripción, haga clic en la suscripción y, a continuación, haga clic en **Reinicializar suscripción**.  
  
4.  Para ver información sobre los agentes, haga clic en la pestaña **Agentes** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:  
  
    -   Para ver información detallada sobre un agente (por ejemplo, mensajes informativos y mensajes de error), haga clic en el agente y, a continuación, haga clic en **Ver detalles**.  
  
    -   Para ver información detallada sobre el trabajo que se ejecuta el agente (por ejemplo, la programación, detalles del paso de trabajo etc.), haga clic en el agente y, a continuación, haga clic en **propiedades**.  
  
    -   Para administrar perfiles para el agente, haga clic en el agente y, a continuación, haga clic en **perfil del agente**. Para obtener más información, consulte [trabajar con perfiles de agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
    -   Para iniciar un agente que no se está ejecutando, haga clic en el agente y, a continuación, haga clic en **Iniciar agente**.  
  
    -   Para detener un agente que se ejecuta, haga clic en el agente y, a continuación, haga clic en **Detener agente**.  
  
## Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  