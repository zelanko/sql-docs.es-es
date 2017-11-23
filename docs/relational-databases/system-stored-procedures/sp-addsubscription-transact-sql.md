---
title: sp_addsubscription (Transact-SQL) | Documentos de Microsoft
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addsubscription
- sp_addsubscription_TSQL
helpviewer_keywords: sp_addsubscription
ms.assetid: 61ddf287-1fa0-4c1a-8657-ced50cebf0e0
caps.latest.revision: "53"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 860f2f99457344167af9035d0a9ccc21eebc2577
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddsubscription-transact-sql"></a>sp_addsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega una suscripción a una publicación y define el estado del suscriptor. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addsubscription [ @publication = ] 'publication'  
    [ , [ @article = ] 'article']  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
        [ , [ @sync_type = ] 'sync_type' ]  
    [ , [ @status = ] 'status'  
        [ , [ @subscription_type = ] 'subscription_type' ]  
    [ , [ @update_mode = ] 'update_mode' ]  
    [ , [ @loopback_detection = ] 'loopback_detection' ]  
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
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
    [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @backupdevicetype = ] 'backupdevicetype' ]  
    [ , [ @backupdevicename = ] 'backupdevicename' ]  
    [ , [ @mediapassword = ] 'mediapassword' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @fileidhint = ] fileidhint ]  
    [ , [ @unload = ] unload ]  
    [ , [ @subscriptionlsn = ] subscriptionlsn ]  
    [ , [ @subscriptionstreams = ] subscriptionstreams ]  
    [ , [ @subscriber_type = ] subscriber_type ]  
    [ , [ @memory_optimized = ] memory_optimized ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication=] '*publicación*'  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ @article=] '*artículo*'  
 Es el artículo al que está suscrita la publicación. *artículo* es **sysname**, con un valor predeterminado es all. Si el valor es all, se agrega una suscripción a todos los artículos de esa publicación. Los publicadores de Oracle solo admiten los valores all o NULL.  
  
 [ @subscriber=] '*suscriptor*'  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null.  
  
 [ @destination_db=] '*destination_db*'  
 Es el nombre de la base de datos de destino en la que se colocan los datos replicados. *destination_db* es **sysname**, su valor predeterminado es null. Si es NULL, *destination_db* se establece en el nombre de la base de datos de publicación. Para los publicadores de Oracle, *destination_db* debe especificarse. Para un suscriptor no SQL Server, especifique un valor de (destino predeterminado) para *destination_db*.  
  
 [ @sync_type=] '*sync_type*'  
 Es el tipo de sincronización de suscripción. *sync_type* es **nvarchar (255)**, y puede tener uno de los siguientes valores:  
  
|Valor|Description|  
|-----------|-----------------|  
|none|El suscriptor tiene ya el esquema y los datos iniciales de las tablas publicadas.<br /><br /> Nota: Esta opción está en desuso. En su lugar, utilice replication support only.|  
|automatic (predeterminado)|El esquema y los datos iniciales de las tablas publicadas se transfieren primero al suscriptor.|  
|replication support only|Proporciona la generación automática en el suscriptor de los desencadenadores y procedimientos almacenados personalizados de artículos que admiten las suscripciones de actualización, si es apropiado. Supone que el suscriptor tiene ya el esquema y los datos iniciales de las tablas publicadas. Al configurar una topología de replicación transaccional punto a punto, asegúrese de que los datos de todos los nodos de la topología son idénticos. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).<br /><br /> *No se admite para las suscripciones a publicaciones que no sea SQL Server.*|  
|initialize with backup|El esquema y los datos iniciales de las tablas publicadas se obtienen de una copia de seguridad de la base de datos de publicaciones. Se da por supuesto que el suscriptor tiene acceso a una copia de seguridad de la base de datos de publicaciones. La ubicación de la copia de seguridad y tipo de medio para la copia de seguridad se especifica mediante *backupdevicename* y *backupdevicetype*. Cuando se utiliza esta opción, la topología de replicación transaccional punto a punto no debe detenerse durante la configuración.<br /><br /> *No se admite para las suscripciones a publicaciones que no sea SQL Server.*|  
|initialize from lsn|Se utiliza cuando se agrega un nodo a una topología de replicación transaccional punto a punto. Se usa con @subscriptionlsn para asegurarse de que todas las transacciones pertinentes se repliquen en el nuevo nodo. Supone que el suscriptor tiene ya el esquema y los datos iniciales de las tablas publicadas. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
> [!NOTE]  
>  Las tablas y los datos del sistema se transfieren siempre.  
  
 [ @status=] '*estado*'  
 Es el estado de la suscripción. *estado* es **sysname**, su valor predeterminado es null. Si este parámetro no se establece de forma explícita, la replicación lo establece automáticamente en uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|active|La suscripción está inicializada y lista para aceptar cambios. Esta opción se establece cuando el valor de *sync_type* es, inicialización con una copia de seguridad o solo compatibilidad con replicación.|  
