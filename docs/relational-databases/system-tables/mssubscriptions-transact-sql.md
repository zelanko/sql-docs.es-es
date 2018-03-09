---
title: MSsubscriptions (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsubscriptions_TSQL
- MSsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriptions system table
ms.assetid: b7e8301d-d115-41f6-8d4f-e0d25f453b25
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e37aa7c4c227739fe528abe4a2b067fe51a4ba4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSsubscriptions** tabla contiene una fila por cada artículo publicado en una suscripción que da servicio el distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|El Id. de la base de datos del publicador.|  
|**iddeeditor**|**smallint**|El identificador del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publication_id**|**int**|Id. de la publicación.|  
|**article_id**|**int**|Id. del artículo.|  
|**subscriber_id**|**smallint**|El identificador del suscriptor.|  
|**subscriber_db**|**sysname**|El nombre de la base de datos de suscripción.|  
|**subscription_type**|**int**|El tipo de suscripción:<br /><br /> **0** = inserción.<br /><br /> **1** = extracción.<br /><br /> **2** = anónima.|  
|**sync_type**|**tinyint**|Tipo de sincronización:<br /><br /> **1** = automático.<br /><br /> **2** = sin sincronización.|  
|**status**|**tinyint**|El estado de la suscripción:<br /><br /> **0** = inactivo.<br /><br /> **1** = suscrito.<br /><br /> **2** = activo.|  
|**subscription_seqno**|**varbinary (16)**|Número de secuencia de la transacción de instantáneas.|  
|**snapshot_seqno_flag**|**bit**|Indica que el origen del número de secuencia de transacción de instantánea, donde un valor de **1** significa que **subscription_seqno** es el número de secuencia de instantánea.|  
|**independent_agent**|**bit**|Indica si hay un agente de distribución independiente para esta publicación.|  
|**subscription_time**|**datetime**|Exclusivamente para uso interno.|  
|**argumento loopback_detection**|**bit**|Se aplica a las suscripciones que forman parte de una topología de replicación transaccional bidireccional. La detección de bucles de retorno determina si el Agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor:<br /><br /> **1** = no no volver a enviar.<br /><br /> **0** = las envía.<br /><br /> Nota: Esta columna solo se admite para mantener la compatibilidad con la funcionalidad de replicación bidireccional en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Para las versiones posteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se debe utilizar la replicación punto a punto en su lugar. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|**agent_id**|**int**|Id. del agente.|  
|**update_mode**|**tinyint**|Tipo de actualización.|  
|**publisher_seqno**|**varbinary (16)**|Número de secuencia de la transacción en el publicador de esta suscripción.|  
|**ss_cplt_seqno**|**varbinary (16)**|El número de secuencia utilizado para indicar el término del procesamiento de instantáneas simultáneas.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
