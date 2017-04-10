---
title: "Suscripci&#243;n, Historial de Publicador a distribuidor (suscripci&#243;n transaccional) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.subscription.pubtodist.tran.f1"
ms.assetid: d5a4c697-1342-49fd-8b7b-b059af32556a
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Suscripci&#243;n, Historial de Publicador a distribuidor (suscripci&#243;n transaccional)
  La pestaña **Historial de Publicador a distribuidor** muestra información detallada en el Agente de registro del LOG, incluidos el estado, el historial y los mensajes informativos, así como cualquier mensaje de error.  
  
## Opciones  
 Seleccione las sesiones del Agente de registro del LOG que se van a ver en el menú **Ver** y, a continuación, seleccione una sesión específica en la cuadrícula con la etiqueta **Sesiones del Agente de registro del LOG**. En la cuadrícula con la etiqueta **Acciones en la sesión seleccionada**se muestra información detallada de la sesión. Si la sesión seleccionada finalizó con un error, también se muestra el área de texto con la etiqueta **Detalles del error o mensaje de la sesión seleccionada** .  
  
 **Ver**  
 Seleccione las sesiones del Agente de registro del LOG que se van a ver. Normalmente, el Agente de registro del LOG se ejecuta sin interrupción, por lo que es posible que solo haya una sesión para ver.  
  
 **Estado**  
 Indica el estado del Agente de registro del LOG. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Completado  
  
-   Intentando de nuevo  
  
-   En ejecución  
  
 **Start Time**  
 Muestra la hora de inicio de la sesión.  
  
 **Hora de finalización**  
 Muestra la hora de finalización de la sesión. Si no se ha detenido el agente, el campo se mostrará vacío.  
  
 **Duración**  
 Período de tiempo durante el que se ha ejecutado el Agente de registro del LOG en esta sesión. El tiempo representa el tiempo transcurrido si el agente se está ejecutando, y el tiempo total de la sesión si la sesión del agente ha finalizado.  
  
 **Mensaje de error**  
 Si una sesión ha finalizado con un error, este campo muestra el último mensaje de error registrado por el Agente de registro del LOG. Si la sesión no ha finalizado con error, el campo se mostrará vacío.  
  
 **Mensaje de la acción**  
 Muestra todos los mensajes informativos y los mensajes de error que ha registrado el Agente de registro del LOG durante la sesión seleccionada.  
  
 **Hora de la acción**  
 La hora a la que la acción descrita en la **mensaje de acción** se realizó la columna.  
  
 **Detalles del error o mensaje de la sesión seleccionada**  
 Muestra solo si la sesión seleccionada presenta un valor de **Error** en la **estado** columna. El área de texto muestra la información detallada del error y el comando que se intentaba ejecutar en el momento de producirse el error. También incluye vínculos a la información adicional relativa al error.  
  
## Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Ver la información y realizar tareas de los agentes asociados con una suscripción & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  