|subscribed|La suscripción debe inicializarse. Esta opción se establece cuando el valor de *sync_type* es automático.|  
  
 [ @subscription_type=] '*subscription_type*'  
 Es el tipo de suscripción. *subscription_type* es **nvarchar (4)**, con un valor predeterminado es push. Puede ser de inserción o de extracción. Los agentes de distribución de suscripciones de inserción residen en el distribuidor y los agentes de distribución de suscripciones de extracción residen en el suscriptor. *subscription_type* puede ser de extracción para crear una suscripción de extracción con nombre conocida para el publicador. Para obtener más información, vea [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md).  
  
> [!NOTE]  
>  Las suscripciones anónimas no necesitan utilizar este procedimiento almacenado.  
  
 [ @update_mode=] '*update_mode*'  
 Es el tipo de actualización. *update_mode* es **nvarchar (30)**, y puede tener uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|read only (predeterminado)|La suscripción es de solo lectura. Los cambios en el suscriptor no se envían al publicador.|  
|sync tran|Habilita la compatibilidad con las suscripciones de actualización inmediata. No es compatible con publicadores de Oracle.|  
|queued tran|Permite la actualización en cola de la suscripción. Las modificaciones de los datos se realizan en el suscriptor, se almacenan en una cola y después se propagan al publicador. No es compatible con publicadores de Oracle.|  
|failover|Permite la actualización inmediata de las suscripciones con la actualización en cola como conmutación por error. Las modificaciones de los datos se pueden realizar en el suscriptor y propagarse inmediatamente al publicador. Si el publicador y el suscriptor no están conectados, el modo de actualización se puede cambiar para que las modificaciones de los datos realizadas en el suscriptor se almacenen en una cola hasta que el suscriptor y el publicador vuelvan a conectarse. No es compatible con publicadores de Oracle.|  
|queued failover|Habilita la suscripción como una suscripción de actualización en cola con la capacidad de cambiar al modo de actualización inmediata. Las modificaciones de los datos se pueden realizar en el suscriptor y almacenarse en una cola hasta que se establezca una conexión entre el suscriptor y el publicador. Cuando se establece una conexión continua, el modo de actualización puede cambiar a actualización inmediata. No es compatible con publicadores de Oracle.|  
  
 Tenga en cuenta que los valores synctran y queued tran no se permiten si la publicación que se está suscribiendo permite DTS.  
  
 [ @loopback_detection=] '*el argumento loopback_detection*'  
 Especifica si el agente de distribución envía transacciones originadas en el suscriptor al mismo suscriptor. *el argumento loopback_detection* es **nvarchar (5)**, y puede tener uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|true|El Agente de distribución no envía las transacciones originadas en el suscriptor al mismo suscriptor. Se utilizan con replicación transaccional bidireccional. Para más información, consulte [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).|  
|false|El Agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor.|  
|NULL (predeterminado)|Se establece automáticamente en true para un suscriptor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en false para un suscriptor que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 [ @frequency_type=] *frequency_type*  
 Es la frecuencia con que se programa la tarea de distribución. *frequency_type* es de tipo int y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|1|Una vez|  
