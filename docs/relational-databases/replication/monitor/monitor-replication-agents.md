---
title: "Supervisar agentes de replicaci&#243;n | Microsoft Docs"
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
  - "supervisar rendimiento [replicación de SQL Server], agentes"
  - "Agente de registro del LOG, supervisar"
  - "Monitor de replicación, agentes"
  - "Agente de mezcla, supervisar"
  - "Agente de lectura de cola, supervisar"
  - "Agente de instantáneas, supervisar"
  - "agentes [replicación de SQL Server], supervisar"
  - "Agente de distribución, supervisar"
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Supervisar agentes de replicaci&#243;n
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona una vista sistémica de la actividad de replicación, aunque también facilita la búsqueda de información sobre un agente concreto. En la siguiente lista se incluye cada agente, las pestañas del Monitor de replicación en las que se puede encontrar y un vínculo a un tema en el que se explica el modo de obtener acceso a dichas pestañas:  
  
-   Los siguientes agentes están asociados con publicaciones en el Monitor de replicación:  
  
    -   Agente de instantáneas  
  
    -   Agente de registro del LOG  
  
    -   Agente de lectura de cola  
  
     Acceso a información y tareas asociadas a estos agentes a través de las siguientes fichas: **agentes** (disponible para todos los publicadores y publicaciones) y **advertencias** (disponible para cada publicación). Para obtener más información, consulte [Ver información y realizar tareas para los agentes asociados con una publicación & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
-   Los siguientes agentes están asociados con suscripciones en el Monitor de replicación:  
  
    -   Agente de distribución  
  
    -   Agente de mezcla  
  
     Acceso a información y tareas asociadas a estos agentes a través de las siguientes fichas: **lista de observación de suscripción** (disponible para cada publicador) o la **todas las suscripciones** (disponible para cada publicación). Para obtener más información, consulte [Ver información y realizar tareas para los agentes asociados a una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Usar SQL Server Management Studio para supervisar agentes de replicación  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] proporciona los siguientes cuadros de diálogo para supervisar agentes de replicación:  
  
-   **Ver estado del agente de instantáneas** (para todas las publicaciones)  
  
-   **Ver estado del agente de lector de registro** (para todas las publicaciones transaccionales)  
  
-   **Ver estado de sincronización** (para todas las suscripciones; este cuadro de diálogo permite el acceso para el agente de distribución y el agente de mezcla)  
  
 El Monitor de replicación proporciona información adicional sobre cada agente y ofrece la posibilidad de supervisar al Agente de lectura de cola, si se utiliza. Para obtener más información, consulte [Ver información y realizar tareas para los agentes asociados con una publicación & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), [Ver información y realizar tareas de los agentes asociados con una publicación & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), y [Ver información y realizar tareas de los agentes asociados con una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
#### Para supervisar el Agente de instantáneas y el Agente de registro del LOG  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic en una publicación y, a continuación, haga clic en **Ver estado del agente de registro** o **Ver estado del agente de instantáneas**.  
  
4.  En el cuadro de diálogo **Ver estado del Agente de registro del LOG** o **Ver estado del Agente de instantáneas** :  
  
    -   Vea el estado del agente.  
  
    -   Inicie o detenga el agente si fuese necesario.  
  
    -   Haga clic en **Supervisar** para iniciar el **Monitor de replicación**.  
  
5.  Haga clic en **Cerrar**.  
  
#### Para supervisar el Agente de distribución y el Agente de mezcla (en el publicador)  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Expanda la publicación de la suscripción que desea supervisar.  
  
4.  Haga clic en la suscripción y, a continuación, haga clic en **Ver estado de sincronización**.  
  
5.  En el cuadro de diálogo **Ver estado de sincronización** :  
  
    -   Vea el estado del agente.  
  
    -   Inicie o detenga el agente si fuese necesario.  
  
    -   Para las suscripciones de inserción, haga clic en **Supervisar** para iniciar el **Monitor de replicación**.  
  
    -   Para las suscripciones de extracción, haga clic en **Ver historial de trabajos** para iniciar el **Visor del archivo de registros**, que muestra información sobre el registro del agente.  
  
6.  Haga clic en **Cerrar**.  
  
#### Para supervisar el Agente de distribución y el Agente de mezcla (en el suscriptor)  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Suscripciones locales** .  
  
3.  Haga clic en la suscripción que desea supervisar y, a continuación, haga clic en **Ver estado de sincronización**.  
  
4.  En el cuadro de diálogo **Ver estado de sincronización** :  
  
    -   Vea el estado del agente.  
  
    -   Inicie o detenga el agente si fuese necesario.  
  
    -   Haga clic en **Ver historial de trabajos** para iniciar el **Visor del archivo de registros**, que muestra información sobre el registro del agente.  
  
5.  Haga clic en **Cerrar**.  
  
## Vea también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Información general sobre los agentes de replicación](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  