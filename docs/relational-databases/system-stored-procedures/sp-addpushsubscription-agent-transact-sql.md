---
title: sp_addpushsubscription_agent (Transact-SQL) | Documentos de Microsoft
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
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d111bef33c73d2417ddccf88c5bb083be6c2a35f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spaddpushsubscriptionagent-transact-sql"></a>sp_addpushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un nuevo trabajo del agente programado que se utiliza para sincronizar una suscripción de inserción con una publicación transaccional. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addpushsubscription_agent [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
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
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @distribution_job_name = ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @subscriber_provider = ] 'subscriber_provider' ]   
    [ , [ @subscriber_datasrc = ] 'subscriber_datasrc' ]   
    [ , [ @subscriber_location = ] 'subscriber_location' ]  
    [ , [ @subscriber_provider_string = ] 'subscriber_provider_string' ]   
    [ , [ @subscriber_catalog = ] 'subscriber_catalog' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@subscriber =**] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_db =**] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db* es **sysname**, su valor predeterminado es null. Para un suscriptor no SQL Server, especifique un valor de **(destino predeterminado)** para *subscriber_db*.  
  
 [  **@subscriber_security_mode =**] *subscriber_security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con un suscriptor durante la sincronización. *subscriber_security_mode* es **int**, su valor predeterminado es 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. **1** especifica autenticación de Windows.  
  
> [!IMPORTANT]  
>  En el caso de las suscripciones de actualización en cola, utilice la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las conexiones a los suscriptores y especifique otra cuenta para la conexión a cada suscriptor. Para el resto de las suscripciones, utilice la autenticación de Windows.  
  
 [  **@subscriber_login =**] **'***subscriber_login***'**  
 Es el inicio de sesión del suscriptor que se debe utilizar al conectarse con un suscriptor durante la sincronización. *subscriber_login* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_password =**] **'***subscriber_password***'**  
 Es la contraseña del suscriptor. *subscriber_password* es necesaria si *subscriber_security_mode* está establecido en **0**. *subscriber_password* es **sysname**, su valor predeterminado es null. Si se utiliza una contraseña de suscriptor, se cifra automáticamente.  
  
> [!IMPORTANT]  
>  No utilice una contraseña en blanco. Utilice una contraseña segura. Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@job_login =** ] **'***job_login***'**  
 Es el inicio de sesión de la cuenta de Windows en la que se ejecuta el agente. *job_login* es **nvarchar (257)**, su valor predeterminado es null. Esta cuenta de Windows se utiliza siempre para las conexiones del agente con el distribuidor y para las conexiones con el suscriptor al utilizar la Autenticación de Windows integrada.  
  
 [  **@job_password =** ] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows en la que se ejecuta el agente. *job_password* es **sysname**, no tiene ningún valor predeterminado.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@job_name =** ] **'***job_name***'**  
 Es el nombre de un trabajo del agente existente. *job_name* es **sysname**, su valor predeterminado es null. Este parámetro solamente se especifica cuando la suscripción se va a sincronizar mediante un trabajo existente en lugar de uno recién creado (el valor predeterminado). Si no es un miembro de la **sysadmin** rol fijo de servidor, debe especificar *job_login* y *job_password* cuando se especifica *job_name*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 Es la frecuencia con que se programa el agente de distribución. *frequency_type* es **int**, y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64** (valor predeterminado)|Iniciar automáticamente|  
|**128**|Periódica|  
  
