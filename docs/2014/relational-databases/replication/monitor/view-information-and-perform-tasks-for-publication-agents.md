---
title: Ver información y realizar tareas para los agentes asociados con una publicación (Monitor de replicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a92f56a6a9c68d984323ba8801755f87a1eaaec7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758037"
---
# <a name="view-information-and-perform-tasks-for-the-agents-associated-with-a-publication-replication-monitor"></a>Ver información y realizar tareas para los agentes asociados a una publicación (Monitor de replicación)
  El Monitor de replicación proporciona la pestaña **Agentes** , que incluye información sobre los agentes asociados con la publicación seleccionada. El agente de distribución y el agente de mezcla están asociados con suscripciones. Para más información, vea [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](view-information-and-perform-tasks-for-subscription-agents.md).  
  
 Esta pestaña muestra información de los siguientes agentes:  
  
-   El Agente de instantáneas, utilizado por todas las publicaciones.  
  
-   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.  
  
-   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
 Para ver más información acerca de las opciones de esta pestaña, haga clic en **Ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>Para ver información y realizar tareas para los agentes asociados con una publicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Para ver información sobre los agentes, haga clic en la pestaña **Agentes** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:  
  
    -   Para ver información detallada sobre un agente (por ejemplo, mensajes informativos y mensajes de error), haga clic con el botón secundario en el agente y, a continuación, haga clic en **Ver detalles**.  
  
    -   Para ver información detallada del trabajo que ejecuta el agente (como la programación, los detalles de los pasos del trabajo, etc.), haga clic con el botón secundario en el agente y, a continuación, haga clic en **Propiedades**.  
  
    -   Para administrar perfiles para el agente, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Perfil del agente**. Para más información, vea [Trabajar con perfiles del Agente de replicación](../agents/replication-agent-profiles.md).  
  
    -   Para iniciar un agente que no se está ejecutando, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Iniciar agente**.  
  
    -   Para detener un agente que se está ejecutando, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Detener agente**.  
  
## <a name="see-also"></a>Vea también  
 [Establecer umbrales y advertencias en el Monitor de replicación](set-thresholds-and-warnings-in-replication-monitor.md)   
 [Ver información y realizar tareas para una publicación &#40;Monitor de replicación&#41;](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Administración del Agente de replicación](../agents/replication-agent-administration.md)   
 [Supervisar la replicación](../monitoring-replication.md)  
  
  
