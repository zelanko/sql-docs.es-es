---
title: sp_changesubstatus (Transact-SQL) | Documentos de Microsoft
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
applies_to:
- SQL Server
f1_keywords:
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords:
- sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 94c26330636d4e13fe84a2776a72315a418d3d96
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spchangesubstatus-transact-sql"></a>sp_changesubstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia el estado de un suscriptor existente. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changesubstatus [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
        , [ @status = ] 'status'  
    [ , [ @previous_status = ] 'previous_status' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
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
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @distribution_jobid = ] distribution_jobid ]  
    [ , [ @from_auto_sync = ] from_auto_sync ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @offloadagent= ] remote_agent_activation ]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] dts_package_location ]  
    [ , [ @skipobjectactivation = ] skipobjectactivation  
  [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%**. Si *publicación* no se especifica, se ven afectadas todas las publicaciones.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo. Debe ser único para la publicación. *artículo* es **sysname**, su valor predeterminado es **%**. Si *artículo* no se especifica, se ven afectados todos los artículos.  
  
 [  **@subscriber=**] **'***suscriptor***'**  
 Es el nombre del suscriptor cuyo estado se va a cambiar. *suscriptor* es **sysname**, su valor predeterminado es **%**. Si *suscriptor* no se especifica, se cambia el estado para todos los suscriptores al artículo especificado.  
  
 [  **@status =**] **'***estado***'**  
 Es el estado de suscripción en el **syssubscriptions** tabla. *estado* es **sysname**, no tiene ningún valor predeterminado y puede ser uno de estos valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**Active**|El suscriptor está sincronizado y recibe datos.|  
|**Inactivo**|Existe una entrada de suscriptor sin que haya una suscripción.|  
|**suscrito**|El suscriptor solicita datos, pero aún no está sincronizado.|  
  
 [  **@previous_status=**] **'***previous_status***'**  
 Es el estado anterior de la suscripción. *previous_status* es **sysname**, su valor predeterminado es null. Este parámetro permite cambiar las suscripciones que tienen actualmente ese estado, lo que permite agrupar funciones en un conjunto específico de suscripciones (por ejemplo, establecer active todas las suscripciones de nuevo a **suscrito**).  
  
 [  **@destination_db=**] **'***destination_db***'**  
 Es el nombre de la base de datos de destino. *destination_db* es **sysname**, su valor predeterminado es **%**.  
  
 [  **@frequency_type=**] *frequency_type*  
 Es la frecuencia con que se programa la tarea de distribución. *frequency_type* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_interval=**] *frequency_interval*  
 Es el valor que se aplican a la frecuencia establecida por *frequency_type*. *frequency_interval* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Es la fecha de la tarea de distribución. Este parámetro se utiliza cuando *frequency_type* está establecido en 32 (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
|NULL (predeterminado)||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Indica la frecuencia, en minutos, con que se reprograma durante el período definido. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (predeterminado)||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Es la hora del día en que la tarea de distribución se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Es la hora del día en que la tarea de distribución deja de estar programada, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_date=**] *active_start_date*  
 Es la fecha en que la tarea de distribución se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_date=**] *active_end_date*  
 Es la fecha en la que la tarea de distribución deja de estar programada, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 Es un símbolo del sistema opcional. *optional_command_line* es **nvarchar (4000)**, su valor predeterminado es null.  
  
 [  **@distribution_jobid=**] *distribution_jobid*  
 Es el Id. de trabajo del Agente de distribución en el distribuidor de la suscripción cuando se cambia el estado de la suscripción de inactiva a activa. En otros casos, no se define. Si interviene más de un agente de distribución en una sola llamada a este procedimiento almacenado, el resultado no se define. *distribution_jobid* es **binary (16)**, su valor predeterminado es null.  
  
 [  **@from_auto_sync=**] *from_auto_sync*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 > [!NOTE]  
>  La activación remota del agente ha quedado desusada y ya no es compatible. Este parámetro solamente se admite por compatibilidad de scripts con versiones anteriores. Establecer *remote_agent_activation* en un valor distinto de **0** genera un error.  
  
 [  **@offloadserver=** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  La activación remota del agente ha quedado desusada y ya no es compatible. Este parámetro solamente se admite por compatibilidad de scripts con versiones anteriores. Establecer *remote_agent_server_name* en cualquier valor distinto de NULL, genera un error.  
  
 [ **@dts_package_name**=] **'***dts_package_name***'**  
 Especifica el nombre del paquete de Servicios de transformación de datos (DTS). *dts_package_name* es un **sysname**, su valor predeterminado es null. Por ejemplo, para un paquete denominado **DTSPub_Package** especificaría `@dts_package_name = N'DTSPub_Package'`.  
  
 [ **@dts_package_password**=] **'***dts_package_password***'**  
 Especifica la contraseña del paquete. *dts_package_password* es **sysname** con un valor predeterminado es NULL, que especifica que la propiedad de contraseña se debe dejar sin cambios.  
  
> [!NOTE]  
>  Un paquete DTS debe tener una contraseña.  
  
 [ **@dts_package_location**=] *dts_package_location*  
 Especifica la ubicación del paquete. *dts_package_location* es un **int**, su valor predeterminado es **0**. Si **0**, la ubicación del paquete está en el distribuidor. Si **1**, la ubicación del paquete está en el suscriptor. La ubicación del paquete puede ser **distribuidor** o **suscriptor**.  
  
 [ **@skipobjectactivation**=] *skipobjectactivation*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@distribution_job_name=** ] **'***distribution_job_name***'**  
 Es el nombre del trabajo de distribución. *distribution_job_name* es **sysname**, su valor predeterminado es null.  
  
 [ **@publisher**=] **'***publisher***'**  
 Especifica un no[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse al cambiar las propiedades de artículo en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changesubstatus** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_changesubstatus** cambia el estado del suscriptor en el **syssubscriptions** tabla con el estado cambiado. Si es necesario, actualiza el estado del artículo en el **sysarticles** tabla para indicar activo o inactivo. Si es necesario, Establece la marca de replicación o desactivar el **sysobjects** tabla para la tabla replicada.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor **db_owner** rol fijo de base de datos o el creador de la suscripción puede ejecutar **sp_changesubstatus**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
