---
title: sp_addpullsubscription_agent (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords: sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e13ce0bc7be6b2e21a30f13a3cf7cc299d00295
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddpullsubscriptionagent-transact-sql"></a>sp_addpullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un nuevo trabajo de agente programado utilizado para sincronizar una suscripción de extracción a una publicación transaccional. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addpullsubscription_agent [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor = ] 'distributor' ]  
    [ , [ @distribution_db = ] 'distribution_db' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]  
    [ , [ @distributor_login = ] 'distributor_login' ]  
    [ , [ @distributor_password = ] 'distributor_password' ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subda y= ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @distribution_jobid = ] distribution_jobid OUTPUT ]  
    [ , [ @encrypted_distributor_password = ] encrypted_distributor_password ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port = ] ftp_port ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]  
    [ , [ @working_directory = ] 'working_directory' ]  
    [ , [ @use_ftp = ] 'use_ftp' ]  
    [ , [ @publication_type = ] publication_type ]  
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @offloadagent = ] 'remote_agent_activation' ]  
    [ , [ @offloadserver = ] 'remote_agent_server_name']  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=**] **'***publisher_db'*  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es null. *publisher_db* omite los publicadores de Oracle.  
  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@subscriber=**] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores.  
  
 [  **@subscriber_security_mode=**] *subscriber_security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con un suscriptor durante la sincronización. *subscriber_security_mode* es **int,** con un valor predeterminado es NULL. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. **1** especifica autenticación de Windows.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores. El Agente de distribución siempre conecta con el suscriptor local mediante Autenticación de Windows. Si un valor distinto de NULL o **1** se especifica para este parámetro, se devuelve un mensaje de advertencia.  
  
 [  **@subscriber_login =**] **'***subscriber_login***'**  
 Es el inicio de sesión del suscriptor que se utilizará al conectarse a un suscriptor durante la sincronización. *subscriber_login* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores. Si se especifica un valor para este parámetro, se devuelve un mensaje de advertencia, pero el valor se pasa por alto.  
  
 [  **@subscriber_password=**] **'***subscriber_password***'**  
 Es la contraseña del suscriptor. *subscriber_password* es necesaria si *subscriber_security_mode* está establecido en **0**. *subscriber_password* es **sysname**, su valor predeterminado es null. Si se utiliza una contraseña de suscriptor, se cifra automáticamente.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores. Si se especifica un valor para este parámetro, se devuelve un mensaje de advertencia, pero el valor se pasa por alto.  
  
 [  **@distributor=**] **'***distribuidor***'**  
 Es el nombre del distribuidor. *distribuidor* es **sysname**, su valor predeterminado es el valor especificado por *publisher*.  
  
 [  **@distribution_db=**] **'***distribution_db***'**  
 Es el nombre de la base de datos de distribución. *distribution_db* es **sysname**, su valor predeterminado es null.  
  
 [  **@distributor_security_mode=**] *distributor_security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con un distribuidor durante la sincronización. *distributor_security_mode* es **int**, su valor predeterminado es **1**. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. **1** especifica autenticación de Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login=**] **'***distributor_login***'**  
 Es el inicio de sesión del distribuidor que se debe utilizar al conectarse con un distribuidor durante la sincronización. *distributor_login* es necesaria si *distributor_security_mode* está establecido en **0**. *distributor_login* es **sysname**, su valor predeterminado es null.  
  
 [  **@distributor_password =**] **'***distributor_password***'**  
 Es la contraseña del distribuidor. *distributor_password* es necesaria si *distributor_security_mode* está establecido en **0**. *distributor_password* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  No utilice una contraseña en blanco. Utilice una contraseña segura. Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 Es un símbolo del sistema opcional proporcionado al Agente de distribución. Por ejemplo, **- DefinitionFile** C:\Distdef.txt o **- CommitBatchSize** 10. *optional_command_line* es **nvarchar (4000)**, su valor predeterminado es una cadena vacía.  
  
 [  **@frequency_type=**] *frequency_type*  
 Es la frecuencia con que se programa el agente de distribución. *frequency_type* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2** (predeterminado)|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64**|Iniciar automáticamente|  
|**128**|Periódica|  
  
