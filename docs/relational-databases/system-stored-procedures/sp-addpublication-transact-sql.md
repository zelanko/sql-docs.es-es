---
title: sp_addpublication (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e47d331f57abede1d4b0e20ebba44cced109035
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una publicación de instantáneas o transaccional. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación que se va a crear. *publicación* es **sysname**, no tiene ningún valor predeterminado. El nombre debe ser único dentro de la base de datos.  
  
 [  **@taskid=**] *taskid*  
 Admite por razones de compatibilidad; usar [sp_addpublication_snapshot &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md).  
  
 [  **@restricted=**] **'***restringido***'**  
 Admite por razones de compatibilidad; usar *default_access*.  
  
 [  **@sync_method=**] *' sync_method***'**  
 Es el modo de sincronización. *sync_method* es **nvarchar(13)**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**nativo**|Genera la salida de todas las tablas mediante un programa de copia masiva en modo nativo. *No se admite en publicadores de Oracle*.|  
|**carácter**|Genera la salida de todas las tablas mediante un programa de copia masiva en modo de caracteres. *Para un publicador de Oracle,* **caracteres** *sólo es válido para la replicación de instantáneas*.|  
|**simultáneas**|Produce la salida de todas las tablas mediante un programa de copia masiva en modo nativo, pero no bloquea las tablas durante la instantánea. Solo se admite para publicaciones transaccionales. *No se admite en publicadores de Oracle*.|  
|**concurrent_c**|Produce la salida de todas las tablas mediante un programa de copia masiva en modo de carácter, pero no bloquea las tablas durante la instantánea. Solo se admite para publicaciones transaccionales.|  
|**instantánea de base de datos**|Produce la salida de todas las tablas mediante un programa de copia masiva en modo nativo desde una instantánea de base de datos. Las instantáneas de base de datos no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|**carácter de la instantánea de base de datos**|Produce la salida de todas las tablas mediante un programa de copia masiva en modo de carácter desde una instantánea de base de datos. Las instantáneas de base de datos no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|NULL (predeterminado)|Valor predeterminado es **nativo** para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. Para no -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, el valor predeterminado es **caracteres** cuando el valor de *repl_freq* es **instantánea** y a **concurrent_c** para todos los demás casos.|  
  
 [  **@repl_freq=**] **'***repl_freq***'**  
 Es el tipo de frecuencia de replicación, *repl_freq* es **nvarchar (10)**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**continuo** (valor predeterminado)|El publicador proporciona la salida de todas las transacciones basadas en el registro. Para no -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, esto requiere que *sync_method* establecerse en **concurrent_c**.|  
|**instantánea**|El publicador solamente genera eventos de sincronización programados. Para no -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, esto requiere que *sync_method* establecerse en **caracteres**.|  
  
 [  **@description=**] **'***descripción***'**  
 Es una descripción opcional de la publicación. *descripción* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@status=**] **'***estado***'**  
 Especifica si los datos de publicación están disponibles. *estado* es **nvarchar (8)**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Active**|Los datos de la publicación están inmediatamente disponibles para los suscriptores.|  
