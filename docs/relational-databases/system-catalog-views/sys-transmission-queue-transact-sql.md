---
title: Sys.transmission_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7bd461a677a7bfab145846baaf09c0a8a62d6f8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022599"
---
# <a name="systransmissionqueue-transact-sql"></a>sys.transmission_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta vista de catálogo contiene una fila por cada mensaje en la cola de transmisión, como se muestra en la tabla siguiente:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|Identificador para la conversación a la que pertenece este mensaje. No acepta valores NULL.|  
|**to_service_name**|**nvarchar(256)**|Nombre del servicio al que se destina este mensaje. QUE ACEPTA VALORES NULL.|  
|**to_broker_instance**|**nvarchar(128)**|Identificador del agente que hospeda el servicio al que se destina este mensaje. QUE ACEPTA VALORES NULL.|  
|**from_service_name**|**nvarchar(256)**|Nombre del servicio que origina este mensaje. QUE ACEPTA VALORES NULL.|  
|**service_contract_name**|**nvarchar(256)**|Nombre del contrato por el que se rige la conversación para este mensaje. QUE ACEPTA VALORES NULL.|  
|**enqueue_time**|**datetime**|Hora en que el mensaje entró en la cola. Este valor utiliza UTC, independientemente de la zona horaria local de la instancia. No acepta valores NULL.|  
|**message_sequence_number**|**bigint**|Número de secuencia del mensaje. No acepta valores NULL.|  
|**message_type_name**|**nvarchar(256)**|Nombre del tipo de mensaje para el mensaje. QUE ACEPTA VALORES NULL.|  
|**is_conversation_error**|**bit**|Indica si este mensaje es un mensaje de error.<br /><br /> 0 = No es un mensaje de error.<br /><br /> 1 = Mensaje de error.<br /><br /> No acepta valores NULL.|  
|**is_end_of_dialog**|**bit**|Indica si este mensaje es un mensaje de final de conversación. No acepta valores NULL.<br /><br /> 0 = No es un mensaje de final de conversación.<br /><br /> 1 = Mensaje de final de conversación.<br /><br /> No acepta valores NULL.|  
|**message_body**|**varbinary(max)**|El cuerpo del mensaje. QUE ACEPTA VALORES NULL.|  
|**transmission_status**|**nvarchar(4000)**|Razón por la que este mensaje está en la cola. Normalmente es un mensaje de error que explica la razón por la que no se ha enviado el mensaje. Si está en blanco, el mensaje no se ha enviado todavía. QUE ACEPTA VALORES NULL.|  
|**priority**|**tinyint**|Nivel de prioridad asignado a este mensaje. No acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
