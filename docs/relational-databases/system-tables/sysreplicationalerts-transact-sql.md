---
title: sysreplicationalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dbc1aa2be529d00d2dfd453b181a72ea116809a2
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103013"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información acerca de las condiciones que hacen que se active una alerta de replicación. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|El identificador de la alerta.|  
|**status**|**int**|Valor definido por el usuario:<br /><br /> **0** = sin servicio.<br /><br /> **1** = con servicio.|  
|**agent_type**|**int**|Tipo de agente:<br /><br /> **1** = agente de instantáneas.<br /><br /> **2** = Agente lector del registro.<br /><br /> **3** = agente de distribución.<br /><br /> **4** = agente de mezcla.|  
|**valor de agent_id**|**int**|El identificador del agente de las tablas **MSsnapshot_agents**, **MSlogreader_agents**, **MSdistribution_agents**, o **MSmerge_agents**.|  
|**error_id**|**int**|El identificador de error almacenado en **MSrepl_errors**.|  
|**alert_error_code**|**int**|Id. del mensaje de la alerta activada al registrar esta entrada.|  
|**time**|**datetime**|Hora de inserción del registro.|  
|**publicador**|**sysname**|Nombre del publicador asociado al agente que ha activado esta alerta.|  
|**publisher_db**|**sysname**|Base de datos del publicador asociada al agente que ha activado esta alerta.|  
|**publicación**|**sysname**|Publicación asociada al agente que ha activado esta alerta.|  
|**publication_type**|**int**|Tipo de publicación:<br /><br /> **0** = la instantánea.<br /><br /> **1** = transaccional.<br /><br /> **2** = la mezcla.|  
|**suscriptor**|**sysname**|Nombre del suscriptor asociado al agente que ha activado esta alerta.|  
|**subscriber_db**|**sysname**|Nombre de la base de datos del suscriptor asociada al agente que ha activado esta alerta.|  
|**article**|**sysname**|Nombre del artículo asociado al agente que ha activado esta alerta.|  
|**destination_object**|**sysname**|Nombre de la tabla de suscripciones asociada a la alerta.|  
|**source_object**|**sysname**|Nombre de la tabla de publicaciones asociada a la alerta.|  
|**alert_error_text**|**ntext**|Texto de la alerta.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