> [!NOTE]  
>  Especifica el valor de **64** hace que el agente de distribución para que se ejecute en modo continuo. Esto equivale a configurar la **-continua** parámetro para el agente. Para más información, consulte [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
 [  **@frequency_interval=**] *frequency_interval*  
 Es el valor que se aplican a la frecuencia establecida por *frequency_type*. *frequency_interval* es **int**, su valor predeterminado es 1.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Es la fecha del Agente de distribución. Este parámetro se utiliza cuando *frequency_type* está establecido en **32** (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1** (predeterminado)|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es **1**.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Es la frecuencia de repetición de la programación durante el periodo definido. *frequency_subday* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1** (predeterminado)|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es **1**.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Es la hora del día en que el agente de distribución se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es **0**.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Es la hora del día en que el agente de distribución deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es **0**.  
  
 [  **@active_start_date=**] *active_start_date*  
 Es la fecha en que el agente de distribución se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es **0**.  
  
 [  **@active_end_date=**] *active_end_date*  
 Es la fecha en la que el agente de distribución deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es **0**.  
  
 [  **@distribution_jobid =**] *distribution_jobid***salida**  
 Es el identificador del agente de distribución para este trabajo. *distribution_jobid* es **binary (16)**, su valor predeterminado es NULL y es un parámetro de salida.  
  
 [  **@encrypted_distributor_password=**] *encrypted_distributor_password*  
 Establecer *encrypted_distributor_password* ya no se admite. Intentando establecer esta **bits** parámetro **1** se producirá un error.  
  
 [  **@enabled_for_syncmgr=**] **'***enabled_for_syncmgr***'**  
 Indica si se puede sincronizar la suscripción a través de [!INCLUDE[msCoName](../../includes/msconame-md.md)] el Administrador de sincronización. *enabled_for_syncmgr* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **false**, la suscripción no está registrada con el Administrador de sincronización. Si **true**, la suscripción se registra con el Administrador de sincronización y se puede sincronizar sin iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@ftp_address=**] **'***ftp_address***'**  
 Se conserva únicamente por compatibilidad con versiones anteriores.  
  
 [  **@ftp_port=**] *ftp_port*  
 Se conserva únicamente por compatibilidad con versiones anteriores.  
  
 [  **@ftp_login=**] **'***ftp_login***'**  
 Se conserva únicamente por compatibilidad con versiones anteriores.  
  
 [  **@ftp_password=**] **'***ftp_password***'**  
 Se conserva únicamente por compatibilidad con versiones anteriores.  
  
 [  **@alt_snapshot_folder=** ] **'***alternate_snapshot_folder'*  
 Especifica la ubicación de la carpeta alternativa de la instantánea. *alternate_snapshot_folder* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@working_directory** =] **'***working_director***'**  
 Es el nombre del directorio de trabajo utilizado para almacenar archivos de datos y de esquema para la publicación. *working_directory* es **nvarchar (255)**, su valor predeterminado es null. El nombre se debe especificar en el formato UNC.  
  
 [  **@use_ftp** =] **'***use_ftp***'**  
 Especifica que se utilizará FTP en lugar del protocolo regular para recuperar las instantáneas. *use_ftp* es **nvarchar (5)**, con un valor predeterminado es FALSE.  
  
 [  **@publication_type** =] *publication_type*  
 Especifica el tipo de replicación de la publicación. *publication_type* es un **tinyint** con un valor predeterminado de **0**. Si **0**, publicación es un tipo de transacción. Si **1**, publicación es un tipo de instantánea. Si **2**, publicación es un tipo de combinación.  
  
 [  **@dts_package_name** =] **'***dts_package_name***'**  
 Especifica el nombre del paquete DTS. *dts_package_name* es un **sysname** con un valor predeterminado es NULL. Por ejemplo, para especificar un paquete de `DTSPub_Package`, el parámetro sería `@dts_package_name = N'DTSPub_Package'`.  
  
 [  **@dts_package_password** =] **'***dts_package_password***'**  
 Especifica la contraseña del paquete, si procede. *dts_package_password* es **sysname** su valor predeterminado es null, lo que significa que una contraseña no está en el paquete.  
  
> [!NOTE]  
>  Debe especificar una contraseña si *dts_package_name* se especifica.  
  
 [  **@dts_package_location** =] **'***dts_package_location***'**  
 Especifica la ubicación del paquete. *dts_package_location* es un **tipo (12)**, su valor predeterminado es **suscriptor**. La ubicación del paquete puede ser **distribuidor** o **suscriptor**.  
  
 [  **@reserved** =] **'***reservada***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@offloadagent** =] '*remote_agent_activation*'  
 > [!NOTE]  
>  La activación remota del agente ha quedado desusada y ya no es compatible. Este parámetro solamente se admite por compatibilidad de scripts con versiones anteriores. Establecer *remote_agent_activation* en un valor distinto de **false** generará un error.  
  
 [  **@offloadserver** =] '*remote_agent_server_name*'  
 > [!NOTE]  
>  La activación remota del agente ha quedado desusada y ya no es compatible. Este parámetro solamente se admite por compatibilidad de scripts con versiones anteriores. Establecer *remote_agent_server_name* en cualquier valor distinto de NULL, se generará un error.  
  
 [  **@job_name** =] '*job_name*'  
 Es el nombre de un trabajo del agente existente. *job_name* es **sysname**, su valor predeterminado es null. Este parámetro solamente se especifica cuando la suscripción se va a sincronizar mediante un trabajo existente en lugar de uno recién creado (el valor predeterminado). Si no es un miembro de la **sysadmin** rol fijo de servidor, debe especificar *job_login* y *job_password* cuando se especifica *job_name*.  
  
 [  **@job_login** =] **'***job_login***'**  
 Es el inicio de sesión de la cuenta de Windows en la que se ejecuta el agente. *job_login* es **nvarchar (257)**, no tiene ningún valor predeterminado. Esta cuenta de Windows siempre se utiliza para las conexiones del agente con el suscriptor.  
  
 [  **@job_password** =] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows en la que se ejecuta el agente. *job_password* es **sysname**, no tiene ningún valor predeterminado.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addpullsubscription_agent** se utiliza en la replicación de instantáneas y transaccional.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addpullsubscription_agent**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