> [!NOTE]  
>  Especifica el valor de **64** hace que el agente de distribución para que se ejecute en modo continuo. Esto equivale a configurar la **-continua** parámetro para el agente. Para más información, consulte [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 Es el valor que se aplican a la frecuencia establecida por *frequency_type*. *frequency_interval* es **int**, su valor predeterminado es 1.  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 Es la fecha del Agente de distribución. Este parámetro se utiliza cuando *frequency_type* está establecido en **32** (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**1** (predeterminado)|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, con un valor predeterminado es 0.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 Es la frecuencia de repetición de la programación durante el periodo definido. *frequency_subday* es **int**, y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4** (valor predeterminado)|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es 5.  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 Es la hora del día en que el agente de distribución se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, con un valor predeterminado es 0.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 Es la hora del día en que el agente de distribución deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es 235959.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Es la fecha en que el agente de distribución se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, con un valor predeterminado es 0.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Es la fecha en la que el agente de distribución deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, con un valor predeterminado es 99991231.  
  
 [  **@dts_package_name =** ] **'***dts_package_name***'**  
 Especifica el nombre del paquete de Servicios de transformación de datos (DTS). *dts_package_name* es un **sysname** con un valor predeterminado es NULL. Por ejemplo, para especificar el nombre de paquete `DTSPub_Package`, el parámetro sería `@dts_package_name = N'DTSPub_Package'`.  
  
 [  **@dts_package_password =** ] **'***dts_package_password***'**  
 Especifica la contraseña necesaria para ejecutar el paquete. *dts_package_password* es **sysname** con un valor predeterminado es NULL.  
  
> [!NOTE]  
>  Debe especificar una contraseña si *dts_package_name* se especifica.  
  
 [  **@dts_package_location =** ] **'***dts_package_location***'**  
 Especifica la ubicación del paquete. *dts_package_location* es un **tipo (12)**, su valor predeterminado del distribuidor. La ubicación del paquete puede ser **distribuidor** o **suscriptor**.  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 Indica si se puede sincronizar la suscripción a través de [!INCLUDE[msCoName](../../includes/msconame-md.md)] el Administrador de sincronización. *enabled_for_syncmgr* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **false**, la suscripción no está registrada con el Administrador de sincronización. Si **true**, la suscripción se registra con el Administrador de sincronización y se puede sincronizar sin iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@distribution_job_name =** ] **'***distribution_job_name***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@publisher =** ] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_provider=** ] **'***subscriber_provider***'**  
 Es el identificador de programación (PROGID) único mediante el cual se registra el proveedor OLE DB para los orígenes de datos que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *subscriber_provider* es **sysname**, su valor predeterminado es NULL. *subscriber_provider* debe ser único para el proveedor OLE DB instalado en el distribuidor. *subscriber_provider* solo se admite para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
 [  **@subscriber_datasrc=** ] **'***subscriber_datasrc***'**  
 Es el nombre del origen de datos tal y como lo entiende el proveedor OLE DB. *subscriber_datasrc* es **nvarchar (4000)**, su valor predeterminado es null. *subscriber_datasrc* se pasa como la propiedad DBPROP_INIT_DATASOURCE para inicializar el proveedor OLE DB. *subscriber_datasrc* solo se admite para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
 [  **@subscriber_location=** ] **'***subscriber_location***'**  
 Es la ubicación de la base de datos tal y como la entiende el proveedor OLE DB. *subscriber_location* es **nvarchar (4000)**, su valor predeterminado es null. *subscriber_location* se pasa como la propiedad DBPROP_INIT_LOCATION para inicializar el proveedor OLE DB. *subscriber_location* solo se admite para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
 [  **@subscriber_provider_string=** ] **'***subscriber_provider_string***'**  
 Es la cadena de conexión específica del proveedor OLE DB que identifica el origen de datos. *subscriber_provider_string* es **nvarchar (4000)**, su valor predeterminado es null. *subscriber_provider_string* se pasó a IDataInitialize o se establece como la propiedad DBPROP_INIT_PROVIDERSTRING para inicializar el proveedor OLE DB. *subscriber_provider_string* solo se admite para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
 [  **@subscriber_catalog=** ] **'***subscriber_catalog***'**  
 Es el catálogo que debe utilizarse al establecer una conexión con el proveedor OLE DB. *subscriber_catalog* es **sysname**, su valor predeterminado es NULL. *subscriber_catalog* se pasa como la propiedad DBPROP_INIT_CATALOG para inicializar el proveedor OLE DB. *subscriber_catalog* solo se admite para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addpushsubscription_agent** se utiliza en la replicación de instantáneas y transaccional.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addpushsubscription_agent**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Crear una suscripción para un suscriptor que no sea de SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