|**inactiva** (valor predeterminado)|Los datos de la publicación no están disponibles para los suscriptores la primera vez que se crea la publicación (pueden suscribirse, pero las suscripciones no se procesan).|  
  
 *No se admite en publicadores de Oracle*.  
  
 [  **@independent_agent=**] **'***independent_agent***'**  
 Especifica si hay un agente de distribución independiente para esta publicación. *independent_agent* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **true**, hay un agente de distribución independiente para esta publicación. Si **false**, la publicación utiliza un agente de distribución compartido, y cada par de base de datos de publicador y suscriptor de base de datos tiene un único agente compartido.  
  
 [  **@immediate_sync=**] **'***immediate_sync***'**  
 Especifica si los archivos de sincronización de la publicación se crean cada vez que se ejecuta el agente de instantáneas. *immediate_sync* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **true**, los archivos de sincronización se crean o se vuelven a crear cada vez que se ejecuta el agente de instantáneas. Los suscriptores pueden disponer inmediatamente de los archivos si el Agente de instantáneas ya ha terminado su tarea antes de crear la suscripción. Las nuevas suscripciones obtienen los últimos archivos de sincronización generados por la ejecución más reciente del Agente de instantáneas. *independent_agent* debe ser **true** para *immediate_sync* como **true**. Si **false**, los archivos de sincronización se crean solo si hay nuevas suscripciones. Debe llamar a [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para cada suscripción cuando se agrega incrementalmente un nuevo artículo a una publicación existente. Los suscriptores no pueden recibir los archivos de sincronización después de suscribirse hasta que los Agentes de instantáneas hayan empezado y terminado.  
  
 [  **@enabled_for_internet=**] **'***enabled_for_internet***'**  
 Especifica si la publicación está habilitada para Internet y determina si se puede utilizar el protocolo de transferencia de archivos (FTP) para transferir los archivos de instantánea a un suscriptor. *enabled_for_internet* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **true**, los archivos de sincronización para la publicación se colocan en el directorio C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp. El usuario debe crear el directorio Ftp.  
  
 [  **@allow_push=**] **'***allow_push***'**  
 Especifica si es posible crear suscripciones de inserción para la publicación indicada. *allow_push* es **nvarchar (5)**, su valor predeterminado es TRUE, que permite suscripciones de inserción en la publicación.  
  
 [  **@allow_pull=**] **'***allow_pull***'**  
 Especifica si es posible crear suscripciones de extracción para la publicación indicada. *allow_pull* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **false**, no se permiten las suscripciones de extracción en la publicación.  
  
 [  **@allow_anonymous=**] **'***allow_anonymous***'**  
 Especifica si es posible crear suscripciones anónimas para la publicación indicada. *allow_anonymous* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **true**, *immediate_sync* también debe establecerse en **true**. Si **false**, no se admiten suscripciones anónimas en la publicación.  
  
 [  **@allow_sync_tran=**] **'***allow_sync_tran***'**  
 Especifica si se permiten suscripciones de actualización inmediata en la publicación. *allow_sync_tran* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** es *no se admite en publicadores de Oracle*.  
  
 [  **@autogen_sync_procs=**] **'***autogen_sync_procs***'**  
 Especifica si se ha generado en el publicador un procedimiento almacenado de sincronización para suscripciones de actualización. *autogen_sync_procs* es **nvarchar (5)**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**true**|Se define de forma automática cuando se habilita la actualización de suscripciones.|  
|**false**|Se define automáticamente cuando no se ha habilitado la actualización de suscripciones o para publicadores de Oracle.|  
|NULL (predeterminado)|Valor predeterminado es **true** cuando se habilita la actualización de las suscripciones y a **false** cuando no esté habilitada suscripciones de actualización.|  
  
> [!NOTE]  
>  El usuario proporciona el valor para *autogen_sync_procs*serán reemplazadas según los valores especificados para *allow_queued_tran* y *allow_sync_tran*.  
  
 [  **@retention=**] *retención*  
 Es el período de retención, en horas, para la actividad de suscripción. *retención* es **int**, su valor predeterminado es 336 horas. Si una suscripción no ha estado activa durante el período de retención, expira y se quita. El valor puede ser mayor que el período máximo de retención de la base de datos de distribución utilizada por el publicador. Si **0**, las suscripciones conocidas de la publicación no expire nunca y puede quitar el agente de limpieza de suscripción caducada.  
  
 [  **@allow_queued_tran=** ] **'***allow_queued_updating***'**  
 Habilita o deshabilita la colocación en cola de los cambios del suscriptor hasta que se puedan aplicar en el publicador. *allow_queued_updating* es **nvarchar (5)** con un valor predeterminado es FALSE. Si **false**, cambios en el suscriptor no se ponen en cola. **True** es *no se admite en publicadores de Oracle*.  
  
 [  **@snapshot_in_defaultfolder=** ] **'***snapshot_in_default_folder***'**  
 Especifica si los archivos de instantánea se almacenan en la carpeta predeterminada. *snapshot_in_default_folder* es **nvarchar (5)** con un valor predeterminado es TRUE. Si **true**, archivos de instantáneas se pueden encontrar en la carpeta predeterminada. Si **false**, archivos de instantáneas se han almacenado en la ubicación alternativa especificada por *alternate_snapshot_folder*. Las ubicaciones alternativas pueden encontrarse en otro servidor, en una unidad de red o en medios extraíbles (tales como CD-ROM o discos extraíbles). También puede guardar los archivos de instantánea en un sitio FTP, para que el suscriptor los recupere más tarde. Tenga en cuenta que este parámetro puede ser true y seguir teniendo una ubicación la  **@alt_snapshot_folder**  parámetro. Esta combinación especifica que los archivos de instantáneas se almacenarán tanto en la ubicación predeterminada como en la alternativa.  
  
 [  **@alt_snapshot_folder=** ] **'***alternate_snapshot_folder***'**  
 Especifica la ubicación de la carpeta alternativa de la instantánea. *alternate_snapshot_folder* es **nvarchar (255)** con un valor predeterminado es NULL.  
  
 [  **@pre_snapshot_script=** ] **'***pre_snapshot_script***'**  
 Especifica un puntero a un **.sql** ubicación del archivo. *pre_snapshot_script* es **nvarchar (255),**con un valor predeterminado es NULL. El Agente de distribución ejecutará el script previo a la instantánea antes de la ejecución de cualquiera de los scripts de objetos replicados al aplicar la instantánea en un suscriptor. El script se ejecuta en el contexto de seguridad utilizado por el Agente de distribución al conectarse a la base de datos de suscripciones.  
  
 [  **@post_snapshot_script=** ] **'***post_snapshot_script***'**  
 Especifica un puntero a un **.sql** ubicación del archivo. *post_snapshot_script* es **nvarchar (255)**, su valor predeterminado es null. El Agente de distribución ejecutará el script posterior a la instantánea después de que se apliquen el resto de scripts de objetos replicados y datos durante la sincronización inicial. El script se ejecuta en el contexto de seguridad utilizado por el Agente de distribución al conectarse a la base de datos de suscripciones.  
  
 [  **@compress_snapshot=** ] **'***compress_snapshot***'**  
 Especifica que la instantánea que se escribe en el  **@alt_snapshot_folder**  ubicación está comprimida en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. *compress_snapshot* es **nvarchar (5)**, con un valor predeterminado es FALSE. **false** especifica que no se comprimirá la instantánea; **true** especifica que se comprimirá la instantánea. No se pueden comprimir los archivos de instantánea de más de 2 gigabytes (GB). Los archivos de instantánea comprimidos se descomprimen en la ubicación en la que se ejecuta el Agente de distribución; por lo general, se usan suscripciones de extracción con las instantáneas comprimidas para descomprimir los archivos en el suscriptor. La instantánea de la carpeta predeterminada no se puede comprimir.  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 Es la dirección de red del servicio FTP para el distribuidor. *ftp_address* es **sysname**, su valor predeterminado es null. Especifica dónde se encuentran los archivos de instantánea de una publicación para que los recoja el Agente de distribución o el Agente de mezcla de un suscriptor. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener diferentes *ftp_address*. La publicación debe ser compatible con la propagación de instantáneas mediante FTP.  
  
 [  **@ftp_port=** ] *ftp_port*  
 Es el número de puerto del servicio FTP para el distribuidor. *ftp_port* es **int**, su valor predeterminado es 21. Especifica dónde se encuentran el agente de distribución o el agente de mezcla de un suscriptor para recoger los archivos de instantáneas de publicación. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener su propio *ftp_port*.  
  
 [  **@ftp_subdirectory =** ] **'***ftp_subdirectory***'**  
 Especifica dónde estarán disponibles los archivos de instantánea para que los recoja el Agente de distribución o el Agente de mezcla del suscriptor si la publicación admite la propagación de instantáneas mediante FTP. *ftp_subdirectory* es **nvarchar (255)**, su valor predeterminado es null. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener su propio *ftp_subdirctory* o elegir no tener subdirectorio, indicándolo con un valor NULL.  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 Es el nombre de usuario que se utiliza para conectar con el servicio FTP. *ftp_login* es **sysname**, con un valor predeterminado es ANONYMOUS.  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 Es la contraseña del usuario que se utiliza para conectarse al servicio FTP. *ftp_password* es **sysname**, su valor predeterminado es null.  
  
 [  **@allow_dts =** ] **'***allow_dts***'**  
 Especifica que la publicación permite transformaciones de datos. Puede especificar un paquete DTS al crear una suscripción. *allow_transformable_subscriptions* es **nvarchar (5)** con el valor predeterminado es FALSE, que no permite transformaciones DTS. Cuando *allow_dts* es true, *sync_method* debe establecerse en **caracteres** o **concurrent_c**.  
  
 **True** es *no se admite en publicadores de Oracle*.  
  
 [  **@allow_subscription_copy =** ] **'***allow_subscription_copy***'**  
 Habilita o deshabilita la funcionalidad de copia de las bases de datos de suscripciones suscritas a esta publicación. *allow_subscription_copy* es**nvarchar (5)**, con un valor predeterminado es FALSE.  
  
 [  **@conflict_policy =** ] **'***conflict_policy***'**  
 Especifica la directiva de resolución de conflictos seguida cuando se utiliza la opción de suscriptor de actualización en cola. *conflict_policy* es **nvarchar (100)** con un valor predeterminado es NULL y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**wins pub**|El publicador gana el conflicto|  
|**Sub reinit**|Reinicializar la suscripción.|  
|**Sub wins**|El suscriptor gana el conflicto|  
|NULL (predeterminado)|Si es NULL y se trata de una publicación de instantáneas, la directiva predeterminada será **sub reinit**. Si es NULL y la publicación no es una publicación de instantáneas, la directiva predeterminada será **wins pub**.|  
  
 *No se admite en publicadores de Oracle*.  
  
 [  **@centralized_conflicts =** ] **'***centralized_conflicts***'**  
 Especifica si los registros de conflictos se almacenan en el publicador. *centralized_conflicts* es **nvarchar (5)**, con un valor predeterminado es TRUE. Si **true**, los registros de conflictos se almacenan en el publicador. Si **false**, los registros de conflictos se almacenan tanto en el publicador y en el suscriptor que provocó el conflicto. *No se admite en publicadores de Oracle*.  
  
 [  **@conflict_retention =** ] *conflict_retention*  
 Especifica el período de retención de conflictos, en días. Es el período de tiempo durante el que se almacenan los metadatos de conflictos para la replicación transaccional punto a punto y para las suscripciones de actualización en cola. *conflict_retention* es **int**, su valor predeterminado es 14. *No se admite en publicadores de Oracle*.  
  
 [  **@queue_type =** ] **'***queue_type***'**  
 Especifica el tipo de cola utilizado. *queue_type* es **nvarchar (10)**, su valor predeterminado es null y puede tener uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**SQL**|Utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar las transacciones.|  
|NULL (predeterminado)|Valor predeterminado es **sql**, que especifica que se use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar las transacciones.|  
  
> [!NOTE]  
>  La compatibilidad para utilizar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server ha dejado de incluirse. Especifica el valor de **msmq** dará como resultado una advertencia y la replicación establecerá automáticamente el valor **sql**.  
  
 *No se admite en publicadores de Oracle*.  
  
 [  **@add_to_active_directory =** ] **'***agregar**_**to_active_directory***'**  
 Este parámetro ha quedado desusado y solo se admite para la compatibilidad de scripts con versiones anteriores. Ya no se puede agregar información de publicación a [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
 [  **@logreader_job_name =** ] **'***logreader_agent_name***'**  
 Es el nombre de un trabajo del agente existente. *logreader_agent_name* es **sysname**, su valor predeterminado es null. Este parámetro se especifica solo cuando el Agente de registro del LOG utiliza un trabajo existente en lugar de otro nuevo que se esté creando.  
  
 [  **@qreader_job_name =** ] **'***queue_reader_agent_name***'**  
 Es el nombre de un trabajo del agente existente. *queue_reader_agent_name* es **sysname**, su valor predeterminado es null. Este parámetro se especifica solo cuando el Agente de lectura de cola utiliza un trabajo existente en lugar de otro nuevo que se esté creando.  
  
 [  **@publisher =** ] **'***publisher***'**  
 Especifica un no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse cuando se agrega una publicación para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
 [  **@allow_initialize_from_backup =** ] **'***allow_initialize_from_backup***'**  
 Indica si los suscriptores pueden inicializar una suscripción a esta publicación a partir de una copia de seguridad en lugar de una instantánea inicial. *allow_initialize_from_backup* es **nvarchar (5)**, y puede tener uno de estos valores:  
  
|Valor|Description|  
|-----------|-----------------|  
|**true**|Habilita la inicialización desde una copia de seguridad.|  
|**false**|Deshabilita la inicialización desde una copia de seguridad.|  
|NULL (predeterminado)|Valor predeterminado es **true** para una publicación en una topología de replicación punto a punto y **false** para todas las demás publicaciones.|  
  
 Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!WARNING]  
>  Para evitar perder los datos del suscriptor, al utilizar **sp_addpublication** con `@allow_initialize_from_backup = N'true'`, utilice siempre `@immediate_sync = N'true'`.  
  
 [  **@replicate_ddl =** ] *replicate_ddl*  
 Indica si la publicación admite replicación de esquema. *replicate_ddl* es **int**, su valor predeterminado es **1** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores y **0** para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. **1** indica que se replican instrucciones de DDL (lenguaje) de definición de datos ejecutadas en el publicador, y **0** indica que no se replican las instrucciones de DDL. *La replicación del esquema no se admite en publicadores de Oracle.* Para más información, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 El  *@replicate_ddl*  parámetro se observa cuando una instrucción DDL agrega una columna. El  *@replicate_ddl*  parámetro se ignora cuando una instrucción DDL modifica o quita una columna por las razones siguientes.  
  
-   Cuando se quita una columna, sysarticlecolumns debe actualizarse para evitar que las nuevas instrucciones DML incluyan la columna quitada lo que haría que el agente de distribución genere un error. El  *@replicate_ddl*  parámetro se ignora porque la replicación siempre debe replicar el cambio de esquema.  
  
-   Cuando se modifica una columna, es posible que el tipo de datos de origen o la nulabilidad hayan cambiado, lo que hace que las instrucciones DML contengan un valor que quizás no sea compatible con la tabla en el suscriptor. Estas instrucciones DML pueden hacer que el agente de distribución genere un error. El  *@replicate_ddl*  parámetro se ignora porque la replicación siempre debe replicar el cambio de esquema.  
  
-   Cuando una instrucción DDL agrega una nueva columna, sysarticlecolumns no incluye la nueva columna. Las instrucciones DML no intentarán replicar datos para la nueva columna. Se respeta el parámetro porque la DDL es aceptable se realice o no la replicación.  
  
 [  **@enabled_for_p2p =** ] **'***enabled_for_p2p***'**  
 Permite utilizar la publicación en una topología de replicación punto a punto. *enabled_for_p2p* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** indica que la publicación admite la replicación punto a punto. Al establecer *enabled_for_p2p* a **true**, se aplican las restricciones siguientes:  
  
-   *allow_anonymous* debe ser **false**.  
  
-   *allow_dts* debe ser **false**.  
  
-   *allow_initialize_from_backup* debe ser **true**.  
  
-   *allow_queued_tran* debe ser **false**.  
  
-   *allow_sync_tran* debe ser **false**.  
  
-   *conflict_policy* debe ser **false**.  
  
-   *independent_agent* debe ser **true**.  
  
-   *repl_freq* debe ser **continua**.  
  
-   *replicate_ddl* debe ser **1**.  
  
 Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 [  **@publish_local_changes_only =** ] **'***publish_local_changes_only***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@enabled_for_het_sub=** ] **'***enabled_for_het_sub***'**  
 Habilita la publicación para que admita suscriptores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *enabled_for_het_sub* es **nvarchar (5)** con un valor predeterminado de FALSE. Un valor de **true** significa que la publicación admite no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores. Cuando *enabled_for_het_sub* es **true**, se aplican las restricciones siguientes:  
  
-   *allow_initialize_from_backup* debe ser **false**.  
  
-   *allow_push* debe ser **true**.  
  
-   *allow_queued_tran* debe ser **false**.  
  
-   *allow_subscription_copy* debe ser **false**.  
  
-   *allow_sync_tran* debe ser **false**.  
  
-   *autogen_sync_procs* debe ser **false**.  
  
-   *conflict_policy* debe ser NULL.  
  
-   *enabled_for_internet* debe ser **false**.  
  
-   *enabled_for_p2p* debe ser **false**.  
  
-   *ftp_address* debe ser NULL.  
  
-   *ftp_subdirectory* debe ser NULL.  
  
-   *ftp_password* debe ser NULL.  
  
-   *pre_snapshot_script* debe ser NULL.  
  
-   *post_snapshot_script* debe ser NULL.  
  
-   *replicate_ddl* debe ser 0.  
  
-   *qreader_job_name* debe ser NULL.  
  
-   *queue_type* debe ser NULL.  
  
-   *sync_method* no puede ser **nativo** o **simultáneas**.  
  
 Para más información, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 [  **@p2p_conflictdetection=** ] **'***p2p_conflictdetection***'**  
 Habilita el agente de distribución para detectar conflictos si la publicación está habilitada para la replicación punto a punto. *p2p_conflictdetection* es **nvarchar (5)** con un valor predeterminado es true. Para obtener más información, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [  **@p2p_originator_id=** ] *p2p_originator_id*  
 Especifica un Id. para un nodo en una topología punto a punto. *p2p_originator_id* es **int**, su valor predeterminado es null. Este identificador se utiliza para la detección de conflictos si *p2p_conflictdetection* está establecida en TRUE. Especifique un identificador positivo distinto de cero que no se haya utilizado jamás en la topología. Para obtener una lista de identificadores que ya se ha usado, ejecutar [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).  
  
 [  **@p2p_continue_onconflict=** ] **'***p2p_continue_onconflict***'**  
 Determina si el Agente de distribución continúa procesando los cambios después de la detección de un conflicto. *p2p_continue_onconflict* es **nvarchar (5)** con un valor predeterminado de FALSE.  
  
> [!CAUTION]  
>  Recomendamos que utilice el valor predeterminado de FALSE. Cuando esta opción está establecida en TRUE, el Agente de distribución intenta converger los datos en la topología aplicando la fila en conflicto del nodo que tiene el Id. de originador más alto. Este método no garantiza la convergencia. Debe asegurarse de que la topología sea coherente una vez detectado un conflicto. Para obtener más información, vea "Controlar los conflictos" en [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [  **@allow_partition_switch=** ] **'***allow_partition_switch***'**  
 Especifica si las instrucciones ALTER TABLE...SWITCH se pueden ejecutar con la base de datos publicada. *allow_partition_switch* es **nvarchar (5)** con un valor predeterminado de FALSE. Para obtener más información, vea [Replicar tablas e índices con particiones](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
 [  **@replicate_partition_switch=** ] **'***replicate_partition_switch***'**  
 Especifica si las instrucciones ALTER TABLE...SWITCH que se ejecutan con la base de datos publicada se deben replicar en los suscriptores. *replicate_partition_switch* es **nvarchar (5)** con un valor predeterminado de FALSE. Esta opción es válida sólo si *allow_partition_switch* está establecida en TRUE.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addpublication** se utiliza en la replicación de instantáneas y transaccional.  
  
 Si existen varias publicaciones que publicar el mismo objeto de base de datos, solamente las publicaciones con un *replicate_ddl* valo **1** replicará ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION y Instrucciones ALTER TRIGGER de DDL. Sin embargo, todas las publicaciones que publiquen la columna quitada replicarán una instrucción ALTER TABLE DROP COLUMN de DDL.  
  
 Con la replicación DDL habilitada (*replicate_ddl* = **1**) para una publicación, con el fin de realizar sin replicación DDL cambios en la publicación, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) primero debe ejecutar para establecer *replicate_ddl* a **0**. Una vez que se han ejecutado las instrucciones de DDL sin replicación, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) puede ejecutarse de nuevo para volver a activar la replicación DDL.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addpublication**. Los inicios de sesión que usan la autenticación de Windows deben tener una cuenta de usuario en la base de datos que represente su cuenta de usuario de Windows. No es suficiente con una cuenta de usuario que represente un grupo de Windows.  
  
## <a name="see-also"></a>Vea también  
 [sp_addlogreader_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
