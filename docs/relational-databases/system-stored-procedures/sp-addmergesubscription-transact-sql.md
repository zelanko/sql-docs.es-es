---
title: sp_addmergesubscription (Transact-SQL) | Documentos de Microsoft
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
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8d5b8cf744909969166b2d391604735c1a2a7db4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993672"
---
# <a name="spaddmergesubscription-transact-sql"></a>sp_addmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una suscripción de mezcla de inserción o extracción. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergesubscription [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @subscriber_type= ] 'subscriber_type' ]  
    [ , [ @subscription_priority= ] subscription_priority ]  
    [ , [ @sync_type= ] 'sync_type' ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @optional_command_line= ] 'optional_command_line' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @use_interactive_resolver= ] 'use_interactive_resolver' ]  
    [ , [ @merge_job_name= ] 'merge_job_name' ]  
    [ , [ @hostname = ] 'hostname'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado. La publicación debe existir.  
  
 [  **@subscriber =**] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db*es **sysname**, su valor predeterminado es null.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 Es el tipo de suscripción. *subscription_type*es **nvarchar (15)**, con un valor predeterminado es PUSH. Si **inserción**, se agrega una suscripción de inserción y el agente de mezcla se agrega en el distribuidor. Si **extracción**, se agrega una suscripción de extracción sin agregar un agente de mezcla en el distribuidor.  
  
> [!NOTE]  
>  Las suscripciones anónimas no necesitan utilizar este procedimiento almacenado.  
  
 [  **@subscriber_type=**] **'***subscriber_type***'**  
 Es el tipo de suscriptor. *propiedad subscriber_type*es **nvarchar (15)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**local** (valor predeterminado)|Suscriptor solo conocido para el publicador.|  
|**Global**|Suscriptor conocido para todos los servidores.|  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, se hace referencia a las suscripciones locales como suscripciones de cliente y a las suscripciones globales como suscripciones de servidor.  
  
 [  **@subscription_priority=**] *subscription_priority*  
 Es un número que indica la prioridad de la suscripción. *subscription_priority*es **real**, su valor predeterminado es null. En las suscripciones locales y anónimas, la prioridad es 0.0. En el caso de las suscripciones globales, la prioridad debe ser inferior a 100.0.  
  
 [  **@sync_type=**] **'***sync_type***'**  
 Es el tipo de sincronización de suscripción. *sync_type*es **nvarchar (15)**, su valor predeterminado es **automática**. Puede ser **automática** o **ninguno**. Si **automática**, el esquema y los datos iniciales de las tablas publicadas se transfieren primero al suscriptor. Si **ninguno**, se supone el suscriptor ya tiene el esquema y los datos iniciales de las tablas publicadas. Las tablas y los datos del sistema se transfieren siempre.  
  
> [!NOTE]  
>  Se recomienda no especificar un valor de **ninguno**.  
  
 [  **@frequency_type=**] *frequency_type*  
 Es un valor que indica cuándo se ejecutará el agente de mezcla. *frequency_type* es **int**, y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**10**|Programación mensual|  
|**20**|Mensualmente, dependiendo del intervalo de frecuencia|  
|**40**|Cuando se inicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|NULL (predeterminado)||  
  
 [  **@frequency_interval=**] *frequency_interval*  
 El día o los días que se ejecuta el agente de mezcla. *frequency_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
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
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Es la repetición de mezcla programada del intervalo de frecuencia de cada mes. *frequency_relative_interval* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
|NULL (predeterminado)||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor*es **int**, su valor predeterminado es null.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Es la unidad de *frequency_subday_interval*. *frequency_subday* es **int**, y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (predeterminado)||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 Es la frecuencia de *frequency_subday* que transcurren entre cada mezcla. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Es la hora del día en que el agente de mezcla se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Es la hora del día en que el agente de mezcla deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_date=**] *active_start_date*  
 Es la fecha en que el agente de mezcla se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_date=**] *active_end_date*  
 Es la fecha en la que el agente de mezcla deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 Es el símbolo del sistema opcional que se va a ejecutar. *optional_command_line*es **nvarchar (4000)**, su valor predeterminado es null. Este parámetro se utiliza para agregar un comando que captura el resultado y lo guarda en un archivo o para especificar un atributo o archivo de configuración.  
  
 [  **@description=**] **'***descripción***'**  
 Es una breve descripción de esta suscripción de mezcla. *descripción*es **nvarchar (255)**, su valor predeterminado es null. Este valor se muestra el Monitor de replicación en el **Nombre_descriptivo** columna, que se puede usar para ordenar las suscripciones para una publicación supervisada.  
  
 [  **@enabled_for_syncmgr=**] **'***enabled_for_syncmgr***'**  
 Especifica si la suscripción se puede sincronizar mediante el Administrador de sincronización de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. *enabled_for_syncmgr* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **false**, la suscripción no está registrada con el Administrador de sincronización. Si **true**, la suscripción se registra con el Administrador de sincronización y se puede sincronizar sin iniciar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 Especifica que el agente puede activarse de manera remota. *remote_agent_activation* es **bits** con un valor predeterminado de **0**.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solamente se mantiene por compatibilidad con versiones anteriores de scripts.  
  
 [  **@offloadserver=** ] **'***remote_agent_server_name***'**  
 Especifica el nombre de red del servidor a utilizar en la activación remota del agente. *remote_agent_server_name*es **sysname**, su valor predeterminado es null.  
  
 [  **@use_interactive_resolver=** ] **'***use_interactive_resolver***'**  
 Permite que los conflictos se resuelvan de forma interactiva para todos los artículos que lo permitan. *use_interactive_resolver* es **nvarchar (5)**, con un valor predeterminado es FALSE.  
  
 [  **@merge_job_name=** ] **'***merge_job_name***'**  
 El *@merge_job_name* parámetro está en desuso y no se puede establecer. *merge_job_name* es **sysname**, su valor predeterminado es null.  
  
 [ **@hostname**=] **'***hostname***'**  
 Invalida el valor devuelto por [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) cuando esta función se utiliza en la cláusula WHERE de un filtro con parámetros. *Nombre de host* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  Por motivos de rendimiento, se recomienda no aplicar funciones a los nombres de columna en las cláusulas de filtro de fila con parámetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Si usa [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) en una cláusula de filtro e invalide el valor de HOST_NAME, puede que sea necesario para convertir tipos de datos mediante [convertir](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obtener más información acerca de las prácticas recomendadas para este caso, vea la sección "Reemplazar el valor de HOST_NAME()" del tema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergesubscription** se utiliza en la replicación de mezcla.  
  
 Cuando **sp_addmergesubscription** se ejecuta un miembro de la **sysadmin** rol fijo de servidor para crear una suscripción de inserción, el trabajo de agente de mezcla se crea implícitamente y se ejecuta bajo la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente cuenta de servicio. Se recomienda ejecutar [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) y especifique las credenciales de una cuenta de Windows diferente, específica del agente para **@job_login** y **@job_password**. Para más información, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addmergesubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Resolución interactiva de conflictos](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
