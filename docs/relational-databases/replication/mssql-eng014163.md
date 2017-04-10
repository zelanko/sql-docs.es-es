---
title: "MSSQL_ENG014163 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG014163, error"
ms.assetid: b53dd463-ba36-421e-9745-67c7387e68dd
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG014163
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14163|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Asegúrese de que el agente de mezcla se está ejecutando y cumple con el requisito esperado.|  
  
## Explicación  
 La replicación le permite habilitar advertencias para varias condiciones. Incluye la superación de un período de tiempo específico para sincronizar cambios entre un publicador y suscriptor de mezcla. Se pueden especificar diferentes horas para las conexiones LAN y las de acceso telefónico.  
  
 Al habilitar una advertencia con el Monitor de replicación o [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md), especifique un umbral que determine cuándo se desencadena una advertencia. Cuando se alcanza o se supera un umbral, aparece una advertencia en el Monitor de replicación y se escribe un evento en el registro de eventos de Windows. Alcanzar un umbral también puede desencadenar una alerta del Agente SQL Server. Para obtener más información, consulte [establecer umbrales y advertencias en el Monitor de replicación de](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) y [mediante programación el Monitor de replicación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md).  
  
## Acción del usuario  
 Si una suscripción supera un umbral de duración, debe determinar si hay algún problema de rendimiento en el sistema o si debe ajustarse el umbral. Una vez configurada la replicación, desarrolle una línea base de rendimiento que le permitirá determinar el comportamiento de la replicación con la carga de trabajo habitual de las aplicaciones y la topología. Incluya la duración de sincronización en esta línea base para poder establecer un valor adecuado para el umbral.  
  
 Si el valor del umbral es adecuado, pero está siendo superado, debe determinar dónde se encuentra el cuello de botella en el sistema. Para obtener más información acerca de cómo supervisar y solucionar problemas de rendimiento de la replicación, consulte [Monitor de rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  