---
title: "Ver el estado de la suscripci&#243;n y la publicaci&#243;n en el Monitor de replicaci&#243;n | Microsoft Docs"
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
  - "Agente de registro del LOG, supervisar"
  - "Agente de mezcla, supervisar"
  - "Agente de lectura de cola, supervisar"
  - "publicaciones [replicación de SQL Server], ver información"
  - "Agente de instantáneas, supervisar"
  - "Agente de distribución, supervisar"
  - "supervisar rendimiento [replicación de SQL Server], estado de publicación"
  - "supervisar rendimiento [replicación de SQL Server], estado de suscripción"
  - "suscripciones [replicación de SQL Server], ver estado"
  - "Monitor de replicación, estado de publicación y suscripción"
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Ver el estado de la suscripci&#243;n y la publicaci&#243;n en el Monitor de replicaci&#243;n
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se muestra información de estado de las publicaciones y suscripciones:  
  
-   El estado de una publicación está determinado por el estado de prioridad más alto de sus suscripciones. Por ejemplo, si una suscripción a una publicación tiene un error y otra tiene un problema de rendimiento se muestra un estado de error para la publicación.  
  
-   El estado de una suscripción se determina por el estado de los agentes que dan servicio a la suscripción. En la replicación de mezcla, es el Agente de mezcla. En la replicación transaccional, es el Agente de registro del LOG o el Agente de distribución (se muestra el estado de prioridad más alto; el estado también se puede determinar por el Agente de lectura de cola si se utilizan suscripciones de actualización en cola). En la replicación de instantáneas, es el Agente de instantáneas o el Agente de distribución (se muestra el estado de prioridad más alto).  
  
 En las tablas de las siguientes secciones se enumeran los posibles valores de estado de publicaciones y suscripciones. Tres de los valores de estado solamente se muestran si se cumple o supera un umbral:  
  
-   Suscripción expirada  
  
     Este valor de estado se aplica a todos los tipos de replicación. Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Rendimiento crítico  
  
     Este valor de estado se aplica a la replicación transaccional y a la replicación de mezcla. Para obtener más información, consulte [Monitor de rendimiento con el Monitor de replicación](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
-   Mezcla de ejecución prolongada  
  
     Este valor de estado se aplica a la replicación de mezcla. Para obtener más información, consulte [Monitor de rendimiento con el Monitor de replicación](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 Además de los estados de suscripción y publicación, la replicación de mezcla proporciona estadísticas de artículos, que ofrecen información detallada sobre cuánto tiempo tarda en completarse la fase de mezcla, cuanto tiempo se invierte en procesar un artículo determinado, el tipo de conexión de conexión que utiliza un suscriptor y demás información importante. Las estadísticas se muestran en la ventana del Agente de mezcla en el Monitor de replicación. La replicación de instantáneas y transaccional proporciona información detallada sobre el proceso del Agente de distribución.  
  
 **Para ver el estado de la publicación y la suscripción**  
  
-   Monitor de replicación: [Ver información y realizar tareas para una publicación & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md) y [Ver información y realizar tareas para una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
  
 **Para ver información detallada de los agentes**  
  
-   Monitor de replicación: [Ver información y realizar tareas de los agentes asociados con una publicación & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md) y [Ver información y realizar tareas de los agentes asociados con una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Valores del estado de la publicación  
 En la siguiente tabla se muestran los valores de estado de la publicación y sus iconos correspondientes en orden de prioridad.  
  
|Estado|Icono|  
|------------|----------|  
|Error|![Icono de interfaz de usuario: error](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "Icono de interfaz de usuario: error")|  
|Rendimiento crítico|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Reintentando comando con errores|![Icono de interfaz de usuario: reintento del agente de replicación](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "Icono de interfaz de usuario: reintento del agente de replicación")|  
|Aceptar|none|  
  
## Valores de estado de la suscripción  
 En las siguientes tablas se muestran los valores de estado de la suscripción y sus iconos correspondientes en orden de prioridad. Es posible que una suscripción tenga dos Estados al mismo tiempo, como **expiración en breve/expirado** y **reintentando comando con errores**; se muestra el estado de prioridad más alto.  
  
 Los valores de estado **rendimiento crítico**, **expiración en breve/expirado**, y **no inicializado** son advertencias. Cuando se muestra una advertencia, el Monitor de replicación también muestra si se está ejecutando un agente. Por ejemplo, el estado podría ser **En ejecución, Rendimiento crítico**.  
  
### Suscripciones transaccionales  
  
|Estado|Icono|  
|------------|----------|  
|Error|![Icono de interfaz de usuario: error](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "Icono de interfaz de usuario: error")|  
|Rendimiento crítico|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Con expiración en breve/Expirado|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Suscripción no inicializada|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Reintentando comando con errores|![Icono de interfaz de usuario: reintento del agente de replicación](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "Icono de interfaz de usuario: reintento del agente de replicación")|  
|No está en ejecución|![Icono de interfaz de usuario: agente de replicación detenido](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "Icono de interfaz de usuario: agente de replicación detenido")|  
|En ejecución|![Icono de interfaz de usuario: ejecución del agente de replicación](../../../relational-databases/replication/monitor/media/repl-icon-running.png "Icono de interfaz de usuario: ejecución del agente de replicación")|  
  
### Suscripciones de mezcla  
  
|Estado|Icono|  
|------------|----------|  
|Error|![Icono de interfaz de usuario: error](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "Icono de interfaz de usuario: error")|  
|Rendimiento crítico|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Mezcla de ejecución prolongada|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Con expiración en breve/Expirado|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Suscripción no inicializada|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Reintentando comando con errores|![Icono de interfaz de usuario: reintento del agente de replicación](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "Icono de interfaz de usuario: reintento del agente de replicación")|  
|Sincronizando|![Icono de interfaz de usuario: ejecución del agente de replicación](../../../relational-databases/replication/monitor/media/repl-icon-running.png "Icono de interfaz de usuario: ejecución del agente de replicación")|  
|No se están sincronizando|![Icono de interfaz de usuario: agente de replicación detenido](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "Icono de interfaz de usuario: agente de replicación detenido")|  
  
### Suscripciones de instantáneas  
  
|Estado|Icono|  
|------------|----------|  
|Error|![Icono de interfaz de usuario: error](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "Icono de interfaz de usuario: error")|  
|Con expiración en breve/Expirado|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Suscripción no inicializada|![Icono de interfaz de usuario: advertencia](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Icono de interfaz de usuario: advertencia")|  
|Reintentando comando con errores|![Icono de interfaz de usuario: reintento del agente de replicación](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "Icono de interfaz de usuario: reintento del agente de replicación")|  
|Sincronizando|![Icono de interfaz de usuario: ejecución del agente de replicación](../../../relational-databases/replication/monitor/media/repl-icon-running.png "Icono de interfaz de usuario: ejecución del agente de replicación")|  
|No se están sincronizando|![Icono de interfaz de usuario: agente de replicación detenido](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "Icono de interfaz de usuario: agente de replicación detenido")|  
  
## Vea también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  