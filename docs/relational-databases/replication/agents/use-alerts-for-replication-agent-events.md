---
title: "Usar alertas para eventos del Agente de replicaci&#243;n | Microsoft Docs"
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
  - "ver alertas"
  - "Agente de lectura de cola, alertas"
  - "alertas [replicación de SQL Server]"
  - "alertas de replicación predefinidas [replicación de SQL Server]"
  - "Agente de registro de cola, alertas"
  - "Agente de distribución, alertas"
  - "Agente de mezcla, alertas"
  - "agentes [replicación de SQL Server], alertas"
  - "mostrar alertas"
  - "Agente de instantáneas, alertas"
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Usar alertas para eventos del Agente de replicaci&#243;n
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y el Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporcionan un modo de supervisar eventos, tales como eventos de Agente de replicación, mediante alertas. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supervisa el registro de aplicación de Windows en busca de eventos que se asocian con alertas. Si se produce uno de esos eventos, el Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] responde automáticamente, mediante la ejecución de una tarea que haya sido definida y/o el envío de un mensaje de correo electrónico o de buscapersonas a un operador especificado. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluye un conjunto de alertas predefinidas para los agentes de replicación que se pueden configurar para ejecutar una tarea o notificar a un operador. Para obtener más información sobre cómo definir la ejecución de una tarea, vea la sección "Automatizar la respuesta a una alerta" en este tema.  
  
 Las siguientes alertas se instalan cuando un equipo se configura como distribuidor:  
  
|Id. del mensaje|Alerta predefinida|Condición que desencadena la alerta|Especifica información adicional en msdb..sysreplicationalerts|  
|----------------|----------------------|-----------------------------------------|-----------------------------------------------------------------|  
|14150|**Replicación: éxito de agente**|Un agente termina correctamente.|Sí|  
|14151|**Replicación: error de agente**|Un agente termina con un error.|Sí|  
|14152|**Replicación: reintento de agente**|El agente termina después de volver a intentar sin éxito una operación (el agente encuentra un error, por ejemplo que el servidor no está disponible, interbloqueo, error en la conexión o error de tiempo de espera).|Sí|  
|14157|**Replicación: suscripción expirada quitada**|Se quitó la suscripción expirada.|No|  
|20572|**Replicación: Suscripción reinicializada por no pasar la validación**|El trabajo de respuesta "Reinicializar suscripciones con errores de validación de datos" reinicializa correctamente una suscripción.|No|  
|20574|**Replicación: el suscriptor no ha superado la validación de datos**|Un agente de distribución o de mezcla no puede validar los datos.|Sí|  
|20575|**Replicación: El suscriptor ha pasado la validación de datos**|Un agente de distribución o de mezcla pasa la validación de los datos.|Sí|  
|20578|**Replicación: cierre personalizado del agente**|||  
|22815|**Alerta de detección de conflictos punto a punto**|El Agente de distribución detecta un conflicto cuando intenta aplicar un cambio en un nodo punto a punto.|Sí|  
  
 Además de estas alertas, el Monitor de replicación proporciona una serie de advertencias y alertas relacionadas con el estado y el rendimiento. Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). También puede definir alertas para otros eventos de replicación con la infraestructura de alertas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [crear un evento definido por el usuario](../../../ssms/agent/create-a-user-defined-event.md).  
  
 **Para configurar las alertas de replicación predefinidas**  
  
-   [! INCLUIR [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [Configure Predefined Replication Alerts &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## Ver directamente el registro de aplicación  
 Para ver el registro de aplicación Windows, utilice el Visor de eventos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. El registro de aplicación contiene mensajes de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] así como mensajes de muchas otras actividades del equipo. A diferencia del registro de errores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], no se crea un nuevo registro de aplicación cada vez que se inicia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (cada sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] escribe nuevos eventos en un registro de aplicación existente); no obstante, puede especificar durante cuánto tiempo desea mantener los eventos registrados. Al ver un registro de aplicación Windows, puede filtrar el registro en busca de eventos específicos. Para obtener más información, consulte la documentación de Windows.  
  
## Automatizar la respuesta a una alerta  
 La replicación proporciona un trabajo de respuesta para las suscripciones que no pueden validar los datos y también proporciona un marco de trabajo para la creación de respuestas automatizadas adicionales a las alertas. El trabajo de respuesta se llama **Reinicializar suscripciones con errores de validación de datos** y se almacena en la carpeta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Trabajos **del Agente** en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obtener información acerca de cómo habilitar este trabajo de respuesta, consulte [Configurar alertas de replicación predefinidas & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md). Si se produce un error en la validación de los artículos de una publicación transacional, el trabajo de respuesta reinicializa únicamente aquellos artículos que no se hayan validado. Si se produce un error en la validación de los artículos de una publicación de combinación, el trabajo de respuesta reinicializa todos los artículos de la publicación.  
  
### Marco de trabajo para la automatización de respuestas  
 Normalmente, cuando se produce una alerta, la única información de que dispone para comprender qué la ha provocado y la acción más apropiada que puede llevar a cabo está contenida en el propio mensaje de la alerta. El análisis de esta información puede estar sujeta a errores y lleva mucho tiempo. La replicación facilita la automatización de respuestas al proporcionar información adicional sobre la alerta en la tabla del sistema **sysreplicationalerts** ; la información que se proporciona ya está analizada de una forma que los programas personalizados pueden utilizar fácilmente.  
  
 Por ejemplo, si se produce un error al validar los datos de la tabla **Sales.SalesOrderHeader** en el suscriptor A, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede desencadenar el mensaje 20574, que le notifica dicho error. El mensaje que reciba será: "La suscripción del suscriptor 'A' al artículo 'SalesOrderHeader' de la publicación 'MyPublication', no pasó la validación de datos."  
  
 Si crea un trabajo de respuesta basado en el mensaje, debe analizar manualmente el nombre del suscriptor, el nombre del artículo, el nombre de la publicación y el error del mensaje. Sin embargo, dado que el agente de distribución y el agente de mezcla escriben la misma información para **sysreplicationalerts** (junto con detalles como el tipo de agente, la hora de la alerta, la base de datos de publicación, la base de datos de suscriptor y el tipo de publicación), el trabajo de respuesta puede consultar directamente la información pertinente de la tabla. Aunque la fila exacta no puede asociarse con una instancia específica de la alerta, la tabla tiene una columna **status** que se puede utilizar para realizar un seguimiento de las entradas atendidas. Las entradas de esta tabla se mantienen durante el período de retención del historial.  
  
 Por ejemplo, si creara un trabajo de respuesta en [!INCLUDE[tsql](../../../includes/tsql-md.md)] para dar servicio al mensaje de alerta 20574, podría utilizar la lógica siguiente:  
  
```  
declare @publisher sysname, @publisher_db sysname, @publication sysname, @publication_type int, @article sysname, @subscriber sysname, @subscriber_db sysname, @alert_id int  
declare hc cursor local for select publisher, publisher_db, publication, publication_type, article, subscriber,   
  subscriber_db, alert_id from   
  msdb..sysreplicationalerts where  
  alert_error_code = 20574 and status = 0  
  for read only  
open hc  
fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
while (@@fetch_status <> -1)  
begin  
/* Do custom work  */  
/* Update status to 1, which means the alert has been serviced. This prevents subsequent runs of this job from doing this again */  
update msdb..sysreplicationalerts set status = 1 where alert_id = @alert_id  
 fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
end  
close hc  
deallocate hc  
```  
  
## Vea también  
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Prácticas recomendadas para la administración de replicación](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [La supervisión de & #40; Replicación y nº 41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  