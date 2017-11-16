---
title: "Ver información y realizar tareas para una publicación (Monitor de replicación) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3cc21b75d345df304fd84514e62e609866ccced0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="view-information-and-perform-tasks-for-a-publication-replication-monitor"></a>Ver información y realizar tareas para una publicación (Monitor de replicación)
  El Monitor de replicación proporciona las siguientes pestañas con información acerca de la publicación seleccionada:  
  
-   **Todas las suscripciones**  
  
     En esta pestaña se muestra información acerca de todas las suscripciones de la publicación seleccionada.  
  
-   **Agentes**  
  
     En esta pestaña se muestra información sobre todos los agentes utilizados por una replicación.  
  
    -   El Agente de instantáneas, utilizado por todas las publicaciones.  
  
    -   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.  
  
    -   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola.  
  
-   **Advertencias** (para distribuidores que ejecutan [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores)  
  
    -   Esta pestaña permite especificar advertencias y alertas para agentes.  
  
-   **Testigos de seguimiento** (solo replicación transaccional, para distribuidores que ejecuten [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores)  
  
     Esta pestaña permite medir la latencia, es decir, el tiempo que transcurre entre la confirmación de una transacción en el publicador y la confirmación de la transacción correspondiente en el suscriptor.  
  
 Para obtener más información acerca de las opciones de cada pestaña, haga clic en la pestaña en el panel derecho y, a continuación, haga clic en **Ayuda** en la barra de menús. Para obtener información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-a-publication"></a>Para ver información y realizar tareas para una publicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Para ver y modificar las propiedades de una publicación, haga clic con el botón secundario en la publicación y, a continuación, haga clic en **Propiedades**.  
  
3.  Para ver información acerca de las suscripciones, haga clic en la pestaña **Todas las suscripciones** .  
  
     Para ver y modificar las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**. En esta pestaña, también puede realizar tareas y tener acceso a información más detallada. Para más información, vea [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
4.  Para ver información sobre los agentes, haga clic en la pestaña **Agentes** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada. Para más información, vea [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
5.  Para ver información sobre las advertencias del agente y umbrales, haga clic en la pestaña **Advertencias** . Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
6.  Para ver información acerca de los token de seguimiento, haga clic en la pestaña **Token de seguimiento** . Para obtener más información acerca de cómo utilizar los testigos de seguimiento, vea [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
