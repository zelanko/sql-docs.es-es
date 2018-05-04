---
title: Sys.transmission_queue (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- transmission_queue
- sys.transmission_queue_TSQL
- sys.transmission_queue
- transmission_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.transmission_queue catalog view
ms.assetid: f3515d1a-be8f-4a27-8058-8865f0919838
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9dce78af7983d26f286860259911ac3bbd91f668
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="systransmissionqueue-transact-sql"></a>sys.transmission_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta vista de catálogo contiene una fila por cada mensaje en la cola de transmisión, como se muestra en la tabla siguiente:  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|Identificador para la conversación a la que pertenece este mensaje. No acepta valores NULL.|  
|**to_service_name**|**nvarchar(256)**|Nombre del servicio al que se destina este mensaje. ACEPTA VALORES NULL.|  
|**to_broker_instance**|**nvarchar(128)**|Identificador del agente que hospeda el servicio al que se destina este mensaje. ACEPTA VALORES NULL.|  
|**from_service_name**|**nvarchar(256)**|Nombre del servicio que origina este mensaje. ACEPTA VALORES NULL.|  
|**service_contract_name**|**nvarchar(256)**|Nombre del contrato por el que se rige la conversación para este mensaje. ACEPTA VALORES NULL.|  
|**enqueue_time**|**datetime**|Hora en que el mensaje entró en la cola. Este valor utiliza UTC, independientemente de la zona horaria local de la instancia. No acepta valores NULL.|  
|**message_sequence_number**|**bigint**|Número de secuencia del mensaje. No acepta valores NULL.|  
|**message_type_name**|**nvarchar(256)**|Nombre de tipo de mensaje para el mensaje. ACEPTA VALORES NULL.|  
|**is_conversation_error**|**bit**|Indica si este mensaje es un mensaje de error.<br /><br /> 0 = No es un mensaje de error.<br /><br /> 1 = Mensaje de error.<br /><br /> No acepta valores NULL.|  
|**is_end_of_dialog**|**bit**|Indica si este mensaje es un mensaje de final de conversación. No acepta valores NULL.<br /><br /> 0 = No es un mensaje de final de conversación.<br /><br /> 1 = Mensaje de final de conversación.<br /><br /> No acepta valores NULL.|  
|**message_body**|**varbinary(max)**|El cuerpo de este mensaje. ACEPTA VALORES NULL.|  
|**transmission_status**|**nvarchar(4000)**|Razón por la que este mensaje está en la cola. Normalmente es un mensaje de error que explica la razón por la que no se ha enviado el mensaje. Si está en blanco, el mensaje no se ha enviado todavía. ACEPTA VALORES NULL.|  
|**priority**|**tinyint**|Nivel de prioridad asignado a este mensaje. No acepta valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
