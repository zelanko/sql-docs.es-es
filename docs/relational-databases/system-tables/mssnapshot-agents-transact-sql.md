---
title: MSsnapshot_agents (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- MSsnapshot_agents
- MSsnapshot_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_agents system table
ms.assetid: aeae0a2e-4c21-4c45-be65-1e426fa52bdd
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5ef7538fa8b7066397804b1b58521f090a44a3d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshotagents-transact-sql"></a>MSsnapshot_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSsnapshot_agents** tabla contiene una fila por cada agente de instantáneas asociados al distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del Agente de instantáneas.|  
|**Nombre**|**nvarchar (100)**|Nombre del Agente de instantáneas.|  
|**publisher_id**|**smallint**|El identificador del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**Publicación**|**sysname**|Nombre de la publicación.|  
|**publication_type**|**int**|Tipo de publicación:<br /><br /> **0** = transaccional.<br /><br /> **1** = instantánea.<br /><br /> **2** = la mezcla.|  
|**local_job**|**bit**|Indica si hay un trabajo de Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  en el distribuidor local.|  
|**job_id**|**binary (16)**|El número de identificación del trabajo.|  
|**profile_id**|**int**|El identificador de configuración de la [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabla.|  
|**dynamic_filter_login**|**sysname**|El valor utilizado para evaluar la [SUSER_SNAME &#40;Transact-SQL&#41; ](../../t-sql/functions/suser-sname-transact-sql.md) función en filtros con parámetros que definen una partición. Esta columna se utiliza para una instantánea con particiones.|  
|**dynamic_filter_hostname**|**sysname**|El valor utilizado para evaluar la [HOST_NAME &#40;Transact-SQL&#41; ](../../t-sql/functions/host-name-transact-sql.md) función en filtros con parámetros que definen una partición. Esta columna se utiliza para una instantánea con particiones.|  
|**publisher_security_mode**|**smallint**|El modo de seguridad utilizado por el agente al conectar al publicador. Puede ser uno de los siguientes:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticación de Windows.|  
|**publisher_login**|**sysname**|Inicio de sesión utilizado al conectar al publicador.|  
|**publisher_password**|**nvarchar (524)**|Valor cifrado de la contraseña que se utiliza al conectar al publicador.|  
|**job_step_uid**|**uniqueidentifier**|El Id. único del paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que se inicia el agente.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
