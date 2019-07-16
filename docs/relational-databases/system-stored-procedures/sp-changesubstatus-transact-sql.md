---
title: sp_changesubstatus (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords:
- sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe75ffcf1e8cdcc387acb48c882e247b21889c06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113811"
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
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%** . Si *publicación* no se especifica, se ven afectadas todas las publicaciones.  
  
`[ @article = ] 'article'` Es el nombre del artículo. Debe ser único para la publicación. *artículo* es **sysname**, su valor predeterminado es **%** . Si *artículo* no se especifica, se ven afectados todos los artículos.  
  
`[ @subscriber = ] 'subscriber'` Es el nombre del suscriptor para cambiar el estado de. *suscriptor* es **sysname**, su valor predeterminado es **%** . Si *suscriptor* no se especifica, se cambia el estado para todos los suscriptores al artículo especificado.  
  
`[ @status = ] 'status'` Es el estado de la suscripción en el **syssubscriptions** tabla. *estado* es **sysname**, no tiene ningún valor predeterminado y puede ser uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**active**|El suscriptor está sincronizado y recibe datos.|  
|**inactive**|Existe una entrada de suscriptor sin que haya una suscripción.|  
|**suscrito**|El suscriptor solicita datos, pero aún no está sincronizado.|  
  
`[ @previous_status = ] 'previous_status'` Es el estado anterior de la suscripción. *previous_status* es **sysname**, su valor predeterminado es null. Este parámetro le permite cambiar las suscripciones que tienen actualmente ese estado, lo que permite agrupar funciones en un conjunto específico de suscripciones (por ejemplo, establecer todos los activos hacer una copia de las suscripciones a **suscrito**).  
  
`[ @destination_db = ] 'destination_db'` Es el nombre de la base de datos de destino. *destination_db* es **sysname**, su valor predeterminado es **%** .  
  
`[ @frequency_type = ] frequency_type` Es la frecuencia con que se programa la tarea de distribución. *frequency_type* es **int**, su valor predeterminado es null.  
  
`[ @frequency_interval = ] frequency_interval` Es el valor que se aplican a la frecuencia establecida por *frequency_type*. *frequency_interval* es **int**, su valor predeterminado es null.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` Es la fecha de la tarea de distribución. Este parámetro se utiliza cuando *frequency_type* está establecido en 32 (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
|NULL (predeterminado)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es null.  
  
`[ @frequency_subday = ] frequency_subday` Es la frecuencia, en minutos, para volver a programar durante el período definido. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (predeterminado)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` Es la hora del día en la tarea de distribución se primer programa, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` Es la hora del día en que la tarea de distribución deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
`[ @active_start_date = ] active_start_date` Es la fecha en la tarea de distribución programada, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
`[ @active_end_date = ] active_end_date` Es la fecha en la tarea de distribución deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
`[ @optional_command_line = ] 'optional_command_line'` Es un símbolo del sistema opcional. *optional_command_line* es **nvarchar (4000)** , su valor predeterminado es null.  
  
`[ @distribution_jobid = ] distribution_jobid` Es el Id. de trabajo del agente de distribución en el distribuidor para la suscripción al cambiar el estado de la suscripción de inactiva a activa. En otros casos, no se define. Si interviene más de un agente de distribución en una sola llamada a este procedimiento almacenado, el resultado no se define. *distribution_jobid* es **binary (16)** , su valor predeterminado es null.  
  
`[ @from_auto_sync = ] from_auto_sync` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] remote_agent_activation`
 > [!NOTE]  
>  La activación remota del agente ha quedado desusada y ya no es compatible. Este parámetro solamente se admite por compatibilidad de scripts con versiones anteriores. Establecer *remote_agent_activation* a un valor distinto de **0** genera un error.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  La activación remota del agente ha quedado desusada y ya no es compatible. Este parámetro solamente se admite por compatibilidad de scripts con versiones anteriores. Establecer *remote_agent_server_name* en cualquier valor distinto de NULL se genera un error.  
  
`[ @dts_package_name = ] 'dts_package_name'` Especifica el nombre del paquete de servicios de transformación de datos (DTS). *dts_package_name* es un **sysname**, su valor predeterminado es null. Por ejemplo, para un paquete denominado **DTSPub_Package** especificaría `@dts_package_name = N'DTSPub_Package'`.  
  
`[ @dts_package_password = ] 'dts_package_password'` Especifica la contraseña del paquete. *dts_package_password* es **sysname** con el valor predeterminado es NULL, que especifica que la propiedad de contraseña se dejará sin cambios.  
  
> [!NOTE]  
>  Un paquete DTS debe tener una contraseña.  
  
`[ @dts_package_location = ] dts_package_location` Especifica la ubicación del paquete. *dts_package_location* es un **int**, su valor predeterminado es **0**. Si **0**, es la ubicación del paquete en el distribuidor. Si **1**, la ubicación del paquete está en el suscriptor. La ubicación del paquete puede ser **distribuidor** o **suscriptor**.  
  
`[ @skipobjectactivation = ] skipobjectactivation` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @distribution_job_name = ] 'distribution_job_name'` Es el nombre de la tarea de distribución. *distribution_job_name* es **sysname**, su valor predeterminado es null.  
  
`[ @publisher = ] 'publisher'` Especifica que no es [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse cuando se cambia las propiedades del artículo en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changesubstatus** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_changesubstatus** cambia el estado del suscriptor en el **syssubscriptions** tabla con el estado cambiado. Si es necesario, actualiza el estado del artículo en el **sysarticles** tabla para indicar el activo o inactivo. Si es necesario, Establece la marca de replicación o desactivar el **sysobjects** tabla para la tabla replicada.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor **db_owner** rol fijo de base de datos o el creador de la suscripción puede ejecutar **sp_changesubstatus**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