|2|A petición|  
|4|Cada día|  
|8|Programación semanal|  
|16|Programación mensual|  
|32|Mensualmente relativa|  
|64 (valor predeterminado)|Iniciar automáticamente|  
|128|Periódica|  
  
 [ @frequency_interval=] *frequency_interval*  
 Es el valor que se aplican a la frecuencia establecida por *frequency_type*. *frequency_interval* es **int**, su valor predeterminado es null.  
  
 [ @frequency_relative_interval=] *frequency_relative_interval*  
 Es la fecha del Agente de distribución. Este parámetro se utiliza cuando *frequency_type* está establecido en 32 (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|1|Primero|  
|2|Second|  
|4|Tercero|  
|8|Cuarto|  
|16|Último|  
|NULL (predeterminado)||  
  
 [ @frequency_recurrence_factor=] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es null.  
  
 [ @frequency_subday=] *frequency_subday*  
 Indica la frecuencia, en minutos, con que se reprograma durante el período definido. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|1|Una vez|  
|2|Second|  
|4|Minute|  
|8|Hour|  
|NULL||  
  
 [ @frequency_subday_interval=] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
 [ @active_start_time_of_day=] *active_start_time_of_day*  
 Es la hora del día en que el agente de distribución se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [ @active_end_time_of_day=] *active_end_time_of_day*  
 Es la hora del día en que el agente de distribución deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
 [ @active_start_date=] *active_start_date*  
 Es la fecha en que el agente de distribución se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [ @active_end_date=] *active_end_date*  
 Es la fecha en la que el agente de distribución deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
 [ @optional_command_line=] '*optional_command_line*'  
 Es el símbolo del sistema opcional que se va a ejecutar. *optional_command_line* es **nvarchar (4000)**, su valor predeterminado es null.  
  
 [ @reserved=] '*reservada*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @enabled_for_syncmgr=] '*enabled_for_syncmgr*'  
 Indica si se puede sincronizar la suscripción a través de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Administrador de sincronización de Windows. *enabled_for_syncmgr* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si el valor es false, la suscripción no se registra con el Administrador de sincronización de Windows. Si el valor es true, la suscripción se registra con el Administrador de sincronización de Windows y se puede sincronizar sin iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No es compatible con publicadores de Oracle.  
  
 [ @offloadagent=] '*remote_agent_activation*'  
 Especifica que el agente puede activarse de manera remota. *remote_agent_activation* es **bits** con un valor predeterminado es 0.  
  
> [!NOTE]  
>  Este parámetro ha quedado desusado y solamente se mantiene por compatibilidad con versiones anteriores de scripts.  
  
 [ @offloadserver=] '*remote_agent_server_name*'  
 Especifica el nombre de red del servidor que se utilizará en la activación remota. *remote_agent_server_name*es **sysname**, su valor predeterminado es null.  
  
 [ @dts_package_name=] '*dts_package_name*'  
 Especifica el nombre del paquete de Servicios de transformación de datos (DTS). *dts_package_name* es un **sysname** con un valor predeterminado es NULL. Por ejemplo, para especificar un paquete DTSPub_Package, el parámetro sería `@dts_package_name = N'DTSPub_Package'`. Este parámetro está disponible para suscripciones de inserción. Paga agregar información de un paquete DTS a una suscripción de extracción, utilice sp_addpullsubscription_agent.  
  
 [ @dts_package_password=] '*dts_package_password*'  
 Especifica la contraseña del paquete, si procede. *dts_package_password* es **sysname** con un valor predeterminado es NULL.  
  
> [!NOTE]  
>  Debe especificar una contraseña si *dts_package_name* se especifica.  
  
 [ @dts_package_location=] '*dts_package_location*'  
 Especifica la ubicación del paquete. *dts_package_location* es un **tipo (12)**, su valor predeterminado del distribuidor. La ubicación del paquete puede ser distributor o subscriber.  
  
 [ @distribution_job_name=] '*distribution_job_name*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @publisher=] '*publisher*'  
 Especifica un no[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no se debe especificar para una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
 [ @backupdevicetype=] '*backupdevicetype*'  
 Especifica el tipo de dispositivo de copia de seguridad utilizado al inicializar un suscriptor a partir una copia de seguridad. *backupdevicetype* es **nvarchar (20)**, y puede tener uno de estos valores:  
  
|Valor|Description|  
|-----------|-----------------|  
|logical (predeterminado)|El dispositivo de copia de seguridad es un dispositivo lógico.|  
|disk|El dispositivo de copia de seguridad es una unidad de disco.|  
|tape|El dispositivo de copia de seguridad es una unidad de cinta.|  
  
 *backupdevicetype* solamente se utiliza cuando *sync_method*está establecido en initialize_with_backup.  
  
 [ @backupdevicename=] '*backupdevicename*'  
 Especifica el nombre del dispositivo utilizado al inicializar un suscriptor a partir de una copia de seguridad. *backupdevicename* es **nvarchar (1000)**, su valor predeterminado es null.  
  
 [ @mediapassword=] '*mediapassword*'  
 Especifica una contraseña para el conjunto de medios si esta se estableció al dar formato a los medios. *MEDIAPASSWORD* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 [ @password=] '*contraseña*'  
 Especifica una contraseña para la copia de seguridad si esta se estableció al crear la copia de seguridad. *contraseña*es **sysname**, su valor predeterminado es null.  
  
 [ @fileidhint=] *fileidhint*  
 Identifica un valor ordinal del conjunto de copia de seguridad que se va a restaurar. *fileidhint* es **int**, su valor predeterminado es null.  
  
 [ @unload=] *descargar*  
 Especifica si un dispositivo de copia de seguridad en cinta se debe descargar una vez completada la inicialización a partir de la copia de seguridad. *descargar* es **bits**, con un valor predeterminado de 1. 1 especifica que la cinta debe descargarse. *descargar* solamente se utiliza cuando *backupdevicetype* es una cinta.  
  
 [ @subscriptionlsn=] *subscriptionlsn*  
 Especifica el número de flujo de registro (LSN) en el que una suscripción debería empezar a entregar cambios a un nodo en una topología de replicación transaccional punto a punto. Usar con un @sync_type valor de initialize from lsn para asegurarse de que todas las transacciones pertinentes se replican en un nuevo nodo. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 [ @subscriptionstreams=] *subscriptionstreams*  
 Es el número de conexiones permitidas por el agente de distribución para aplicar lotes de cambios en paralelo a un suscriptor, aunque manteniendo muchas de las características transaccionales presentes al utilizar un único subproceso. *subscriptionstreams* es **tinyint**, su valor predeterminado es null. Se admite un intervalo de valores de 1 a 64. Este parámetro no se admite para los suscriptores que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los publicadores de Oracle ni las suscripciones punto a punto. Cada vez que se usan flujos de suscripción, se agregan filas adicionales en la tabla msreplication_subscriptions (una por cada flujo) con un agent_id establecido en NULL.  
  
> [!NOTE]  
>  Los flujos de suscripción no funcionan en los artículos configurados para entregar [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para usar flujos de suscripción, configure en su lugar los artículos para que entreguen llamadas de procedimiento almacenado.  
  
 [ @subscriber_type=] *subscriber_type*  
 Es el tipo de suscriptor. *propiedad subscriber_type* es **tinyint**, y puede tener uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|0 (predeterminado)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Suscriptor|  
|1|Servidor del origen de datos ODBC|  
|2|Base de datos [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet|  
|3|Proveedor OLE DB|  
  
 [ @memory_optimized=] *memory_optimized*  
 Indica que la suscripción admite tablas optimizadas en memoria. *memory_optimized* es **bits**, donde 1 es igual a true (la suscripción es compatible con tablas optimizadas en memoria).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_addsubscription se utiliza en la replicación de instantáneas y transaccional.  
  
 Cuando un miembro del rol fijo de servidor sysadmin ejecuta sp_addsubscription para crear una suscripción de inserción, se crea implícitamente el trabajo del Agente de distribución y se ejecuta en la cuenta de servicio del Agente SQL Server. Se recomienda ejecutar [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) y especifique las credenciales de una cuenta de Windows diferente, específica del agente para @job_login y @job_password. Para más información, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 sp_addsubscription impide que los suscriptores ODBC y OLE DB tengan acceso a publicaciones que:  
  
-   Se crearon con nativo *sync_method* en la llamada a [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
-   Contengan artículos que se han agregado a la publicación mediante el [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) procedimiento almacenado que tenía un *pre_creation_cmd* valor del parámetro de 3 (truncar).  
  
-   Se intentó establecer *update_mode* para sincronizar tran.  
  
-   Tengan un artículo configurado para utilizar instrucciones con parámetros.  
  
 Además, si una publicación tiene la *allow_queued_tran* opción establecida en true (que permite poner en cola cambios en el suscriptor hasta que se pueden aplicar en el publicador), la columna de marca de tiempo en un artículo se automatizará como **marca de tiempo**, y los cambios de esa columna se envían al suscriptor. El suscriptor genera y actualiza el valor de la columna timestamp. Para un suscriptor ODBC u OLE DB, sp_addsubscription dará error si se realiza un intento para suscribirse a una publicación que tiene *allow_queued_tran* establecida en true y artículos con columnas timestamp.  
  
 Si una suscripción no utiliza un paquete DTS, no es posible suscribirse a una publicación que se establece en *allow_transformable_subscriptions*. Si la tabla de la publicación debe replicarse en una suscripción DTS y una suscripción no DTS, deben crearse dos publicaciones independientes: una para cada tipo de suscripción.  
  
 Al seleccionar las opciones **replication support only** , *initialize with backup*o *initialize from lsn*de *sync_type*, el agente de registro del LOG se debe ejecutar después de ejecutar **sp_addsubscription**, de modo que los scripts de instalación se escriban en la base de datos de distribución. El agente de registro del LOG se debe ejecutar con una cuenta que sea miembro del rol fijo de servidor **sysadmin** . Cuando la opción **sync_type** se establece en *Automatic*, no se requiere ninguna acción especial del agente de registro del LOG.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros del rol fijo de servidor sysadmin o del rol fijo de base de datos db_owner pueden ejecutar sp_addsubscription. En las suscripciones de extracción, los usuarios que tengan inicios de sesión en la lista de acceso de la publicación pueden ejecutar  sp_addsubscription.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addsubscription-trans_1.sql)]  
  
## <a name="see-also"></a>Vea también  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Crear una suscripción para un suscriptor que no sea de SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpushsubscription_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_changesubstatus &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
