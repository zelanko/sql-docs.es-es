---
title: Supervisión de agentes de replicación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], agents
- Log Reader Agent, monitoring
- Replication Monitor, agents
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- agents [SQL Server replication], monitoring
- Distribution Agent, monitoring
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab277c5ad8d85fdc7c24046bfa191078525fe705
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667133"
---
# <a name="monitor-replication-agents"></a>Supervisar agentes de replicación
  El Monitor de replicación de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona una vista sistémica de la actividad de replicación, aunque también facilita la búsqueda de información sobre un agente concreto. En la siguiente lista se incluye cada agente, las pestañas del Monitor de replicación en las que se puede encontrar y un vínculo a un tema en el que se explica el modo de obtener acceso a dichas pestañas:  
  
-   Los siguientes agentes están asociados con publicaciones en el Monitor de replicación:  
  
    -   Agente de instantáneas  
  
    -   Agente de registro del LOG  
  
    -   Agente de lectura de cola  
  
     Acceda a la información y a las tareas asociadas con estos agentes a través de las pestañas siguientes: **Agentes** (disponible para todos los publicadores y publicaciones) y **Advertencias** (disponible para todas las publicaciones). Para más información, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
-   Los siguientes agentes están asociados con suscripciones en el Monitor de replicación:  
  
    -   Agente de distribución  
  
    -   Agente de mezcla  
  
     Acceda a la información y a las tareas asociadas con estos agentes a través de las pestañas siguientes: **Lista de supervisión de suscripciones** (disponible para todos los publicadores) o la pestaña **Todas las suscripciones** (disponible para todas las publicaciones). Para más información, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="using-sql-server-management-studio-to-monitor-replication-agents"></a>Usar SQL Server Management Studio para supervisar agentes de replicación  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] proporciona los siguientes cuadros de diálogo para supervisar agentes de replicación:  
  
-   **Ver estado del Agente de instantáneas** (para todas las publicaciones)  
  
-   **Ver estado del Agente de registro del LOG** (para todas las publicaciones transaccionales)  
  
-   **Ver estado de sincronización** (para todas las suscripciones; este cuadro de diálogo permite el acceso al Agente de distribución y al Agente de mezcla)  
  
 El Monitor de replicación proporciona información adicional sobre cada agente y ofrece la posibilidad de supervisar al Agente de lectura de cola, si se utiliza. Para más información, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
#### <a name="to-monitor-the-snapshot-agent-and-log-reader-agent"></a>Para supervisar el Agente de instantáneas y el Agente de registro del LOG  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y luego expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic con el botón secundario en una publicación y, a continuación, en **Ver estado del Agente de registro del LOG** o en **Ver estado del Agente de instantáneas**.  
  
4.  En el cuadro de diálogo **Ver estado del Agente de registro del LOG** o **Ver estado del Agente de instantáneas** :  
  
    -   Vea el estado del agente.  
  
    -   Inicie o detenga el agente si fuese necesario.  
  
    -   Haga clic en **Supervisar** para iniciar el **Monitor de replicación**.  
  
5.  Haga clic en **Cerrar**.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-publisher"></a>Para supervisar el Agente de distribución y el Agente de mezcla (en el publicador)  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y luego expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Expanda la publicación de la suscripción que desea supervisar.  
  
4.  Haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Ver estado de sincronización**.  
  
5.  En el cuadro de diálogo **Ver estado de sincronización** :  
  
    -   Vea el estado del agente.  
  
    -   Inicie o detenga el agente si fuese necesario.  
  
    -   Para las suscripciones de inserción, haga clic en **Supervisar** para iniciar el **Monitor de replicación**.  
  
    -   Para las suscripciones de extracción, haga clic en **Ver historial de trabajos** para iniciar el **Visor del archivo de registros**, que muestra información sobre el registro del agente.  
  
6.  Haga clic en **Cerrar**.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-subscriber"></a>Para supervisar el Agente de distribución y el Agente de mezcla (en el suscriptor)  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, la carpeta **Suscripciones locales**.  
  
3.  Haga clic con el botón secundario en la suscripción que desee supervisar y, a continuación, haga clic en **Ver estado de sincronización**.  
  
4.  En el cuadro de diálogo **Ver estado de sincronización** :  
  
    -   Vea el estado del agente.  
  
    -   Inicie o detenga el agente si fuese necesario.  
  
    -   Haga clic en **Ver historial de trabajos** para iniciar el **Visor del archivo de registros**, que muestra información sobre el registro del agente.  
  
5.  Haga clic en **Cerrar**.  
  
## <a name="see-also"></a>Vea también  
 [Monitoring Replication](../monitoring-replication.md)  (Supervisar la replicación)  
 [Información general sobre los agentes de replicación](../agents/replication-agents-overview.md)  
  
  
