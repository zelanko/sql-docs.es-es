---
title: sp_MSchange_merge_agent_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_merge_agent_properties_TSQL
- sp_MSchange_merge_agent_properties
helpviewer_keywords:
- sp_MSchange_merge_agent_properties
ms.assetid: f775fa0f-28c7-4863-89ce-7bcfa1ab8b5e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f682400bc827d66878499b6e625671d5b9061da
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535655"
---
# <a name="spmschangemergeagentproperties-transact-sql"></a>sp_MSchange_merge_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de un trabajo de agente de mezcla que se ejecuta en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versión posterior de distribuidor. Este procedimiento almacenado se utiliza para cambiar las propiedades cuando el publicador se ejecuta en una instancia de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_MSchange_merge_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @subscriber = ] 'subscriber'` Es el nombre del suscriptor. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @subscriber_db = ] 'subscriber_db'` Es el nombre de la base de datos de suscripción. *subscriber_db* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @property = ] 'property'` Es la propiedad de publicación para cambiar. *propiedad* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @value = ] 'value'` Es el nuevo valor de propiedad. *valor* es **nvarchar (524)**, su valor predeterminado es null.  
  
 Esta tabla describe las propiedades del trabajo del Agente de mezcla que se pueden cambiar y las restricciones de los valores de esas propiedades.  
  
|Property|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**description**||Descripción breve de la suscripción.|  
|**merge_job_login**||Inicio de sesión de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el agente.|  
|**merge_job_password**||Contraseña de la cuenta de Windows en la que se ejecuta el trabajo del agente.|  
|**publisher_login**||Inicio de sesión que se debe utilizar al conectarse a un publicador para sincronizar la suscripción.|  
|**publisher_password**||Contraseña del publicador.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**publisher_security_mode**|**1**|Autenticación de Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**subscriber_login**||Inicio de sesión que se debe utilizar al conectarse a un suscriptor para sincronizar la suscripción.|  
|**subscriber_password**||Contraseña del suscriptor.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_security_mode**|**1**|Autenticación de Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
> [!NOTE]  
>  Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_MSchange_merge_agent_properties** se utiliza en la replicación de mezcla.  
  
 Cuando el publicador se ejecuta en una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, debe utilizar [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) para cambiar las propiedades de un trabajo de agente de mezcla que sincronice una suscripción de inserción que se ejecuta en el distribuidor.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor puede ejecutar **sp_MSchange_merge_agent_properties**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)   
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)  
  
  
