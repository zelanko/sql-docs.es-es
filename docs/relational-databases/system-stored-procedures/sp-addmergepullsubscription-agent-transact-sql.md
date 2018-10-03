---
title: sp_addmergepullsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: da16887ff7debf09e69fc72cf464f5838cf6ddc7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749750"
---
# <a name="spaddmergepullsubscriptionagent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un nuevo trabajo de agente utilizado para programar la sincronización de una suscripción de extracción a una publicación de combinación. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergepullsubscription_agent [ [ @name = ] 'name' ]   
        , [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication =] 'publication'   
    [ , [ @publisher_security_mod e= ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher_encrypted_password = ] publisher_encrypted_password ]   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password= ] 'subscriber_password' ]   
    [ , [ @distributor = ] 'distributor' ]   
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @encrypted_password = ] encrypted_password ]   
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
    [ , [ @merge_jobid = ] merge_jobid ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]    
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @working_directory = ] 'working_directory' ]   
    [ , [ @use_ftp = ] 'use_ftp' ]   
    [ , [ @reserved = ] 'reserved' ]   
    [ , [ @use_interactive_resolver = ] 'use_interactive_resolver' ]   
    [ , [ @offloadagent = ] 'remote_agent_activation' ]   
    [ , [ @offloadserver = ] 'remote_agent_server_name']   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]  
    [ , [ @use_web_sync = ] use_web_sync ]  
        [ , [ @internet_url = ] 'internet_url' ]  
    [ , [ @internet_login = ] 'internet_login' ]  
        [ , [ @internet_password = ] 'internet_password' ]  
    [ , [ @internet_security_mode = ] internet_security_mode ]  
        [ , [ @internet_timeout = ] internet_timeout ]  
    [ , [ @hostname = ] 'hostname' ]  
        [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name =** ] **'***nombre***'**  
 Es el nombre del agente. *nombre* es **sysname**, su valor predeterminado es null.  
  
 [  **@publisher =** ] **'***publisher***'**  
 Es el nombre del servidor del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db =** ] **'***publisher_db***'**  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con un publicador durante la sincronización. *publisher_security_mode* es **int**, su valor predeterminado es 1. Si **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. Si **1**, especifica la autenticación de Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 Es el inicio de sesión que se debe utilizar al conectarse con un publicador durante la sincronización. *publisher_login* es **sysname**, su valor predeterminado es null.  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 Es la contraseña utilizada para conectarse al publicador. *publisher_password* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Cuando sea posible, pida a los usuarios que especifiquen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@publisher_encrypted_password =** ]*publisher_encrypted_password*  
 Establecer *publisher_encrypted_password* ya no se admite. Al intentar establecer esto **bit** parámetro **1** se producirá un error.  
  
 [  **@subscriber =** ] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_security_mode =** ] *subscriber_security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con un suscriptor durante la sincronización. *subscriber_security_mode* es **int**, su valor predeterminado es 1. Si **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. Si **1**, especifica la autenticación de Windows.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores. El Agente de mezcla siempre conecta con el suscriptor local mediante Autenticación de Windows. Si se especifica un valor para este parámetro, se devolverá un mensaje de advertencia, pero el valor se pasará por alto.  
  
 [  **@subscriber_login =** ] **'***subscriber_login***'**  
 Es el inicio de sesión del suscriptor que se debe utilizar al conectarse con un suscriptor durante la sincronización. *subscriber_login* es necesaria si *subscriber_security_mode* está establecido en **0**. *subscriber_login* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores. Si se especifica un valor para este parámetro, se devolverá un mensaje de advertencia, pero el valor se pasará por alto.  
  
 [  **@subscriber_password =** ] **'***subscriber_password***'**  
 Es la contraseña del suscriptor para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *subscriber_password* es necesaria si *subscriber_security_mode* está establecido en **0**. *subscriber_password* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores. Si se especifica un valor para este parámetro, se devolverá un mensaje de advertencia, pero el valor se pasará por alto.  
  
 [  **@distributor =** ] **'***distribuidor***'**  
 Es el nombre del distribuidor. *distribuidor* es **sysname**, su valor predeterminado es *publisher*; es decir, el publicador también es el distribuidor.  
  
 [  **@distributor_security_mode =** ] *distributor_security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con un distribuidor durante la sincronización. *distributor_security_mode* es **int**, su valor predeterminado es 0. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. **1** especifica autenticación de Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login =** ] **'***distributor_login***'**  
 Es el inicio de sesión del distribuidor que se debe utilizar al conectarse con un distribuidor durante la sincronización. *distributor_login* es necesaria si *distributor_security_mode* está establecido en **0**. *distributor_login* es **sysname**, su valor predeterminado es null.  
  
 [  **@distributor_password =** ] **'***distributor_password***'**  
 Es la contraseña del distribuidor. *distributor_password* es necesaria si *distributor_security_mode* está establecido en **0**. *distributor_password* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Cuando sea posible, pida a los usuarios que especifiquen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@encrypted_password =** ] *encrypted_password*  
 Establecer *encrypted_password* ya no se admite. Al intentar establecer esto **bit** parámetro **1** se producirá un error.  
  
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
 El día o los días que se ejecuta el agente de mezcla. *frequency_interval* es **int**, y puede tener uno de estos valores.  
  
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
 Es la fecha del Agente de mezcla. Este parámetro se utiliza cuando *frequency_type* está establecido en **32** (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de estos valores.  
  
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
 Es la frecuencia de repetición de la programación durante el periodo definido. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (predeterminado)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Es la hora del día en que el agente de mezcla se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 Es la hora del día en que el agente de mezcla deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Es la fecha en que el agente de mezcla se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Es la fecha en la que el agente de mezcla deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
 [  **@optional_command_line =** ] **'***optional_command_line***'**  
 Es un símbolo del sistema opcional proporcionado al Agente de mezcla. *optional_command_line* es **nvarchar (255)**, su valor predeterminado es ' '. Se puede utilizar para proporcionar parámetros adicionales al Agente de mezcla, como en el siguiente ejemplo, en el que se aumenta el tiempo de espera predeterminado de las consultas a `600` segundos.  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
 [  **@merge_jobid =** ] *merge_jobid*  
 Es el parámetro de salida del id. de trabajo. *merge_jobid* es **binary (16)**, su valor predeterminado es null.  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 Especifica si la suscripción se puede sincronizar mediante el Administrador de sincronización de Windows. *enabled_for_syncmgr* es **nvarchar (5)**, su valor predeterminado es False. Si **false**, la suscripción no está registrada con el Administrador de sincronización. Si **true**, la suscripción se registra con el Administrador de sincronización y se puede sincronizar sin iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 Se conserva únicamente por compatibilidad con versiones anteriores.  
  
 [  **@ftp_port =** ] *ftp_port*  
 Se conserva únicamente por compatibilidad con versiones anteriores.  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 Se conserva únicamente por compatibilidad con versiones anteriores.  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 Se conserva únicamente por compatibilidad con versiones anteriores.  
  
 [  **@alt_snapshot_folder =** ] **'***alternate_snapshot_folder***'**  
 Especifica la ubicación de la que se obtienen los archivos de instantáneas. *alternate_snapshot_folder* es **nvarchar (255)**, su valor predeterminado es null. Si es NULL, los archivos de instantáneas se recopilarán desde la ubicación predeterminada especificada por el publicador.  
  
 [  **@working_directory =** ] **'***working_directory***'**  
 Es el nombre del directorio de trabajo utilizado para almacenar temporalmente archivos de datos y esquema para la publicación cuando se utiliza FTP para transferir archivos de instantáneas. *working_directory* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@use_ftp =** ] **'***use_ftp***'**  
 Especifica que se utilizará FTP en lugar del protocolo normal para recuperar las instantáneas. *use_ftp* es **nvarchar (5)**, su valor predeterminado es False.  
  
 [  **@reserved =** ] **'***reservada***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@use_interactive_resolver =** ] **'***use_interactive_resolver***'** ]  
 Usa el solucionador interactivo para resolver conflictos de todos los artículos que permitan la resolución interactiva. *use_interactive_resolver* es **nvarchar (5)**, su valor predeterminado es False.  
  
 [  **@offloadagent =** ] **'***remote_agent_activation***'**  
 > [!NOTE]  
