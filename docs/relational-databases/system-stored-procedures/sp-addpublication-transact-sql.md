---
title: sp_addpublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
author: stevestein
ms.author: sstein
ms.openlocfilehash: f676acf9b3ee91bb5a1fb46cae2f7c693dc66983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061818"
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
`[ \@publication = ] 'publication'` Es el nombre de la publicación que se va a crear. *publicación* es **sysname**, no tiene ningún valor predeterminado. El nombre debe ser único dentro de la base de datos.  
  
`[ \@taskid = ] taskid` Admite por razones de compatibilidad; usar [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md).  
  
`[ \@restricted = ] 'restricted'` Admite por razones de compatibilidad; usar *default_access*.  
  
`[ \@sync_method = ] _'sync_method'` Es el modo de sincronización. *sync_method* es **nvarchar(13)** , y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**native**|Genera la salida de todas las tablas mediante un programa de copia masiva en modo nativo. *No se admite para publicadores de Oracle*.|  
|**character**|Genera la salida de todas las tablas mediante un programa de copia masiva en modo de caracteres. _Para un publicador de Oracle,_ **carácter** _sólo es válido para la replicación de instantáneas_.|  
|**concurrent**|Produce la salida de todas las tablas mediante un programa de copia masiva en modo nativo, pero no bloquea las tablas durante la instantánea. Solo se admite para publicaciones transaccionales. *No se admite para publicadores de Oracle*.|  
|**concurrent_c**|Produce la salida de todas las tablas mediante un programa de copia masiva en modo de carácter, pero no bloquea las tablas durante la instantánea. Solo se admite para publicaciones transaccionales.|  
|**Instantánea de base de datos**|Produce la salida de todas las tablas mediante un programa de copia masiva en modo nativo desde una instantánea de base de datos. Las instantáneas de base de datos no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|**carácter de la instantánea de base de datos**|Produce la salida de todas las tablas mediante un programa de copia masiva en modo de carácter desde una instantánea de base de datos. Las instantáneas de base de datos no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|NULL (predeterminado)|El valor predeterminado es **nativo** para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. Para que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, el valor predeterminado es **carácter** cuando el valor de *repl_freq* es **instantánea** y **concurrent_c** todos los demás casos.|  
  
`[ \@repl_freq = ] 'repl_freq'` Es el tipo de frecuencia de replicación, *repl_freq* es **nvarchar (10)** , y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**continua** (valor predeterminado)|El publicador proporciona la salida de todas las transacciones basadas en el registro. Para que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, esto requiere que *sync_method* establecerse **concurrent_c**.|  
|**snapshot**|El publicador solamente genera eventos de sincronización programados. Para que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, esto requiere que *sync_method* establecerse **carácter**.|  
  
`[ \@description = ] 'description'` Es una descripción opcional para la publicación. *descripción* es **nvarchar (255)** , su valor predeterminado es null.  
  
`[ \@status = ] 'status'` Especifica si los datos de la publicación están disponibles. *estado* es **nvarchar (8)** , y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**active**|Los datos de la publicación están inmediatamente disponibles para los suscriptores.|  
|**inactivo** (valor predeterminado)|Los datos de la publicación no están disponibles para los suscriptores la primera vez que se crea la publicación (pueden suscribirse, pero las suscripciones no se procesan).|  
  
 *No se admite para publicadores de Oracle*.  
  
`[ \@independent_agent = ] 'independent_agent'` Especifica si hay un agente de distribución independiente para esta publicación. *independent_agent* es **nvarchar (5)** , su valor predeterminado es False. Si **true**, hay un agente de distribución independiente para esta publicación. Si **false**, la publicación utiliza un agente de distribución compartido, y cada par de base de datos de publicador y suscriptor de base de datos tiene un único agente compartido.  
  
