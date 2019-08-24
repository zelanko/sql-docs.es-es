---
title: MSsubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriptions_TSQL
- MSsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriptions system table
ms.assetid: b7e8301d-d115-41f6-8d4f-e0d25f453b25
author: stevestein
ms.author: sstein
ms.openlocfilehash: cf40b3ea8a8984ee711401adfb561ac86fe0a6ea
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000438"
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSsubscriptions** contiene una fila por cada artículo publicado en una suscripción a la que presta servicio el distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|El Id. de la base de datos del publicador.|  
|**publisher_id**|**smallint**|IDENTIFICADOR del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publication_id**|**int**|Id. de la publicación.|  
|**article_id**|**int**|Id. del artículo.|  
|**subscriber_id**|**smallint**|IDENTIFICADOR del suscriptor.|  
|**subscriber_db**|**sysname**|El nombre de la base de datos de suscripciones.|  
|**subscription_type**|**int**|El tipo de suscripción:<br /><br /> **0** = extracción.<br /><br /> **1** = extracción.<br /><br /> **2** = anónimo.|  
|**sync_type**|**tinyint**|Tipo de sincronización:<br /><br /> **1** = automático.<br /><br /> **2** = sin sincronización.|  
|**status**|**tinyint**|El estado de la suscripción:<br /><br /> **0** = inactivo.<br /><br /> **1** = suscrito.<br /><br /> **2** = activo.|  
|**subscription_seqno**|**varbinary (16)**|Número de secuencia de la transacción de instantáneas.|  
|**snapshot_seqno_flag**|**bit**|Indica el origen del número de secuencia de la transacción de instantáneas, donde el valor **1** significa que **subscription_seqno** es el número de secuencia de la instantánea.|  
|**independent_agent**|**bit**|Indica si hay un agente de distribución independiente para esta publicación.|  
|**subscription_time**|**datetime**|Exclusivamente para uso interno.|  
|**loopback_detection**|**bit**|Se aplica a las suscripciones que forman parte de una topología de replicación transaccional bidireccional. La detección de bucles de retorno determina si el Agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor:<br /><br /> **1** = no devuelve.<br /><br /> **0** = devuelve.<br /><br /> Nota: Esta columna solo se admite para la compatibilidad con versiones anteriores con la funcionalidad de replicación [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]bidireccional en. Para las versiones posteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se debe utilizar la replicación punto a punto en su lugar. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|**agent_id**|**int**|Id. del agente.|  
|**update_mode**|**tinyint**|Tipo de actualización.|  
|**publisher_seqno**|**varbinary (16)**|Número de secuencia de la transacción en el publicador de esta suscripción.|  
|**ss_cplt_seqno**|**varbinary (16)**|El número de secuencia utilizado para indicar el término del procesamiento de instantáneas simultáneas.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas &#40;de replicación de TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas &#40;de replicación de TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact &#40;-SQL de sp_helpsubscription&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
