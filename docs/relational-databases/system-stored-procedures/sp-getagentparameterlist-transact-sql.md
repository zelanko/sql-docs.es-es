---
title: sp_getagentparameterlist (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_getagentparameterlist
- sp_getagentparameterlist_TSQL
helpviewer_keywords:
- sp_getagentparameterlist
ms.assetid: 50d3d3c1-b9a1-417c-bad4-674089c9c60d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3eb58b1f831c1eaec76189b55c8758b0aa6485f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spgetagentparameterlist-transact-sql"></a>sp_getagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista con todos los parámetros del Agente de replicación que se pueden establecer en un perfil de agente para el tipo de agente especificado. Este procedimiento almacenado se ejecuta en el distribuidor en el que se está ejecutando el agente, en cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_getagentparameterlist [ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@agent_type =** ] **'***agent_type***'**  
 Es el agente de replicación para el que se agrega el parámetro. *agent_type* es **int**, y puede tener uno de estos valores:  
  
|Value|Agente|  
|-----------|-----------|  
|**1**|Snapshot|  
|**2**|Registro del LOG|  
|**3**|Distribución|  
|**4**|Mezcla|  
|**9**|Lectura de cola|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_getagentparameter**.  
  
## <a name="see-also"></a>Vea también  
 [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [Perfiles del Agente de replicación](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