`[ \@immediate_sync = ] 'immediate_synchronization'` Especifica si los archivos de sincronización para la publicación se crean cada vez que se ejecuta el agente de instantáneas. *immediate_sync* es **nvarchar (5)** , su valor predeterminado es False. Si **true**, los archivos de sincronización se crean o se vuelve a crear cada vez que se ejecuta el agente de instantáneas. Los suscriptores pueden disponer inmediatamente de los archivos si el Agente de instantáneas ya ha terminado su tarea antes de crear la suscripción. Las nuevas suscripciones obtienen los últimos archivos de sincronización generados por la ejecución más reciente del Agente de instantáneas. *independent_agent* debe ser **true** para *immediate_sync* sea **true**. Si **false**, los archivos de sincronización se crean solo si hay nuevas suscripciones. Debe llamar a [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para cada suscripción cuando se agrega incrementalmente un artículo nuevo a una publicación existente. Los suscriptores no pueden recibir los archivos de sincronización después de suscribirse hasta que los Agentes de instantáneas hayan empezado y terminado.  
  
`[ \@enabled_for_internet = ] 'enabled_for_internet'` Especifica si la publicación está habilitada para Internet y determina si el protocolo de transferencia de archivos (FTP) puede usarse para transferir los archivos de instantáneas a un suscriptor. *enabled_for_internet* es **nvarchar (5)** , su valor predeterminado es False. Si **true**, los archivos de sincronización para la publicación se colocan en el directorio C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp. El usuario debe crear el directorio Ftp.  
  
`[ \@allow_push = ] 'allow_push'` Especifica si se pueden crear suscripciones de inserción para la publicación indicada. *allow_push* es **nvarchar (5)** , su valor predeterminado es TRUE, que permite suscripciones de inserción en la publicación.  
  
`[ \@allow_pull = ] 'allow_pull'` Especifica si se pueden crear suscripciones de extracción para la publicación indicada. *allow_pull* es **nvarchar (5)** , su valor predeterminado es False. Si **false**, no se permiten las suscripciones de extracción en la publicación.  
  
`[ \@allow_anonymous = ] 'allow_anonymous'` Especifica si se pueden crear suscripciones anónimas para la publicación indicada. *allow_anonymous* es **nvarchar (5)** , su valor predeterminado es False. Si **true**, *immediate_sync* también debe establecerse en **true**. Si **false**, no se admiten suscripciones anónimas en la publicación.  
  
`[ \@allow_sync_tran = ] 'allow_sync_tran'` Especifica si se permiten suscripciones de actualización inmediata en la publicación. *allow_sync_tran* es **nvarchar (5)** , su valor predeterminado es False. **True** es *no se admite para publicadores de Oracle*.  
  
`[ \@autogen_sync_procs = ] 'autogen_sync_procs'` Especifica si el procedimiento almacenado de sincronización para suscripciones de actualización se genera en el publicador. *autogen_sync_procs* es **nvarchar (5)** , y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**true**|Se define de forma automática cuando se habilita la actualización de suscripciones.|  
|**false**|Se define automáticamente cuando no se ha habilitado la actualización de suscripciones o para publicadores de Oracle.|  
|NULL (predeterminado)|El valor predeterminado es **true** cuando se habilita la actualización de las suscripciones y a **false** cuando no esté habilitada suscripciones de actualización.|  
  
> [!NOTE]  
>  El usuario proporcionó el valor de *autogen_sync_procs*serán reemplazadas según los valores especificados para *allow_queued_tran* y *allow_sync_tran*.  
  
`[ \@retention = ] retention` Es el período de retención en horas de actividad de la suscripción. *retención* es **int**, su valor predeterminado es 336 horas. Si una suscripción no ha estado activa durante el período de retención, expira y se quita. El valor puede ser mayor que el período máximo de retención de la base de datos de distribución utilizada por el publicador. Si **0**, las suscripciones conocidas de la publicación nunca expirará y se puede quitar el agente de limpieza de suscripción ha expirado.  
  
`[ \@allow_queued_tran = ] 'allow_queued_updating'` Habilita o deshabilita la cola de cambios en el suscriptor hasta que se pueden aplicar en el publicador. *allow_queued_updating* es **nvarchar (5)** con el valor predeterminado es FALSE. Si **false**, los cambios del suscriptor no se ponen en cola. **True** es *no se admite para publicadores de Oracle*.  
  
`[ \@snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'` Especifica si los archivos de instantánea se almacenan en la carpeta predeterminada. *snapshot_in_default_folder* es **nvarchar (5)** con el valor predeterminado es TRUE. Si **true**, los archivos de instantáneas pueden encontrarse en la carpeta predeterminada. Si **false**, los archivos de instantáneas se han almacenado en la ubicación alternativa especificada por *alternate_snapshot_folder*. Las ubicaciones alternativas pueden encontrarse en otro servidor, en una unidad de red o en medios extraíbles (tales como CD-ROM o discos extraíbles). También puede guardar los archivos de instantánea en un sitio FTP, para que el suscriptor los recupere más tarde. Tenga en cuenta que este parámetro puede ser true y seguir teniendo una ubicación la  **\@alt_snapshot_folder** parámetro. Esta combinación especifica que los archivos de instantáneas se almacenarán tanto en la ubicación predeterminada como en la alternativa.  
  
`[ \@alt_snapshot_folder = ] 'alternate_snapshot_folder'` Especifica la ubicación de la carpeta alternativa para la instantánea. *alternate_snapshot_folder* es **nvarchar (255)** con el valor predeterminado es NULL.  
  
`[ \@pre_snapshot_script = ] 'pre_snapshot_script'` Especifica un puntero a un **.sql** ubicación del archivo. *pre_snapshot_script* es **nvarchar (255),** con el valor predeterminado es NULL. El Agente de distribución ejecutará el script previo a la instantánea antes de la ejecución de cualquiera de los scripts de objetos replicados al aplicar la instantánea en un suscriptor. El script se ejecuta en el contexto de seguridad utilizado por el Agente de distribución al conectarse a la base de datos de suscripciones.  
  
`[ \@post_snapshot_script = ] 'post_snapshot_script'` Especifica un puntero a un **.sql** ubicación del archivo. *post_snapshot_script* es **nvarchar (255)** , su valor predeterminado es null. El Agente de distribución ejecutará el script posterior a la instantánea después de que se apliquen el resto de scripts de objetos replicados y datos durante la sincronización inicial. El script se ejecuta en el contexto de seguridad utilizado por el Agente de distribución al conectarse a la base de datos de suscripciones.  
  
`[ \@compress_snapshot = ] 'compress_snapshot'` Especifica que la instantánea que se escribe en el  **\@alt_snapshot_folder** ubicación está comprimida en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. *compress_snapshot* es **nvarchar (5)** , su valor predeterminado es False. **false** especifica que no se comprimirá la instantánea; **true** especifica que se comprimirá la instantánea. No se pueden comprimir los archivos de instantánea de más de 2 gigabytes (GB). Los archivos de instantánea comprimidos se descomprimen en la ubicación en la que se ejecuta el Agente de distribución; por lo general, se usan suscripciones de extracción con las instantáneas comprimidas para descomprimir los archivos en el suscriptor. La instantánea de la carpeta predeterminada no se puede comprimir.  
  
`[ \@ftp_address = ] 'ftp_address'` Es la dirección de red del servicio FTP para el distribuidor. *ftp_address* es **sysname**, su valor predeterminado es null. Especifica dónde se encuentran los archivos de instantánea de una publicación para que los recoja el Agente de distribución o el Agente de mezcla de un suscriptor. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener diferentes *ftp_address*. La publicación debe ser compatible con la propagación de instantáneas mediante FTP.  
  
`[ \@ftp_port = ] ftp_port` Es el número de puerto del servicio FTP para el distribuidor. *ftp_port* es **int**, su valor predeterminado es 21. Especifica dónde se encuentra para el agente de distribución o el agente de mezcla del suscriptor para recoger los archivos de instantáneas de publicación. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener su propio *ftp_port*.  
  
`[ \@ftp_subdirectory = ] 'ftp_subdirectory'` Especifica dónde estarán disponibles para el agente de distribución o el agente de mezcla del suscriptor para recoger si la publicación admite la propagación de instantáneas mediante FTP los archivos de instantáneas. *ftp_subdirectory* es **nvarchar (255)** , su valor predeterminado es null. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener su propio *ftp_subdirctory* o elegir que ningún subdirectorio, indicándolo con un valor NULL.  
  
`[ \@ftp_login = ] 'ftp_login'` Se usa el nombre de usuario para conectarse al servicio FTP. *ftp_login* es **sysname**, su valor predeterminado es anonymous.  
  
`[ \@ftp_password = ] 'ftp_password'` Es la contraseña de usuario utilizada para conectarse al servicio FTP. *ftp_password* es **sysname**, su valor predeterminado es null.  
  
`[ \@allow_dts = ] 'allow_dts'` Especifica que la publicación permite transformaciones de datos. Puede especificar un paquete DTS al crear una suscripción. *allow_transformable_subscriptions* es **nvarchar (5)** con el valor predeterminado es FALSE, que no permite transformaciones DTS. Cuando *allow_dts* es true, *sync_method* debe establecerse en **carácter** o **concurrent_c**.  
  
 **True** es *no se admite para publicadores de Oracle*.  
  
`[ \@allow_subscription_copy = ] 'allow_subscription_copy'` Habilita o deshabilita la capacidad de copiar las bases de datos de suscripciones suscriben a esta publicación. *allow_subscription_copy* es**nvarchar (5)** , su valor predeterminado es False.  
  
`[ \@conflict_policy = ] 'conflict_policy'` Especifica la directiva de resolución de conflictos seguida cuando se utiliza la opción de suscriptor de actualización en cola. *conflict_policy* es **nvarchar (100)** con el valor predeterminado es NULL, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**wins pub**|El publicador gana el conflicto|  
|**Sub reinit**|Reinicializar la suscripción.|  
|**Sub wins**|El suscriptor gana el conflicto|  
|NULL (predeterminado)|Si es NULL y la publicación es una publicación de instantáneas, la directiva predeterminada será **sub reinit**. Si es NULL y la publicación no es una publicación de instantáneas, el valor predeterminado se convierte en **wins pub**.|  
  
 *No se admite para publicadores de Oracle*.  
  
`[ \@centralized_conflicts = ] 'centralized_conflicts'` Especifica si los registros de conflictos se almacenan en el publicador. *centralized_conflicts* es **nvarchar (5)** , su valor predeterminado es true. Si **true**, los registros de conflictos se almacenan en el publicador. Si **false**, los registros de conflictos se almacenan tanto en el publicador y en el suscriptor que provocó el conflicto. *No se admite para publicadores de Oracle*.  
  
`[ \@conflict_retention = ] conflict_retention` Especifica el período de retención de conflictos, en días. Es el período de tiempo durante el que se almacenan los metadatos de conflictos para la replicación transaccional punto a punto y para las suscripciones de actualización en cola. *conflict_retention* es **int**, su valor predeterminado es 14. *No se admite para publicadores de Oracle*.  
  
`[ \@queue_type = ] 'queue_type'` Especifica el tipo de cola utilizado. *queue_type* es **nvarchar (10)** , su valor predeterminado es null, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**sql**|Utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar las transacciones.|  
|NULL (predeterminado)|El valor predeterminado es **sql**, que especifica que se use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar las transacciones.|  
  
> [!NOTE]  
>  La compatibilidad para utilizar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server ha dejado de incluirse. Si se especifica un valor de **msmq** dará como resultado una advertencia y la replicación establece automáticamente el valor en **sql**.  
  
 *No se admite para publicadores de Oracle*.  
  
`[ \@add_to_active_directory = ] 'add\to_active_directory'` Este parámetro ha quedado en desuso y solo se admite para la compatibilidad con versiones anteriores de las secuencias de comandos. Ya no se puede agregar información de publicación a [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
`[ \@logreader_job_name = ] 'logreader_agent_name'` Es el nombre de un trabajo de agente existente. *logreader_agent_name* es **sysname**, su valor predeterminado es null. Este parámetro se especifica solo cuando el Agente de registro del LOG utiliza un trabajo existente en lugar de otro nuevo que se esté creando.  
  
`[ \@qreader_job_name = ] 'queue_reader_agent_name'` Es el nombre de un trabajo de agente existente. *queue_reader_agent_name* es **sysname**, su valor predeterminado es null. Este parámetro se especifica solo cuando el Agente de lectura de cola utiliza un trabajo existente en lugar de otro nuevo que se esté creando.  
  
`[ \@publisher = ] 'publisher'` Especifica que no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse cuando se agrega a una publicación de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
`[ \@allow_initialize_from_backup = ] 'allow_initialize_from_backup'` Indica si los suscriptores pueden inicializar una suscripción a esta publicación desde una copia de seguridad en lugar de una instantánea inicial. *allow_initialize_from_backup* es **nvarchar (5)** , y puede tener uno de estos valores:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**true**|Habilita la inicialización desde una copia de seguridad.|  
|**false**|Deshabilita la inicialización desde una copia de seguridad.|  
|NULL (predeterminado)|El valor predeterminado es **true** para una publicación en una topología de replicación punto a punto y **false** para todas las demás publicaciones.|  
  
 Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!WARNING]  
>  Para evitar perder los datos del suscriptor, al utilizar **sp_addpublication** con `@allow_initialize_from_backup = N'true'`, utilice siempre `@immediate_sync = N'true'`.  
  
`[ \@replicate_ddl = ] replicate_ddl` Indica si se admite la replicación de esquema para la publicación. *replicate_ddl* es **int**, su valor predeterminado es **1** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores y **0** para que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. **1** indica que se replican instrucciones de DDL (lenguaje) de definición de datos ejecutadas en el publicador, y **0** indica que no se replican las instrucciones de DDL. *No se admite la replicación de esquema para los publicadores de Oracle.* Para más información, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 El  *\@replicate_ddl* se respeta el parámetro cuando una instrucción DDL agrega una columna. El  *\@replicate_ddl* parámetro se omite cuando una instrucción DDL modifica o quita una columna por los motivos siguientes.  
  
-   Cuando se quita una columna, sysarticlecolumns debe actualizarse para evitar que las nuevas instrucciones DML, que incluyen la columna quitada, lo que provocaría un error en el agente de distribución. El  *\@replicate_ddl* parámetro se omite porque la replicación siempre debe replicar el cambio de esquema.  
  
-   Cuando se modifica una columna, es posible que el tipo de datos de origen o la nulabilidad hayan cambiado, lo que hace que las instrucciones DML contengan un valor que quizás no sea compatible con la tabla en el suscriptor. Estas instrucciones DML pueden hacer que el agente de distribución genere un error. El  *\@replicate_ddl* parámetro se omite porque la replicación siempre debe replicar el cambio de esquema.  
  
-   Cuando una instrucción DDL agrega una nueva columna, sysarticlecolumns no incluye la nueva columna. Las instrucciones DML no intentarán replicar datos para la nueva columna. Se respeta el parámetro porque la DDL es aceptable se realice o no la replicación.  
  
`[ \@enabled_for_p2p = ] 'enabled_for_p2p'` Habilita la publicación para su uso en una topología de replicación punto a punto. *enabled_for_p2p* es **nvarchar (5)** , su valor predeterminado es False. **True** indica que la publicación admite la replicación punto a punto. Al establecer *enabled_for_p2p* a **true**, se aplican las restricciones siguientes:  
  
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
  
`[ \@publish_local_changes_only = ] 'publish_local_changes_only'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ \@enabled_for_het_sub = ] 'enabled_for_het_sub'` Habilita la publicación admitir que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores. *enabled_for_het_sub* es **nvarchar (5)** con un valor predeterminado es False. Un valor de **true** significa que admite la publicación que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores. Cuando *enabled_for_het_sub* es **true**, se aplican las restricciones siguientes:  
  
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
  
`[ \@p2p_conflictdetection = ] 'p2p_conflictdetection'` Permite que el agente de distribución detectar conflictos si la publicación está habilitada para replicación punto a punto. *p2p_conflictdetection* es **nvarchar (5)** con un valor predeterminado es true. Para más información, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
`[ \@p2p_originator_id = ] p2p_originator_id` Especifica un identificador para un nodo en una topología punto a punto. *p2p_originator_id* es **int**, su valor predeterminado es null. Este identificador se utiliza para la detección de conflictos si *p2p_conflictdetection* está establecida en TRUE. Especifique un identificador positivo distinto de cero que no se haya utilizado jamás en la topología. Para obtener una lista de identificadores que ya se ha utilizado, ejecute [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).  
  
`[ \@p2p_continue_onconflict = ] 'p2p_continue_onconflict'` Determina si el agente de distribución continúa procesando los cambios una vez detectado un conflicto. *p2p_continue_onconflict* es **nvarchar (5)** con un valor predeterminado es False.  
  
> [!CAUTION]  
>  Recomendamos que utilice el valor predeterminado de FALSE. Cuando esta opción está establecida en TRUE, el Agente de distribución intenta converger los datos en la topología aplicando la fila en conflicto del nodo que tiene el Id. de originador más alto. Este método no garantiza la convergencia. Debe asegurarse de que la topología sea coherente una vez detectado un conflicto. Para obtener más información, vea "Controlar los conflictos" en [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
  
`[ \@allow_partition_switch = ] 'allow_partition_switch'` Especifica si ALTER TABLE... Las instrucciones SWITCH se pueden ejecutar en la base de datos publicada. *allow_partition_switch* es **nvarchar (5)** con un valor predeterminado es False. Para obtener más información, vea [Replicar tablas e índices con particiones](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
`[ \@replicate_partition_switch = ] 'replicate_partition_switch'` Especifica si ALTER TABLE... Las instrucciones SWITCH que se ejecutan en la base de datos publicada se deberían replicar en los suscriptores. *replicate_partition_switch* es **nvarchar (5)** con un valor predeterminado es False. Esta opción es válida solo si *allow_partition_switch* está establecida en TRUE.  

## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addpublication** se utiliza en la replicación de instantáneas y transaccional.  
  
 Si existen varias publicaciones que publiquen el mismo objeto de base de datos, solo las publicaciones con un *replicate_ddl* valor **1** replicará ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION y Instrucciones ALTER TRIGGER de DDL. Sin embargo, todas las publicaciones que publiquen la columna quitada replicarán una instrucción ALTER TABLE DROP COLUMN de DDL.  
  
 Con la replicación DDL habilitada (*replicate_ddl* = **1**) para una publicación, con el fin de realizar sin replicación DDL cambios en la publicación, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) primero debe ejecutar para establecer *replicate_ddl* a **0**. Después de que se ha ejecutado las instrucciones de DDL sin replicación, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) puede ejecutarse de nuevo para volver a activar la replicación DDL.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_addpublication**. Los inicios de sesión que usan la autenticación de Windows deben tener una cuenta de usuario en la base de datos que represente su cuenta de usuario de Windows. No es suficiente con una cuenta de usuario que represente un grupo de Windows.  
  
## <a name="see-also"></a>Vea también  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
