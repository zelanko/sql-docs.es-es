---
description: sysreplicationalerts (Transact-SQL)
title: sysreplicationalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f364d00a57c5b31020689ed3a002300e073d429d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473117"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene información acerca de las condiciones que hacen que se active una alerta de replicación. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|IDENTIFICADOR de la alerta.|  
|**status**|**int**|Valor definido por el usuario:<br /><br /> **0** = no servicio.<br /><br /> **1** = servicio.|  
|**agent_type**|**int**|Tipo de agente:<br /><br /> **1** = agente de instantáneas.<br /><br /> **2** = agente de registro del log.<br /><br /> **3** = agente de distribución.<br /><br /> **4** = agente de mezcla.|  
|**agent_id**|**int**|IDENTIFICADOR del agente de las tablas **MSsnapshot_agents**, **MSlogreader_agents**, **MSdistribution_agents**o **MSmerge_agents**.|  
|**error_id**|**int**|IDENTIFICADOR del error almacenado en **MSrepl_errors**.|  
|**alert_error_code**|**int**|Id. del mensaje de la alerta activada al registrar esta entrada.|  
|**time**|**datetime**|Hora de inserción del registro.|  
|**publisher**|**sysname**|Nombre del publicador asociado al agente que ha activado esta alerta.|  
|**publisher_db**|**sysname**|Base de datos del publicador asociada al agente que ha activado esta alerta.|  
|**publicaciones**|**sysname**|Publicación asociada al agente que ha activado esta alerta.|  
|**publication_type**|**int**|Tipo de publicación:<br /><br /> **0** = instantánea.<br /><br /> **1** = transaccional.<br /><br /> **2** = fusionar mediante combinación.|  
|**suscriptor**|**sysname**|Nombre del suscriptor asociado al agente que ha activado esta alerta.|  
|**subscriber_db**|**sysname**|Nombre de la base de datos del suscriptor asociada al agente que ha activado esta alerta.|  
|**artículo**|**sysname**|Nombre del artículo asociado al agente que ha activado esta alerta.|  
|**destination_object**|**sysname**|Nombre de la tabla de suscripciones asociada a la alerta.|  
|**source_object**|**sysname**|Nombre de la tabla de publicaciones asociada a la alerta.|  
|**alert_error_text**|**ntext**|Texto de la alerta.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
