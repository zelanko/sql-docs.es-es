---
title: sp_drop_agent_profile (Transact-SQL) | Documentos de Microsoft
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
- sp_drop_agent_profile
- sp_drop_agent_profile_TSQL
helpviewer_keywords: sp_drop_agent_profile
ms.assetid: b884f9ef-ae89-4cbc-a917-532c3ff6ed41
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d11a60ab8c1b8d13f56c941fe6beeb0284e171b8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spdropagentprofile-transact-sql"></a>sp_drop_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un perfil de la **MSagent_profiles** tabla. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_drop_agent_profile [ @profile_id = ] profile_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id=**] *profile_id*  
 Es el identificador del perfil que se va a quitar. *profile_id* es **int**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_drop_agent_profile** se utiliza en todos los tipos de replicación.  
  
 Los parámetros del perfil especificado también se quitan de la **MSagent_parameters** tabla.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_drop_agent_profile**.  
  
## <a name="see-also"></a>Vea también  
 [sp_add_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
