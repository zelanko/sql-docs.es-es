---
title: MSdistribution_agents (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- MSdistribution_agents_TSQL
- MSdistribution_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_agents system table
ms.assetid: 0e8f0653-1351-41d1-95d2-40f6d5a050ca
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2bb6aa8917a34946eeaab0d79ccb7a9ed04dcf0d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="msdistributionagents-transact-sql"></a>MSdistribution_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSdistribution_agents** tabla contiene una fila por cada agente de distribución que se ejecuta en el distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del Agente de distribución.|  
|**Nombre**|**nvarchar (100)**|Nombre del Agente de distribución.|  
|**publisher_database_id**|**int**|El Id. de la base de datos del publicador.|  
|**publisher_id**|**smallint**|El identificador del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**Publicación**|**sysname**|Nombre de la publicación.|  
|**subscriber_id**|**smallint**|Id. del suscriptor, que solo utilizan los agentes conocidos. En el caso de los agentes anónimos, esta columna está reservada.|  
|**subscriber_db**|**sysname**|El nombre de la base de datos de suscripción.|  
|**subscription_type**|**int**|El tipo de suscripción:<br /><br /> **0** = inserción.<br /><br /> **1** = extracción.<br /><br /> **2** = anónima.|  
|**local_job**|**bit**|Indica si hay un trabajo de agente SQL Server en el distribuidor local.|  
|**job_id**|**binary (16)**|El número de identificación del trabajo.|  
|**subscription_guid**|**binary (16)**|Id. de las suscripciones de este agente.|  
|**profile_id**|**int**|El identificador de configuración de la [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabla.|  
|**anonymous_subid**|**uniqueidentifier**|Id. de un agente anónimo.|  
|**subscriber_name**|**sysname**|Nombre del suscriptor, que solo utilizan los agentes anónimos.|  
|**virtual_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**anonymous_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**creation_date**|**datetime**|Fecha y hora de creación del Agente de distribución o de mezcla.|  
|**queue_id**|**sysname**|Identificador que se utiliza para localizar la cola de suscripciones de actualización en cola. Para las suscripciones que no sean en cola, el valor es NULL. Para las publicaciones basadas en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server, el valor es un GUID que identifica de forma única la cola que se va a utilizar en la suscripción. Para las publicaciones de cola basadas en SQL Server, la columna contiene el valor **SQL**.<br /><br /> Nota: El uso de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server ha quedado desusado y ya no se admite.|  
|**queue_status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offload_enabled**|**bit**|Indica si el agente puede activarse de manera remota.<br /><br /> **0** especifica que el agente no puede activarse de manera remota.<br /><br /> **1** especifica que el agente se activará de forma remota y en el equipo remoto especificado en el *offload_server* propiedad.|  
|**offload_server**|**sysname**|Nombre de red del servidor que se va a utilizar en la activación remota del agente.|  
|**dts_package_name**|**sysname**|Nombre del paquete DTS. Por ejemplo, para un paquete denominado **DTSPub_Package**, especifique `@dts_package_name = N'DTSPub_Package'`.|  
|**dts_package_password**|**nvarchar (524)**|Contraseña del paquete.|  
|**dts_package_location**|**int**|La ubicación del paquete. La ubicación del paquete puede ser **distribuidor** o **suscriptor**.|  
|**SID**|**varbinary(85)**|Número de identificación de seguridad (SID) del Agente de distribución o del Agente de mezcla durante su primera ejecución.|  
|**queue_server**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**subscriber_security_mode**|**smallint**|Modo de seguridad utilizado por el agente cuando se conecta al suscriptor, que puede ser uno de los siguientes:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticación de SQL Server<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticación de Windows.|  
|**subscriber_login**|**sysname**|Inicio de sesión que se utilizará en la conexión con el suscriptor.|  
|**subscriber_password**|**nvarchar (524)**|Es el valor cifrado de la contraseña utilizada al conectarse al suscriptor.|  
|**reset_partial_snapshot_progress**|**bit**|Indica si se descartará una instantánea descargada parcialmente para que todo el proceso de instantánea pueda empezar de nuevo.|  
|**job_step_uid**|**uniqueidentifier**|El identificador único del trabajo del agente de SQL Server paso en que el agente se inicia.|  
|**flujos de suscripción**|**tinyint**|Establece el número de conexiones permitidas por Agente de distribución para aplicar lotes de cambios en paralelo en un suscriptor. Se admite un intervalo de valores de 1 a 64.|  
|**con optimización para memoria**|**bit**|1 indica que el suscriptor se puede utilizar tablas optimizadas en memoria.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
