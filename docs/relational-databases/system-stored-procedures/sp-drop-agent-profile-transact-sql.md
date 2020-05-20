---
title: sp_drop_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_drop_agent_profile
- sp_drop_agent_profile_TSQL
helpviewer_keywords:
- sp_drop_agent_profile
ms.assetid: b884f9ef-ae89-4cbc-a917-532c3ff6ed41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 36ffa90eeb79316ed886990568ba81184d129b05
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826119"
---
# <a name="sp_drop_agent_profile-transact-sql"></a>sp_drop_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un perfil de la tabla **MSagent_profiles** . Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_drop_agent_profile [ @profile_id = ] profile_id  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id`Es el identificador del perfil que se va a quitar. *profile_id* es de **tipo int**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_drop_agent_profile** se utiliza en todos los tipos de replicación.  
  
 Los parámetros del perfil especificado también se quitan de la tabla **MSagent_parameters** .  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_drop_agent_profile**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_agent_profile &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
