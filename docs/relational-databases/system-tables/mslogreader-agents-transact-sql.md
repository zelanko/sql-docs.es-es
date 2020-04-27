---
title: MSlogreader_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSlogreader_agents_TSQL
- MSlogreader_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_agents system table
ms.assetid: 8baa3c5a-cb40-42d0-b966-00e6d55368e8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 802d2075a0146febc4521fb17b65f236533596bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907298"
---
# <a name="mslogreader_agents-transact-sql"></a>MSlogreader_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSlogreader_agents** contiene una fila por cada agente de registro del log que se ejecuta en el distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del Agente de registro del LOG.|  
|**name**|**nvarchar(100**|Nombre del Agente de registro del LOG.|  
|**publisher_id**|**smallint**|IDENTIFICADOR del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publicaciones**|**sysname**|Nombre de la publicación.|  
|**local_job**|**bit**|Indica si hay un trabajo de Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  en el distribuidor local.|  
|**job_id**|**binario (16)**|El número de identificación del trabajo.|  
|**profile_id**|**int**|IDENTIFICADOR de configuración de la tabla [MSagent_profiles](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) .|  
|**publisher_security_mode**|**smallint**|El modo de seguridad utilizado por el agente al conectar al publicador. Puede ser uno de los siguientes:<br /><br /> **0** =  0[!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> **1** =  1[!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticación de Windows.|  
|**publisher_login**|**sysname**|Inicio de sesión utilizado al conectar al publicador.|  
|**publisher_password**|**nvarchar (524)**|Valor cifrado de la contraseña que se utiliza al conectar al publicador.|  
|**job_step_uid**|**uniqueidentifier**|El Id. único del paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que se inicia el agente.|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar (524)**||  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
