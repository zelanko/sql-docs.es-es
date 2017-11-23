---
title: sp_update_agent_profile (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_update_agent_profile_TSQL
- sp_update_agent_profile
helpviewer_keywords: sp_update_agent_profile
ms.assetid: cc81f227-0df3-4151-bb4d-4f45ea997b71
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4f3088c28098611567b80de916b84b73800dc2e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spupdateagentprofile-transact-sql"></a>sp_update_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza el perfil utilizado por un agente de replicación. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_update_agent_profile [@agent_type=] agent_type, [ @agent_id= ] agent_id, [ @profile_id= ] profile_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@agent_type=**] **'***agent_type***'**  
 Es el tipo de agente. *agent_type* es **int**, no tiene ningún valor predeterminado y puede ser uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Agente de instantáneas.|  
|**2**|Agente de lector del registro.|  
|**3**|Agente de distribución.|  
|**4**|Agente de mezcla.|  
|**9**|Agente de lectura de cola|  
  
 [**@agent_id=**] *agent_id*  
 Es el identificador del agente. *agent_id* es **int**, no tiene ningún valor predeterminado.  
  
 [**@profile_id=**] *profile_id*  
 Es el identificador del perfil que debe utilizar el agente. *profile_id* es **int**, no tiene ningún valor predeterminado. Para ver una lista de los perfiles definidos para cada agente, use [sp_help_agent_profile &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Para obtener más información acerca de los perfiles de sistema, consulte [perfiles de agente de replicación](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_update_agent_profile** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_update_agent_profile**.  
  
## <a name="see-also"></a>Vea también  
 [Perfiles del Agente de replicación](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
