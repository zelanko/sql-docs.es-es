---
title: sp_helppullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppullsubscription_TSQL
- sp_helppullsubscription
helpviewer_keywords:
- sp_helppullsubscription
ms.assetid: a0d9c3f1-1fe9-497c-8e2f-5b74f47a7346
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b094d8bb3f9bd2cebfd9184976aeb57de77886e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52801807"
---
# <a name="sphelppullsubscription-transact-sql"></a>sp_helppullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca de una o más suscripciones del suscriptor. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helppullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @show_push = ] 'show_push' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del servidor remoto. *publicador* es **sysname**, su valor predeterminado es **%**, que devuelve información de todos los publicadores.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es **%**, que devuelve todas las bases de datos del publicador.  
  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%**, que devuelve todas las publicaciones. Si este parámetro es igual a todas las suscripciones de extracción solo independent_agent = **0** se devuelven.  
  
 [  **@show_push=**] **'***el argumento show_push***'**  
 Indica si se devuelven todas las suscripciones de inserción. *el argumento show_push*es **nvarchar (5)**, su valor predeterminado es False, que no devuelve las suscripciones de inserción.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|Nombre del publicador.|  
|**base de datos del publicador**|**sysname**|Nombre de la base de datos del publicador.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**independent_agent**|**bit**|Indica si hay un agente de distribución independiente para esta publicación.|  
|**tipo de suscripción**|**int**|Tipo de suscripción a la publicación.|  
|**agente de distribución**|**Nvarchar (100)**|Agente de distribución que controla la suscripción.|  
|**Descripción de la publicación**|**nvarchar(255)**|Descripción de la publicación.|  
|**última hora de actualización**|**date**|Hora en que se actualizó la información de suscripción. Es una cadena UNICODE de fecha ISO (114) + hora ODBC (121). El formato es aaaammdd hh:mi:sss.mmm, donde 'aaaa' es el año, 'mm' el mes, 'dd' el día, 'hh' la hora, 'mi' los minutos, 'sss' los segundos y 'mmm' los milisegundos.|  
|**nombre de la suscripción**|**varchar(386)**|Nombre de la suscripción.|  
|**última marca de tiempo de transacción**|**varbinary (16)**|Marca de tiempo de la última transacción replicada.|  
|**modo de actualización**|**tinyint**|Tipo de actualizaciones permitidas.|  
|**job_id de agente de distribución**|**int**|Id. de trabajo del agente de distribución.|  
|**enabled_for_synmgr**|**int**|Indica si la suscripción se puede sincronizar mediante el Administrador de sincronización de [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|**guid de la suscripción**|**binary (16)**|Identificador global para la versión de la suscripción en la publicación.|  
|**subid**|**binary (16)**|Identificador global de una suscripción anónima.|  
|**immediate_sync**|**bit**|Indica si los archivos de sincronización se crean, o se vuelven a crear, cada vez que se ejecuta el Agente de instantáneas.|  
|**inicio de sesión del publicador**|**sysname**|Id. de inicio de sesión utilizado en el publicador para la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**contraseña del publicador**|**nvarchar (524)**|Contraseña (cifrada) utilizada en el publicador para la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**security_mode de publicador**|**int**|Modo de seguridad aplicado en el publicador:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows<br /><br /> **2** = los desencadenadores de sincronización utilizan una estática **sysservers** entrada para realizar la llamada a procedimiento remoto (RPC), y *publisher* debe definirse en el **sysservers**tabla como un servidor remoto o vinculado.|  
|**distribuidor**|**sysname**|Nombre del distribuidor.|  
|**distributor_login**|**sysname**|Id. de inicio de sesión utilizado en el distribuidor para la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**distributor_password**|**nvarchar (524)**|Contraseña (cifrada) utilizada en el distribuidor para la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**distributor_security_mode**|**int**|Modo de seguridad aplicado en el distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows|  
|**ftp_address**|**sysname**|Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_port**|**int**|Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_login**|**sysname**|Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_password**|**nvarchar (524)**|Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Ubicación donde se almacena la carpeta de instantáneas si no es la ubicación predeterminada o es complementaria a ésta.|  
|**working_directory**|**nvarchar(255)**|Ruta de acceso completa al directorio adonde se transfieren los archivos de instantáneas mediante FTP cuando se especifica esa opción.|  
|**use_ftp**|**bit**|La suscripción se está suscribiendo a la publicación a través de Internet y se han configurado propiedades de direccionamiento FTP. Si **0**, suscripción no utiliza FTP. Si **1**, suscripción utiliza FTP.|  
|**publication_type**|**int**|Especifica el tipo de replicación de la publicación:<br /><br /> **0** = replicación transaccional<br /><br /> **1** = replicación de instantáneas<br /><br /> **2** = replicación de mezcla|  
|**dts_package_name**|**sysname**|Especifica el nombre del paquete de Servicios de transformación de datos (DTS).|  
|**dts_package_location**|**int**|Ubicación donde se almacena el paquete DTS:<br /><br /> **0** = distribuidor<br /><br /> **1** = suscriptor|  
|**offload_agent**|**bit**|Especifica si el agente puede activarse de forma remota. Si **0**, el agente no puede activarse de forma remota.|  
|**offload_server**|**sysname**|Especifica el nombre de red del servidor utilizado para la activación remota.|  
|**last_sync_status**|**int**|Estado de la suscripción:<br /><br /> **0** todos los = trabajos están esperando para iniciar<br /><br /> **1** = uno o más trabajos se están iniciando<br /><br /> **2** = todos los trabajos se han ejecutado correctamente<br /><br /> **3** = al menos un trabajo se está ejecutando<br /><br /> **4** = todos los trabajos están programados y se encuentran inactivos<br /><br /> **5** = al menos un trabajo intenta ejecutarse después de un error anterior<br /><br /> **6** = al menos un trabajo no ha podido ejecutar correctamente|  
|**last_sync_summary**|**sysname**|Descripción de los resultados de la última sincronización.|  
|**last_sync_time**|**datetime**|Hora en que se actualizó la información de suscripción. Es una cadena UNICODE de fecha ISO (114) + hora ODBC (121). El formato es aaaammdd hh:mi:sss.mmm, donde 'aaaa' es el año, 'mm' el mes, 'dd' el día, 'hh' la hora, 'mi' los minutos, 'sss' los segundos y 'mmm' los milisegundos.|  
|**job_login**|**nvarchar(512)**|Es la cuenta de Windows bajo la que se ejecuta el agente de distribución, que se devuelve en el formato *dominio*\\*username*.|  
|**job_password**|**sysname**|Por motivos de seguridad, un valor de "**\*\*\*\*\*\*\*\*\*\***" es siempre se devuelven.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helppullsubscription** se utiliza en la replicación de instantáneas y transaccional.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_helppullsubscription** .  
  
## <a name="see-also"></a>Vea también  
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
