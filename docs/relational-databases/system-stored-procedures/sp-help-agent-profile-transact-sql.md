---
title: sp_help_agent_profile (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords:
- sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 24ceddf37682da448ba318a3ea1050ee6ef5d9af
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpagentprofile-transact-sql"></a>sp_help_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra el perfil de un agente especificado. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_agent_profile [ [ @agent_type = ] agent_type ]   
    [ , [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@agent_type=**] *agent_type*  
 Es el tipo de agente. *agent_type* es **int**, su valor predeterminado es **0**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Agente de instantáneas|  
|**2**|Agente de registro del LOG|  
|**3**|Agente de distribución|  
|**4**|Agente de mezcla|  
|**9**|Agente de lectura de cola|  
  
 [  **@profile_id=**] *profile_id*  
 Es el identificador del perfil que se va a mostrar. *profile_id* es **int**, su valor predeterminado es **-1**, que devuelve todos los perfiles de la **MSagent_profiles** tabla.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|Identificador del perfil.|  
|**profile_name**|**sysname**|Único para el tipo de agente.|  
|**agent_type**|**int**|**1** = agente de instantáneas<br /><br /> **2** = Agente lector del registro<br /><br /> **3** = agente de distribución<br /><br /> **4** = agente de mezcla<br /><br /> **9** = agente de lectura de cola|  
|**Tipo**|**int**|**0** = sistema<br /><br /> **1** = personalizado|  
|**Descripción**|**varchar(3000)**|Descripción del perfil.|  
|**def_profile**|**bit**|Especifica si este perfil es el predeterminado para este tipo de agente.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_agent_profile** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **replmonitor** rol fijo de base de datos puede ejecutar **sp_help_agent_profile**.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con perfiles del Agente de replicación](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
