---
title: sp_add_agent_profile (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83fd104a70e8cda855bc13dcedfbb589af5034fb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddagentprofile-transact-sql"></a>sp_add_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuevo perfil para un agente de replicación. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_agent_profile [ [ @profile_id= ] profile_id OUTPUT ]  
        , [ @profile_name= ] 'profile_name'   
        , [ @agent_type= ] 'agent_type' ]   
    [ , [ @profile_type= ] profile_type ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @default= ] default ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id=** ] *profile_id*  
 Es el identificador asociado al perfil que se acaba de insertar. *profile_id* es **int** y es un parámetro OUTPUT opcional. Si se especifica, el valor se establece en el nuevo Id. de perfil.  
  
 [  **@profile_name=** ] **'***profile_name***'**  
 Es el nombre del perfil. *profile_name* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@agent_type=** ] **'***agent_type***'**  
 Es el tipo de agente de replicación. *agent_type* es **int**, no tiene ningún valor predeterminado y puede ser uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Agente de instantáneas|  
|**2**|Agente de registro del LOG|  
|**3**|Agente de distribución|  
|**4**|Agente de mezcla|  
|**9**|Agente de lectura de cola|  
  
 [  **@profile_type=** ] *profile_type*  
 Es el tipo de perfil. *profile_type* es **int**, su valor predeterminado es **1**.  
  
 **0** indica un perfil del sistema. **1** indica un perfil personalizado. Solo los perfiles personalizados pueden crearse con este procedimiento almacenado; por lo tanto, el único valor válido es **1**. Solo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea perfiles del sistema.  
  
 [  **@description=** ] **'***descripción***'**  
 Es una descripción del perfil. *descripción* es **nvarchar (3000)**, no tiene ningún valor predeterminado.  
  
 [  **@default=** ] *predeterminado*  
 Indica si el perfil es el valor predeterminado de *agent_type**.* *valor predeterminado* es **bits**, su valor predeterminado es **0**. **1** indica que el perfil que se va a agregar se convertirá en el nuevo perfil predeterminado para el agente especificado por *agent_type*.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_add_agent_profile** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
 Los perfiles de agente personalizados se agregan con los valores predeterminados de los parámetros de agente. Use [sp_change_agent_parameter &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md) para cambiar estos valores predeterminados o [sp_add_agent_parameter &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md) para agregar parámetros adicionales.  
  
 Cuando **sp_add_agent_profile** es ejecuta, se agrega una fila para el nuevo perfil personalizado en el [MSagent_profiles &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabla y los parámetros predeterminados asociados para este perfil se agregan a la [MSagent_parameters &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) tabla.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_add_agent_profile**.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con perfiles del Agente de replicación](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Perfiles del Agente de replicación](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
