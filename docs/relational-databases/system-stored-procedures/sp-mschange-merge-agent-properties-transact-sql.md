---
title: sp_MSchange_merge_agent_properties (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_MSchange_merge_agent_properties_TSQL
- sp_MSchange_merge_agent_properties
helpviewer_keywords:
- sp_MSchange_merge_agent_properties
ms.assetid: f775fa0f-28c7-4863-89ce-7bcfa1ab8b5e
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c0a56df34ca780de662d11d826af1b3b88e847e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spmschangemergeagentproperties-transact-sql"></a>sp_MSchange_merge_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de un trabajo de agente de mezcla que se ejecuta en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior distribuidor. Este procedimiento almacenado se utiliza para cambiar las propiedades cuando el publicador se ejecuta en una instancia de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
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
 [ **@publisher** =] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@subscriber=** ] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@subscriber_db=** ] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@property =** ] **'***propiedad***'**  
 Es la propiedad de publicación que se va a cambiar. *propiedad* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@value =** ] **'***valor***'**  
 Es el nuevo valor de la propiedad. *valor* es **nvarchar (524)**, su valor predeterminado es null.  
  
 Esta tabla describe las propiedades del trabajo del Agente de mezcla que se pueden cambiar y las restricciones de los valores de esas propiedades.  
  
|Propiedad|Value|Description|  
|--------------|-----------|-----------------|  
|**Descripción**||Descripción breve de la suscripción.|  
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
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor puede ejecutar **sp_MSchange_merge_agent_properties**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)   
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)  
  
  
