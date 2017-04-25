---
title: "Suscripción, Historial de Distribuidor a suscriptor (Suscripción transaccional) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.subscription.disttosub.f1
ms.assetid: 1aad5b82-592e-4907-92f7-b90794175be5
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e14832b1b0fa335eadd80b65e1d01c727132b53
ms.lasthandoff: 04/11/2017

---
# <a name="subscription-distributor-to-subscriber-history-transactional-subscription"></a>Suscripción, Historial de Distribuidor a suscriptor (Suscripción transaccional)
  La pestaña **Historial de Distribuidor a suscriptor** muestra información detallada sobre el Agente de distribución, incluidos el estado, el historial, los mensajes informativos y cualquier mensaje de error.  
  
## <a name="options"></a>Opciones  
 Seleccione las sesiones del Agente de distribución que desee ver en el menú **Ver** y, a continuación, seleccione una sesión concreta en la cuadrícula etiquetada como **Sesiones del Agente de distribución**. En la cuadrícula con la etiqueta **Acciones en la sesión seleccionada**se muestra información detallada de la sesión. Si la sesión seleccionada finalizó con un error, también se muestra el área de texto con la etiqueta **Detalles del error o mensaje de la sesión seleccionada** .  
  
 **Ver**  
 Seleccione las sesiones del Agente de distribución que desee ver. Normalmente, el Agente de distribución se ejecuta sin interrupción, por lo que es posible que solo haya una sesión para ver.  
  
 **Estado**  
 Estado del Agente de distribución. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Completado  
  
-   Intentando de nuevo  
  
-   En ejecución  
  
 **Start Time**  
 Muestra la hora de inicio de la sesión.  
  
 **Hora de finalización**  
 Muestra la hora de finalización de la sesión. Si no se ha detenido el agente, el campo se mostrará vacío.  
  
 **Duración**  
 Cantidad de tiempo que se ha ejecutado el Agente de distribución en esta sesión. El tiempo representa el tiempo transcurrido si el agente se está ejecutando, y el tiempo total de la sesión si la sesión del agente ha finalizado.  
  
 **Mensaje de error**  
 Si una sesión terminó en error, este campo muestra el último mensaje de error registrado por el Agente de distribución. Si la sesión no ha finalizado con error, el campo se mostrará vacío.  
  
 **Mensaje de la acción**  
 Todos los mensajes informativos y de error que el Agente de distribución ha registrado durante la sesión seleccionada.  
  
 **Hora de la acción**  
 Muestra la hora de realización de la acción descrita en la columna **Mensaje de la acción** .  
  
 **Detalles del error o mensaje de la sesión seleccionada**  
 Solo se muestra si la sesión seleccionada presenta un valor de **Error** en la columna **Estado** . El área de texto muestra la información detallada del error y el comando que se intentaba ejecutar en el momento de producirse el error. También incluye vínculos a la información adicional relativa al error.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
