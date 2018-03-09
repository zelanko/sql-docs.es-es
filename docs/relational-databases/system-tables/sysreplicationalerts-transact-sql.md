---
title: sysreplicationalerts (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46550c4b3cca05eb6d3c434562970084530d4063
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información acerca de las condiciones que hacen que se active una alerta de replicación. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|El identificador de la alerta.|  
|**status**|**int**|Valor definido por el usuario:<br /><br /> **0** = sin servicio.<br /><br /> **1** = realizando tareas de mantenimiento.|  
|**agent_type**|**int**|Tipo de agente:<br /><br /> **1** = agente de instantáneas.<br /><br /> **2** = Agente lector del registro.<br /><br /> **3** = agente de distribución.<br /><br /> **4** = agente de mezcla.|  
|**agent_id**|**int**|El identificador del agente de las tablas **MSsnapshot_agents**, **MSlogreader_agents**, **MSdistribution_agents**, o **MSmerge_agents**.|  
|**error_id**|**int**|El identificador de error almacenado en **MSrepl_errors**.|  
|**alert_error_code**|**int**|Id. del mensaje de la alerta activada al registrar esta entrada.|  
|**time**|**datetime**|Hora de inserción del registro.|  
|**publicador**|**sysname**|Nombre del publicador asociado al agente que ha activado esta alerta.|  
|**publisher_db**|**sysname**|Base de datos del publicador asociada al agente que ha activado esta alerta.|  
|**publicación**|**sysname**|Publicación asociada al agente que ha activado esta alerta.|  
|**publication_type**|**int**|Tipo de publicación:<br /><br /> **0** = instantánea.<br /><br /> **1** = transaccional.<br /><br /> **2** = la mezcla.|  
|**suscriptor**|**sysname**|Nombre del suscriptor asociado al agente que ha activado esta alerta.|  
|**subscriber_db**|**sysname**|Nombre de la base de datos del suscriptor asociada al agente que ha activado esta alerta.|  
|**artículo**|**sysname**|Nombre del artículo asociado al agente que ha activado esta alerta.|  
|**destination_object**|**sysname**|Nombre de la tabla de suscripciones asociada a la alerta.|  
|**source_object**|**sysname**|Nombre de la tabla de publicaciones asociada a la alerta.|  
|**alert_error_text**|**ntext**|Texto de la alerta.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
