---
title: MSreplication_monitordata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 898990152a86380ae9ba28e9766ae47675a39706
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775537"
---
# <a name="msreplicationmonitordata-transact-sql"></a>MSreplication_monitordata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSreplication_monitordata** tabla contiene datos almacenados en caché utilizados por el Monitor de replicación, con una fila por cada suscripción supervisada. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**lastrefresh**|**datetime**|La fecha y la hora a las que se actualizaron los datos del monitor.|  
|**computeTime**|**int**|El tiempo (en segundos) que se tardó en calcular los datos del monitor.|  
|**publication_id**|**int**|El Id. de la publicación.|  
|**publicador**|**sysname**|El nombre del publicador.|  
|**publisher_srvid**|**int**|El Id. del servidor del publicador.|  
|**publisher_db**|**sysname**|El nombre de la base de datos de publicación.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**publication_type**|**int**|El tipo de publicación; puede ser uno de estos valores:<br /><br /> **0** = publicación transaccional<br /><br /> **1** = publicación de instantáneas<br /><br /> **2** = publicación de combinación|  
|**agent_type**|**int**|El tipo de agente de replicación; puede ser uno de estos valores:<br /><br /> **1** = agente de instantáneas<br /><br /> **2** = Agente lector del registro<br /><br /> **3** = agente de distribución<br /><br /> **4** = agente de mezcla<br /><br /> **9** = agente de lector de cola|  
|**valor de agent_id**|**int**|El Id. del agente de replicación.|  
|**agent_name**|**sysname**|El nombre del trabajo del agente de replicación.|  
|**job_id**|**uniqueidentifier**|El GUID del trabajo del agente de replicación.|  
|**status**|**int**|El estado del agente de replicación; puede ser uno de estos valores:<br /><br /> **1** = iniciado<br /><br /> **2** = se ha realizado correctamente<br /><br /> **3** = en curso<br /><br /> **4** = inactivo<br /><br /> **5** = reintentando<br /><br /> **6** = error|  
|**isagentrunningnow**|**bit**|Una marca que indica si el trabajo del agente se está ejecutando, el valor **1** significa que se ejecuta el trabajo.|  
|**Advertencia**|**int**|Advertencia de umbral generada por una suscripción; puede ser el resultado OR lógico de uno o más de estos valores.<br /><br /> **1** = expiration: una suscripción a una publicación transaccional ha superado el período de retención por encima del umbral permitido, como un porcentaje del período de retención.<br /><br /> **2** = latency: el tiempo necesario para replicar datos desde un publicador transaccional al suscriptor supera el umbral, en segundos.<br /><br /> **4** = mergeexpiration: una suscripción a una publicación de combinación ha superado el período de retención por encima del umbral permitido, como un porcentaje del período de retención. 8 = mergefastrunduration. El tiempo que se tarda en finalizar la sincronización de una suscripción de mezcla sobrepasa el umbral, en segundos, en una conexión de red rápida.<br /><br /> **16** = mergeslowrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red lenta o telefónico.<br /><br /> **32** = mergefastrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, a través de una conexión de red rápida.<br /><br /> **64** = mergeslowrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, a través de una conexión de red lenta o telefónico.|  
|**last_distsync**|**datetime**|La fecha y la hora a las que se ejecutó por última vez el Agente de distribución.|  
|**agentstoptime**|**datetime**|La fecha y la hora a las que se detuvo el agente.|  
|**distdb**|**sysname**|El nombre de la base de datos de distribución para la suscripción.|  
|**retención**|**int**|El período de retención para la publicación.|  
|**time_stamp**|**datetime**|Solo para uso interno.|  
|**worst_latency**|**int**|La mayor latencia, en segundos, para los cambios de datos propagados por los agentes de distribución o de registro del LOG para una publicación transaccional.|  
|**best_latency**|**int**|La menor latencia, en segundos, para los cambios de datos propagados por los agentes de distribución o de registro del LOG para una publicación transaccional.|  
|**avg_latency**|**int**|La latencia promedio, en segundos, para los cambios de datos propagados por los agentes de distribución o de registro del LOG para una publicación transaccional.|  
|**cur_latency**|**int**|La latencia, en segundos, para los cambios de datos propagados por los agentes de distribución o de registro del LOG durante la ejecución actual.|  
|**worst_runspeedPerf**|**int**|El mayor tiempo de sincronización de la publicación de combinación|  
|**best_runspeedPerf**|**int**|El menor tiempo de sincronización de la publicación de combinación|  
|**average_runspeedPerf**|**int**|El tiempo promedio de sincronización de la publicación de combinación|  
|**mergePerformance**|**int**|Rendimiento de la última sincronización con respecto a todas las sincronizaciones de la suscripción. Se basa en la tasa de entrega de la última sincronización dividida entre la media de todas las tasas de entrega anteriores.|  
|**mergelatestsessionrunduration**|**int**|La duración de la ejecución más reciente del Agente de mezcla.|  
|**mergelatestsessionrunspeed**|**float(53)**|La velocidad de entrega de la ejecución más reciente del Agente de mezcla.|  
|**mergelatestsessionconnectiontype**|**int**|La conexión utilizada para la sesión más reciente del Agente de mezcla; puede ser uno de los siguientes valores:<br /><br /> **1** = red de área local (LAN)<br /><br /> **2** = conexión de red de acceso telefónico|  
|**retention_period_unit**|**tinyint**|Define la unidad utilizada al definir la retención; puede ser uno de estos valores:<br /><br /> **1** = semana<br /><br /> **2** = mes<br /><br /> **3** = año|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replmonitorhelpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [sp_replmonitorhelppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [sp_replmonitorhelppublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [sp_replmonitorhelpmergesession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [sp_replmonitorhelppublicationthresholds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [sp_replmonitorhelpmergesessiondetail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  
