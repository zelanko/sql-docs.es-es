---
title: sp_change_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_profile
- sp_change_agent_profile_TSQL
helpviewer_keywords:
- sp_change_agent_profile
ms.assetid: e73acf8d-0be8-4197-ba11-fe798d0e2820
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1d4dedd9a7451daa97b3e1ad130f7f6dd95d8dd9
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823537"
---
# <a name="sp_change_agent_profile-transact-sql"></a>sp_change_agent_profile (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cambia un parámetro de un perfil de agente de replicación almacenado en la [MSagent_profiles &#40;tabla de&#41;de Transact-SQL](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) . Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_change_agent_profile [ @profile_id = ] profile_id   
        , [ @property = ] 'property'   
        , [ @value = ] 'value'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id`Es el identificador del perfil. *profile_id* es de **tipo int**y no tiene ningún valor predeterminado.  
  
`[ @property = ] 'property'`Es el nombre de la propiedad. *Property* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @value = ] 'value'`Es el nuevo valor de la propiedad. el *valor* es **nvarchar (3000)** y no tiene ningún valor predeterminado.  
  
 Esta tabla describe las propiedades del perfil que se pueden modificar.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|**denominación**|Descripción del perfil.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_change_agent_profile** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_change_agent_profile**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_agent_profile &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
