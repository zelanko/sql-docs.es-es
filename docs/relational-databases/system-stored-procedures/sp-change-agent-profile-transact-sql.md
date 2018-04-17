---
title: sp_change_agent_profile (Transact-SQL) | Documentos de Microsoft
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
- sp_change_agent_profile
- sp_change_agent_profile_TSQL
helpviewer_keywords:
- sp_change_agent_profile
ms.assetid: e73acf8d-0be8-4197-ba11-fe798d0e2820
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f873d60a003da09753c7c382be71ad1a3fc78e63
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spchangeagentprofile-transact-sql"></a>sp_change_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia un parámetro de un perfil de agente de replicación almacenado en el [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabla. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_change_agent_profile [ @profile_id = ] profile_id   
        , [ @property = ] 'property'   
        , [ @value = ] 'value'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id=** ] *profile_id*  
 Es el identificador del perfil. *profile_id* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@property=** ] **'***propiedad***'**  
 Es el nombre de la propiedad. *propiedad* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@value=** ] **'***valor***'**  
 Es el nuevo valor de la propiedad. *valor* es **nvarchar (3000)**, no tiene ningún valor predeterminado.  
  
 Esta tabla describe las propiedades del perfil que se pueden modificar.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**Descripción**|Descripción del perfil.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_change_agent_profile** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_change_agent_profile**.  
  
## <a name="see-also"></a>Vea también  
 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