>  La activación remota del agente ha quedado desusada y ya no es compatible. Este parámetro solamente se admite por compatibilidad de scripts con versiones anteriores. Establecer *remote_agent_activation* a un valor distinto de **false** generará un error.  
  
 [  **@offloadserver =** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  La activación remota del agente ha quedado desusada y ya no es compatible. Este parámetro solamente se admite por compatibilidad de scripts con versiones anteriores. Establecer *remote_agent_server_name* en cualquier valor distinto de NULL, se generará un error.  
  
 [  **@job_name =** ] **'***job_name***'** ]  
 Es el nombre de un trabajo del agente existente. *job_name* es **sysname**, su valor predeterminado es null. Este parámetro solamente se especifica cuando la suscripción se va a sincronizar mediante un trabajo existente en lugar de uno recién creado (el valor predeterminado). Si no es un miembro de la **sysadmin** rol fijo de servidor, debe especificar *job_login* y *job_password* al especificar *job_name*.  
  
 [  **@dynamic_snapshot_location =** ] **'***dynamic_snapshot_location***'** ]  
 Es la ruta de acceso a la carpeta que los archivos de instantáneas se leerán desde si una instantánea de datos filtrados que se usará. *dynamic_snapshot_location* es **nvarchar (260)**, su valor predeterminado es null. Para más información, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [  **@use_web_sync =** ] *use_web_sync*  
 Indica que la sincronización web está habilitada. *use_web_sync* es **bit**, su valor predeterminado es 0. **1** especifica que se puede sincronizar la suscripción de extracción a través de internet mediante HTTP.  
  
 [  **@internet_url =** ] **'***internet_url***'**  
 Es la ubicación de la escucha de replicación (REPLISAPI.DLL) de la sincronización web. *internet_url* es **nvarchar (260)**, su valor predeterminado es null. *internet_url* es una dirección URL completa, en el formato `http://server.domain.com/directory/replisapi.dll`. Si el servidor está configurado para escuchar en un puerto que no sea el 80, también se debe proporcionar el número de puerto con el formato `http://server.domain.com:portnumber/directory/replisapi.dll`, donde `portnumber` representa al puerto.  
  
 [  **@internet_login =** ] **'***internet_login***'**  
 Es el inicio de sesión que utiliza el Agente de mezcla al conectarse al servidor web que hospeda la sincronización web utilizando autenticación básica HTTP. *internet_login* es **sysname**, su valor predeterminado es null.  
  
 [  **@internet_password =** ] **'***internet_password***'**  
 Es la contraseña que el Agente de mezcla utiliza cuando se conecta al servidor web que hospeda la sincronización web a través de la autenticación básica HTTP. *internet_password* es **nvarchar (524)**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [  **@internet_security_mode =** ] *internet_security_mode*  
 Es el método de autentificación usado por el Agente de mezcla al conectarse al servidor web durante la sincronización web mediante HTTPS. *internet_security_mode* es **int** y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Se utiliza Autenticación básica.|  
