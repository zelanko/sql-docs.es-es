---
title: Sys.dm_broker_forwarded_messages (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_forwarded_messages
- dm_broker_forwarded_messages
- sys.dm_broker_forwarded_messages_TSQL
- dm_broker_forwarded_messages_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_broker_forwarded_messages dynamic management view
ms.assetid: 5576376d-6364-417a-8475-aa770e060845
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c7292ca6344c7492da82c3d65ff4003f23f95f1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmbrokerforwardedmessages-transact-sql"></a>sys.dm_broker_forwarded_messages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada mensaje de Service Broker que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene en proceso de reenvío.  
  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**conversation_id**|**uniqueidentifier**|Id. de la conversación a la que pertenece este mensaje. ACEPTA VALORES NULL.|  
|**is_initiator**|**bit**|Indica si este mensaje es del iniciador de la conversación.  ACEPTA VALORES NULL.<br /><br /> 0 = No es del iniciador.<br /><br /> 1 = Es del iniciador|  
|**to_service_name**|**nvarchar(512)**|Nombre del servicio al que se envía este mensaje. ACEPTA VALORES NULL.|  
|**to_broker_instance**|**nvarchar(512)**|Identificador del agente que hospeda el servicio al que se envía este mensaje. ACEPTA VALORES NULL.|  
|**from_service_name**|**nvarchar(512)**|Nombre del servicio que origina este mensaje. ACEPTA VALORES NULL.|  
|**from_broker_instance**|**nvarchar(512)**|Identificador del agente que hospeda el servicio de donde viene este mensaje. ACEPTA VALORES NULL.|  
|**adjacent_broker_address**|**nvarchar(512)**|Dirección de red a la que se envía este mensaje. ACEPTA VALORES NULL.|  
|**message_sequence_number**|**bigint**|Número de secuencia del mensaje en el cuadro de diálogo. ACEPTA VALORES NULL.|  
|**message_fragment_number**|**int**|Si el mensaje de diálogo está fragmentado, es el número de fragmento que contiene este mensaje de transporte. ACEPTA VALORES NULL.|  
|**hops_remaining**|**tinyint**|Número de veces que se puede retransmitir el mensaje antes de que llegue el destino final. Cada vez que se reenvía el mensaje, este número disminuye en 1. ACEPTA VALORES NULL.|  
|**time_to_live**|**int**|Tiempo máximo en que el mensaje permanece activo. Cuando llega a 0, el mensaje se descarta. ACEPTA VALORES NULL.|  
|**time_consumed**|**int**|Tiempo que el mensaje ha estado activo. Cada vez que se reenvía el mensaje, este número aumenta en el tiempo que ha tardado en reenviarse el mensaje. No acepta valores NULL.|  
|**message_id**|**uniqueidentifier**|Id. del mensaje. ACEPTA VALORES NULL.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

