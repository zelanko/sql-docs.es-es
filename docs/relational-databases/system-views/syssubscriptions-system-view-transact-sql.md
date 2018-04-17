---
title: syssubscriptions (vista del sistema) (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0cab4eb2c04f929a0d161803e36ae7de00fbe01
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (vista del sistema de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **syssubscriptions** vista presenta información de suscripción. Esta vista se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Id. único de un artículo suscrito.|  
|**srvid**|**smallint**|Id. de servidor del suscriptor.|  
|**dest_db**|**sysname**|El nombre de la base de datos de suscripción.|  
|**status**|**tinyint**|El estado de la suscripción:<br /><br /> **0** = inactivo.<br /><br /> **1** = suscrito.<br /><br /> **2** = activo.|  
|**sync_type**|**tinyint**|El tipo de sincronización inicial:<br /><br /> **1** = automático.<br /><br /> **2** = none.|  
|**login_name**|**sysname**|El nombre de inicio de sesión utilizado al conectarse al publicador para agregar la suscripción.|  
|**subscription_type**|**int**|El tipo de suscripción:<br /><br /> **0** = inserción: el agente de distribución se ejecuta en el distribuidor.<br /><br /> **1** = extracción: el agente de distribución se ejecuta en el suscriptor.|  
|**distribution_jobid**|**binary (16)**|Identifica el trabajo del Agente de distribución utilizado para sincronizar la suscripción.|  
|**timestmap**|**timestamp**|Fecha y la hora de creación de la suscripción.|  
|**update_mode**|**tinyint**|Modo de actualización:<br /><br /> **0** = solo lectura.<br /><br /> **1** = actualización inmediata.|  
|**loopback_detection**|**bit**|Se aplica a las suscripciones que forman parte de una topología de replicación transaccional bidireccional. La detección de bucles de retorno determina si el Agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor:<br /><br /> **0** = las envía.<br /><br /> **1** = no no volver a enviar.|  
|**queued_reinit**|**bit**|Especifica si el artículo está marcado para inicialización o reinicialización. Un valor de **1** especifica que el artículo suscrito está marcado para inicialización o reinicialización.|  
|**nosync_type**|**tinyint**|Tipo de inicialización de la suscripción:<br /><br /> **0** = automático (instantánea)<br /><br /> **1** = solo admite replicación<br /><br /> **2** = inicializar con copia de seguridad<br /><br /> **3** = inicializar del número de secuencia de registro (LSN)<br /><br /> Para obtener más información, consulte el **@sync_type** parámetro de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**SRVNAME**|**sysname**|Nombre del suscriptor.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
