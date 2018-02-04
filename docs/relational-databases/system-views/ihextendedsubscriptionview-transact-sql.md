---
title: IHextendedSubscriptionView (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHextendedSubscriptionView_TSQL
- IHextendedSubscriptionView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedSubscriptionView view
ms.assetid: 124756a4-463a-4a81-bf5b-de7e8ffc7a62
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f938ff6df875bf761b58667b328af223eb3af8ee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHextendedSubscriptionView** vista expone información sobre la suscripción a una publicación no es de SQL Server. Esta vista se almacena en la **distribución** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|El identificador único de un artículo.|  
|**dest_db**|**sysname**|El nombre de la base de datos de destino.|  
|**srvid**|**smallint**|El identificador único de un suscriptor.|  
|**login_name**|**sysname**|El inicio de sesión utilizado para establecer la conexión con un suscriptor.|  
|**distribution_jobid**|**binario**|Identifica el trabajo del Agente de distribución.|  
|**publisher_database_id**|**int**|Identifica la base de datos de publicaciones.|  
|**subscription_type**|**int**|El tipo de suscripción:<br /><br /> **0** = inserción: el agente de distribución se ejecuta en el suscriptor.<br /><br /> **1** = extracción: el agente de distribución se ejecuta en el distribuidor.|  
|**sync_type**|**tinyint**|El tipo de sincronización inicial:<br /><br /> **1** = automático<br /><br /> **2** = ninguno|  
|**status**|**tinyint**|El estado de la suscripción:<br /><br /> **0** = inactivo<br /><br /> **1** = suscrito<br /><br /> **2** = activo|  
|**snapshot_seqno_flag**|**bit**|Indica si se utiliza el número de secuencia de instantánea.|  
|**independent_agent**|**bit**|Especifica si hay un Agente de distribución independiente para esta publicación.<br /><br /> **0** = la publicación utiliza un agente de distribución compartido, y cada par de base de datos de publicador y suscriptor de base de datos tiene un único agente compartido.<br /><br /> **1** = hay un agente de distribución independiente para esta publicación.|  
|**subscription_time**|**datetime**|Exclusivamente para uso interno.|  
|**loopback_detection**|**bit**|Se aplica a las suscripciones que forman parte de una topología de replicación transaccional bidireccional. La detección de bucles de retorno determina si el Agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor:<br /><br /> **1** = no no volver a enviar.<br /><br /> **0** = las envía.|  
|**agent_id**|**int**|El identificador único del Agente de distribución.|  
|**update_mode**|**tinyint**|Indica el tipo del modo de actualización, que puede ser uno de los siguientes:<br /><br /> **0** = solo lectura.<br /><br /> **1** = actualización inmediata.<br /><br /> **2** = actualización en cola mediante Message Queue Server.<br /><br /> **3** = inmediato actualizar con actualización en cola como conmutación por error mediante Message Queue Server.<br /><br /> **4** = actualización en cola mediante cola de SQL Server.<br /><br /> **5** = actualización inmediata con conmutación por error de actualización en cola, mediante cola de SQL Server.|  
|**publisher_seqno**|**varbinary(16)**|Número de secuencia de la transacción en el publicador de esta suscripción.|  
|**ss_cplt_seqno**|**varbinary(16)**|El número de secuencia utilizado para indicar el término del procesamiento de instantáneas simultáneas.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