|**1** (predeterminado)|Se utiliza Autenticación integrada de Windows.|  
  
> [!NOTE]  
>  Se recomienda utilizar la autenticación básica con sincronización web. Para utilizar la sincronización web, es necesario realizar una conexión SSL al servidor web. Para más información, consulte [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
 [  **@internet_timeout =** ] *internet_timeout*  
 Es el tiempo que transcurre, en segundos, hasta que expira una solicitud de sincronización web. *internet_timeout* es **int**, su valor predeterminado es **300** segundos.  
  
 [  **@hostname =** ] **'***hostname***'**  
 Omite el valor de HOST_NAME() cuando esta función se utiliza en la cláusula WHERE de un filtro con parámetros. *nombre de host* es **sysname**, su valor predeterminado es null.  
  
 [  **@job_login =** ] **'***job_login***'**  
 Es el inicio de sesión de la cuenta de Windows en la que se ejecuta el agente. *job_login* es **nvarchar (257)**, no tiene ningún valor predeterminado. Esta cuenta de Windows siempre se utiliza para las conexiones del agente al suscriptor y para las conexiones al distribuidor y al publicador cuando se utiliza Autenticación integrada de Windows.  
  
 [  **@job_password =** ] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows en la que se ejecuta el agente. *job_password* es **sysname**, no tiene ningún valor predeterminado.  
  
> [!IMPORTANT]  
>  No almacene información de autenticación en archivos de script. Para una mayor seguridad, los nombres de inicio de sesión y las contraseñas se deben proporcionar en tiempo de ejecución.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergepullsubscription_agent** se utiliza en la replicación de mezcla y utiliza una funcionalidad similar a [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md).  
  
 Para obtener un ejemplo de cómo especificar correctamente la configuración de seguridad al ejecutar **sp_addmergepullsubscription_agent**, consulte [crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md).  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_addmergepullsubscription_agent**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
