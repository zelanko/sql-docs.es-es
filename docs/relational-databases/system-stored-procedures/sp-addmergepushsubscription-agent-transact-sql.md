---
title: sp_addmergepushsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 60058b5f9779ee9fead3284641cce81ae3702dfb
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032825"
---
# <a name="spaddmergepushsubscriptionagent-transact-sql"></a>sp_addmergepushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un nuevo trabajo de agente que se utiliza para programar la sincronización de una suscripción de inserción con una publicación de combinación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergepushsubscription_agent [ @publication =] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password = ] 'subscriber_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@subscriber =** ] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_security_mode =** ] *subscriber_security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con un suscriptor durante la sincronización. *subscriber_security_mode* es **int**, su valor predeterminado es 1. Si **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. Si **1**, especifica la autenticación de Windows.  
  
 [  **@subscriber_login =** ] **'***subscriber_login***'**  
 Es el inicio de sesión del suscriptor que se debe utilizar al conectarse con un suscriptor durante la sincronización. *subscriber_login* es necesaria si *subscriber_security_mode* está establecido en **0**. *subscriber_login* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_password =** ] **'***subscriber_password***'**  
 Es la contraseña del suscriptor para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *subscriber_password* es necesaria si *subscriber_security_mode* está establecido en **0**. *subscriber_password* es **sysname**, su valor predeterminado es null. Si se utiliza una contraseña de suscriptor, se cifra automáticamente.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con un publicador durante la sincronización. *publisher_security_mode* es **int**, su valor predeterminado es 1. Si **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. Si **1**, especifica la autenticación de Windows.  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 Es el inicio de sesión que se debe utilizar al conectarse con un publicador durante la sincronización. *publisher_login* es **sysname**, su valor predeterminado es null.  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 Es la contraseña utilizada para conectarse al publicador. *publisher_password* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@job_login =** ] **'***job_login***'**  
 Es el inicio de sesión de la cuenta de Windows en la que se ejecuta el agente. *job_login* es **nvarchar (257)**, su valor predeterminado es null. Esta cuenta de Windows se utiliza siempre para las conexiones de agentes al distribuidor y para las conexiones al suscriptor y al publicador, cuando se utiliza la autenticación de Windows integrada.  
  
 [  **@job_password =** ] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows en la que se ejecuta el agente. *job_password* es **sysname**, no tiene ningún valor predeterminado.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@job_name =** ] **'***job_name***'**  
 Es el nombre de un trabajo del agente existente. *job_name* es **sysname**, su valor predeterminado es null. Este parámetro solo se especifica cuando se sincroniza la suscripción con un trabajo existente en lugar de utilizar un trabajo recién creado (la opción predeterminada). Si no es un miembro de la **sysadmin** rol fijo de servidor, debe especificar *job_login* y *job_password* al especificar *job_name*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 Es la frecuencia con que se programa el agente de mezcla. *frequency_type* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64**|Iniciar automáticamente|  
|**128**|Periódica|  
|NULL (predeterminado)||  
  
> [!NOTE]  
>  Si se especifica un valor de **64** hace que el agente de mezcla se ejecute en modo continuo. Esto equivale a configurar el **-continua** parámetro para el agente. Para más información, consulte [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 Los días en que se ejecuta el agente de mezcla. *frequency_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Lunes|  
|**3**|Martes|  
|**4**|Miércoles|  
|**5**|Jueves|  
|**6**|Viernes|  
|**7**|Sábado|  
|**8**|Day|  
|**9**|Días de la semana|  
|**10**|Días del fin de semana|  
|NULL (predeterminado)||  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 Es la fecha del Agente de mezcla. Este parámetro se utiliza cuando *frequency_type* está establecido en **32** (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
|NULL (predeterminado)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 Es la frecuencia de repetición de la programación durante el periodo definido. *frequency_subday* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (predeterminado)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 Es la hora del día en que el agente de mezcla se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 Es la hora del día en que el agente de mezcla deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Es la fecha en que el agente de mezcla se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Es la fecha en la que el agente de mezcla deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 Especifica si la suscripción se puede sincronizar mediante el Administrador de sincronización de Windows. *enabled_for_syncmgr* es **nvarchar (5)**, su valor predeterminado es False. Si **false**, la suscripción no está registrada con el Administrador de sincronización. Si **true**, la suscripción se registra con el Administrador de sincronización y se puede sincronizar sin iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Notas  
 **sp_addmergepushsubscription_agent** se utiliza en la replicación de mezcla y utiliza una funcionalidad similar a [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md).  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_addmergepushsubscription_agent**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
