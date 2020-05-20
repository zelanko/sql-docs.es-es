---
title: sp_help_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords:
- sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ae3e555f48958aec87ed012244fae9775fae1619
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826110"
---
# <a name="sp_help_agent_profile-transact-sql"></a>sp_help_agent_profile (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Muestra el perfil de un agente especificado. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_agent_profile [ [ @agent_type = ] agent_type ]   
    [ , [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @agent_type = ] agent_type`Es el tipo de agente. *agent_type* es de **tipo int**, su valor predeterminado es **0**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Agente de instantáneas|  
|**2**|Agente de registro del LOG|  
|**3**|Agente de distribución|  
|**4**|Agente de mezcla|  
|**9**|Agente de lectura de cola|  
  
`[ @profile_id = ] profile_id`Es el identificador del perfil que se va a mostrar. *profile_id* es de **tipo int**y su valor predeterminado es **-1**, que devuelve todos los perfiles de la tabla **MSagent_profiles** .  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|IDENTIFICADOR del perfil.|  
|**profile_name**|**sysname**|Único para el tipo de agente.|  
|**agent_type**|**int**|**1** = agente de instantáneas<br /><br /> **2** = agente de registro del log<br /><br /> **3** = agente de distribución<br /><br /> **4** = agente de mezcla<br /><br /> **9** = agente de lectura de cola|  
|**Tipo**|**int**|**0** = sistema<br /><br /> **1** = personalizado|  
|**denominación**|**VARCHAR (3000)**|Descripción del perfil.|  
|**def_profile**|**bit**|Especifica si este perfil es el predeterminado para este tipo de agente.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_agent_profile** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **replmonitor** pueden ejecutar **sp_help_agent_profile**.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con perfiles de agente de replicación](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
