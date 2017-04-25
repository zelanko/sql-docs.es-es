---
title: "Información del distribuidor, Agentes | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.Distributor.commonjobs..f1
ms.assetid: 5d601a64-6af0-42f9-81b1-cf0087f1c50d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5b1db16b9faf24e2255857203ac4a685d5326ca3
ms.lasthandoff: 04/11/2017

---
# <a name="distributor-information-agents"></a>Información del distribuidor, Agentes
  La pestaña **Agentes** muestra información acerca de los agentes y trabajos de mantenimiento asociados con el publicador y el suscriptor.  
  
 Los agentes que están disponibles en la pestaña **Agentes** de un distribuidor en la vista Distribuidor incluyen todos los agentes que están disponibles en la pestaña **Agentes** de un publicador. Sin embargo, la pestaña **Agentes** para un distribuidor en la vista Distribuidor también incluye un Agente de distribuidor y un Agente de mezcla.  
  
 Para obtener más información acerca de los agentes de instantánea, registro del LOB y de lectura de cola, y de los trabajos del mantenimiento, vea [Publisher Information, Agents](../../relational-databases/replication/publisher-information-agents.md). Observe que cuando está viendo información del agente en la pestaña **Agentes** para un distribuidor, se presenta la información del publicador para los agentes de registro del LOG y de instantánea. Sin embargo, en la pestaña **Agentes** de un distribuidor de la vista Distribuidor, también puede seleccionar **Agente de distribuidor** y **Agente de mezcla**.  
  
## <a name="options"></a>Opciones  
 En las secciones siguientes se describen los datos que se muestran en esta pestaña para el Agente de distribuidor o Agente de mezcla.  
  
### <a name="distributor-agent"></a>Agente de distribuidor  
 **Estado**  
 Estado del agente. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Reintentar  
  
-   En ejecución  
  
-   No está en ejecución  
  
-   No se ha iniciado nunca  
  
 **publicador**  
 La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del publicador.  
  
 **Publicación**  
 Nombre de la publicación a la que está asociada el agente.  
  
 **Suscripción**  
 Nombre de la suscripción, con el formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicación: inserción, extracción o anónima.  
  
 **Última hora de inicio**  
 Última hora en que se inició el agente.  
  
 **Duración**  
 Intervalo de tiempo que se ejecutó el agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
 **Tasa de entrega**  
 La tasa, en comandos por segundo, a la que se confirman los comandos de inicialización en la base de datos de distribución durante la última ejecución del agente.  
  
 **Latencia**  
 El tiempo, en segundos, que ha transcurrido entre el último cambio confirmado en la base de datos de publicación y el comando correspondiente que se confirma en la base de datos de distribución.  
  
 **#Trans**  
 El número de transacciones confirmadas en la base de datos de distribución durante la última ejecución del agente.  
  
 **#Cmds**  
 El número de comandos confirmados en la base de datos de distribución durante la última ejecución del agente. Un comando es lo mismo que un cambio en los datos, como una actualización.  
  
 **Promedio de número de comandos**  
 El promedio de comandos por transacción durante la última ejecución del agente.  
  
### <a name="merge-agent"></a>Agente de mezcla  
 **Estado**  
 Estado del agente. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Reintentar  
  
-   En ejecución  
  
-   No está en ejecución  
  
-   No se ha iniciado nunca  
  
 **publicador**  
 La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del publicador.  
  
 **Publicación**  
 Nombre de la publicación a la que está asociada el agente.  
  
 **Suscripción**  
 Nombre de la suscripción, con el formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicación: inserción, extracción o anónima.  
  
 **Última hora de inicio**  
 Última hora en que se inició el agente.  
  
 **Duración**  
 Intervalo de tiempo que se ejecutó el agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
 **Tasa de entrega**  
 La tasa, en comandos por segundo, a la que se confirman los cambios en la base de datos de distribución.  
  
 **Inserciones de publicador**  
 Número de comandos INSERT aplicados en el publicador.  
  
 **Actualizaciones de publicador**  
 Número de comandos UPDATE aplicados en el publicador.  
  
 **Eliminaciones de publicador**  
 Número de comandos DELETE aplicados en el publicador.  
  
 **Conflictos de publicador**  
 Número de conflictos producidos en el publicador durante el proceso de mezcla.  
  
 **Inserciones de suscriptor**  
 Número de comandos INSERT aplicados en el suscriptor.  
  
 **Actualizaciones de suscriptor**  
 Número de comandos UPDATE aplicados en el suscriptor.  
  
 **Eliminaciones de suscriptor**  
 Número de comandos DELETE aplicados en el suscriptor.  
  
 **Conflictos de suscriptor**  
 Número de conflictos producidos en el suscriptor durante el proceso de mezcla.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Ver información y realizar tareas para un publicador &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
