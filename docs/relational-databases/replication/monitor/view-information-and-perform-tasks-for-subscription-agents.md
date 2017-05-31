---
title: "Ver información y realizar tareas para agentes de suscripción | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: fbb59d31-2424-4552-9195-0da8d83e755f
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e6d7c3133037182042e365e852d7dc8381705e1c
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="view-information-and-perform-tasks-for-subscription-agents"></a>Ver información y realizar tareas para agentes de suscripción
  El Monitor de replicación proporciona dos pestañas que permiten obtener acceso a información sobre los agentes asociados con una suscripción:  
  
-   **Todas las suscripciones**  
  
     En esta pestaña se muestra información acerca de todas las suscripciones de la publicación seleccionada.  
  
-   **Lista de supervisión de suscripciones**  
  
     En esta pestaña se muestra información acerca de las suscripciones de todas las publicaciones disponibles en el publicador seleccionado que tienen errores, advertencias o un rendimiento insuficiente. Esta pestaña no se muestra en los distribuidores que se ejecutan en versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obtener más información acerca de las opciones de cada pestaña, haga clic en la pestaña en el panel derecho y, a continuación, haga clic en **Ayuda** en la barra de menús. Para obtener información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-all-subscriptions-tab"></a>Para ver información y realizar tareas para los agentes asociados con una suscripción (pestaña Todas las suscripciones)  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Todas las suscripciones** para ver información sobre todas las suscripciones. En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:  
  
    -   Para ver información detallada sobre el agente asociado a una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Ver detalles**. La información detallada incluye: historial del agente y mensajes de error, estadísticas de rendimiento de la replicación transaccional y estadísticas de sincronización de los artículos de la replicación de mezcla.  
  
         Las pestañas de la ventana de detalle que se muestra dependen del tipo de suscripción: en las suscripciones de instantánea, la pestaña es **Historial de Distribuidor a suscriptor**; en las suscripciones transaccionales, las pestañas son **Historial de Publicador a distribuidor**, **Historial de Distribuidor a suscriptor**y **Comandos sin distribuir**; en las suscripciones de mezcla, la pestaña es **Historial de sincronizaciones**.  
  
    -   Para sincronizar una suscripción de inserción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Iniciar sincronización**.  
  
    -   Para reinicializar una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Reinicializar suscripción**.  
  
    -   Para validar una única suscripción de mezcla, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar suscripción**. Para validar todas las suscripciones de una publicación de combinación, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar todas las suscripciones**. Para validar todas las suscripciones de una publicación transaccional, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar suscripciones**.  
  
    -   Para administrar perfiles para el agente, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Perfil del agente**. Para más información, vea [Trabajar con perfiles del Agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-subscription-watch-list-tab"></a>Para ver información y realizar tareas para los agentes asociados con una suscripción (pestaña Lista de supervisión de suscripciones)  
  
1.  Expanda un grupo de publicador en el panel izquierdo y, a continuación, haga clic en un publicador.  
  
2.  Haga clic en la pestaña **Lista de supervisión de suscripciones** para ver información sobre todas las suscripciones. En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:  
  
    -   Para ver información detallada sobre el agente asociado a una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Ver detalles**. La información detallada incluye: historial del agente y mensajes de error, estadísticas de rendimiento de la replicación transaccional y estadísticas de sincronización de los artículos de la replicación de mezcla.  
  
         Las pestañas de la ventana de detalle que se muestra dependen del tipo de suscripción: en las suscripciones de instantánea, la pestaña es **Historial de Distribuidor a suscriptor**; en las suscripciones transaccionales, las pestañas son **Historial de Publicador a distribuidor**, **Historial de Distribuidor a suscriptor**y **Rendimiento**; en las suscripciones de mezcla, la pestaña es **Historial de sincronizaciones**.  
  
    -   Para sincronizar una suscripción de inserción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Iniciar sincronización**.  
  
    -   Para reinicializar una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Reinicializar suscripción**.  
  
    -   Para validar una única suscripción de mezcla, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar suscripción**. Para validar todas las suscripciones de una publicación de combinación, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar todas las suscripciones**. Para validar todas las suscripciones de una publicación transaccional, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar suscripciones**.  
  
    -   Para administrar perfiles para el agente, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Perfil del agente**. Para más información, vea [Trabajar con perfiles del Agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
## <a name="see-also"></a>Vea también  
 [Ver información y realizar tareas para una suscripción &#40;Monitor de replicación&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
