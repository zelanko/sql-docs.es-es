---
title: Categoría de eventos Broker | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cab6e66358d16cabb70cd2c371a8f139bd371c99
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="broker-event-category"></a>Broker (categoría de eventos)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La categoría de eventos **Broker** contiene eventos generales de Service Broker.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Broker:Activation (clase de eventos)](../../relational-databases/event-classes/broker-activation-event-class.md)|Evento que se genera cuando un monitor de cola inicia un procedimiento almacenado de activación.|  
|[Broker:Connection (clase de eventos)](../../relational-databases/event-classes/broker-connection-event-class.md)|Evento generado para informar del estado de una conexión de transporte administrada por Service Broker.|  
|[Broker:Conversation (clase de eventos)](../../relational-databases/event-classes/broker-conversation-event-class.md)|Evento generado para informar sobre el progreso de una conversación.|  
|[Broker:Conversation Group (clase de eventos)](../../relational-databases/event-classes/broker-conversation-group-event-class.md)|Evento generado cuando la base de datos crea o quita un grupo de conversación.|  
|[Broker:Corrupted Message (clase de eventos)](../../relational-databases/event-classes/broker-corrupted-message-event-class.md)|Evento que se genera para informar de que la base de datos ha recibido un mensaje dañado.|  
|[Broker:Forwarded Message Dropped (clase de eventos)](../../relational-databases/event-classes/broker-forwarded-message-dropped-event-class.md)|Evento que se genera cuando SQL Server quita un mensaje de Service Broker que tenía que haberse reenviado.|  
|[Broker:Forwarded Message Sent (clase de eventos)](../../relational-databases/event-classes/broker-forwarded-message-sent-event-class.md)|Evento que se genera cuando SQL Server reenvía un mensaje de Service Broker.|  
|[Broker:Message Classify (clase de eventos)](../../relational-databases/event-classes/broker-message-classify-event-class.md)|Evento que se genera cuando Service Broker determina el enrutamiento de un mensaje.|  
|[Broker:Message Drop (clase de eventos)](../../relational-databases/event-classes/broker-message-drop-event-class.md)|Evento que se genera cuando Service Broker no puede retener un mensaje recibido que debería haberse entregado a un servicio de esta instancia.|  
|[Broker:Remote Message Ack (clase de eventos)](../../relational-databases/event-classes/broker-remote-message-ack-event-class.md)|Evento que se genera cuando Service Broker envía o recibe un reconocimiento de mensaje.|  
  
 También se proporcionan dos eventos de auditoría de seguridad para Service Broker. Para obtener más información sobre estos eventos, vea [Clase de eventos Audit Broker Login](../../relational-databases/event-classes/audit-broker-login-event-class.md) y [Audit Broker Conversation (clase de eventos)](../../relational-databases/event-classes/audit-broker-conversation-event-class.md).  
  
## <a name="see-also"></a>Ver también  
 [Auditoría de seguridad (categoría de eventos)](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  
