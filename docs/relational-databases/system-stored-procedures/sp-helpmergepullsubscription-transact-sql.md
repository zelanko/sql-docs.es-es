---
title: sp_helpmergepullsubscription (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c2a84992bdc1cce94bdc997ce017825c0a2fb8e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de las suscripciones de extracción que existen en un suscriptor. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpmergepullsubscription [ [ @publication=] 'publication']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
```  
  
## <a name="argument"></a>Argumento  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%**. Si *publicación* es **%**, se devuelve información sobre todas las publicaciones de combinación y suscripciones en la base de datos actual.  
  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador. *Publisher*es **sysname**, su valor predeterminado es **%**.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Es el nombre de la base de datos del publicador. *publisher_db*es **sysname**, su valor predeterminado es **%**.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 Indica si se muestran las suscripciones de extracción. *subscription_type*es **nvarchar (10)**, su valor predeterminado es **'pull'**. Los valores válidos son **'push'**, **'pull'**, o **'both'**.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**nvarchar(1000)**|Nombre de la suscripción.|  
|**Publicación**|**sysname**|Nombre de la publicación.|  
|**publicador**|**sysname**|Nombre del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**suscriptor**|**sysname**|Nombre del suscriptor.|  
|**subscription_db**|**sysname**|Nombre de la base de datos de suscripciones.|  
|**status**|**int**|Estado de la suscripción:<br /><br /> **0** = suscripción inactiva<br /><br /> **1** = suscripción activa<br /><br /> **2** = suscripción eliminada<br /><br /> **3** = suscripción separada<br /><br /> **4** = suscripción adjunta<br /><br /> **5** = suscripción se ha marcado para reiniciarla con carga<br /><br /> **6** = la suscripción no se pudo asociar el depurador<br /><br /> **7** = suscripción se restauró desde la copia de seguridad|  
|**propiedad subscriber_type**|**int**|Tipo de suscriptor:<br /><br /> **1** = global<br /><br /> **2** = local<br /><br /> **3** = anónima|  
|**subscription_type**|**int**|Tipo de suscripción:<br /><br /> **0** = inserción<br /><br /> **1** = extracción<br /><br /> **2** = anónima|  
|**priority**|**float(8)**|Prioridad de la suscripción. El valor debe ser menor que **100,00**.|  
|**sync_type**|**tinyint**|Tipo de sincronización de suscripción:<br /><br /> **1** = automático<br /><br /> **2** = instantánea no se utiliza.|  
|**Descripción**|**nvarchar(255)**|Breve descripción de la suscripción de extracción.|  
|**merge_jobid**|**binary (16)**|Id. de trabajo del Agente de mezcla.|  
|**enabled_for_syncmgr**|**int**|Indica si la suscripción se puede sincronizar mediante el Administrador de sincronización de [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|**last_updated**|**nvarchar(26)**|Hora a la que el Agente de mezcla sincronizó correctamente la suscripción por última vez.|  
|**publisher_login**|**sysname**|Nombre de inicio de sesión del publicador.|  
|**publisher_password**|**sysname**|La contraseña del publicador.|  
|**publisher_security_mode**|**int**|Especifica el modo de seguridad del publicador:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows|  
|**Distribuidor**|**sysname**|Nombre del distribuidor.|  
|**distributor_login**|**sysname**|Nombre de inicio de sesión del distribuidor.|  
|**distributor_password**|**sysname**|Contraseña del distribuidor.|  
|**distributor_security_mode**|**int**|Especifica el modo de seguridad del distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows|  
|**ftp_address**|**sysname**|Disponible únicamente por compatibilidad con versiones anteriores. Es la dirección de red del servicio de protocolo (FTP) de transferencia de archivo para el distribuidor.|  
|**ftp_port**|**int**|Disponible únicamente por compatibilidad con versiones anteriores. Es el número de puerto del servicio FTP para el distribuidor.|  
|**ftp_login**|**sysname**|Disponible únicamente por compatibilidad con versiones anteriores. Es el nombre de usuario que se utiliza para conectar con el servicio FTP.|  
|**ftp_password**|**sysname**|Disponible únicamente por compatibilidad con versiones anteriores. Es la contraseña del usuario que se utiliza para conectarse al servicio FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Ubicación donde se almacena la carpeta de instantáneas si no es la ubicación predeterminada o es complementaria a ésta.|  
|**working_directory**|**nvarchar(255)**|Ruta de acceso completa al directorio donde se transfieren los archivos de instantáneas por medio de FTP, cuando se especifica esa opción.|  
|**use_ftp**|**bit**|Suscripción se está suscribiendo a la publicación a través de Internet, y se configuran propiedades de direccionamiento FTP. Si **0**, suscripción no utiliza FTP. Si **1**, suscripción utiliza FTP.|  
|**offload_agent**|**bit**|Especifica si el agente se puede activar y ejecutar de manera remota. Si **0**, el agente no puede activarse de forma remota.|  
|**offload_server**|**sysname**|Nombre del servidor utilizado para la activación remota.|  
|**use_interactive_resolver**|**int**|Devuelve si se utiliza o no el solucionador interactivo durante la reconciliación. Si **0**, no se utiliza el solucionador interactivo.|  
|**subid**|**uniqueidentifier**|Id. del suscriptor.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Ruta de acceso de la carpeta donde se guardan los archivos de instantáneas.|  
|**last_sync_status**|**int**|Estado de sincronización:<br /><br /> **1** = a partir de<br /><br /> **2** = se ha realizado correctamente<br /><br /> **3** = en curso<br /><br /> **4** = inactivo<br /><br /> **5** = reintentando después de un error anterior<br /><br /> **6** = error<br /><br /> **7** = error en la validación<br /><br /> **8** = validación superada<br /><br /> **9** = se solicitó un cierre|  
|**last_sync_summary**|**sysname**|Descripción de los resultados de la última sincronización.|  
|**use_web_sync**|**bit**|Especifica si la suscripción se puede sincronizar a través de HTTPS, donde un valor de **1** significa que esta característica está habilitada.|  
|**internet_url**|**nvarchar(260)**|URL que representa la ubicación de la escucha de replicación para la sincronización web.|  
|**internet_login**|**nvarchar(128)**|Inicio de sesión que utiliza el Agente de mezcla al conectarse al servidor web que hospeda la sincronización web utilizando autenticación básica.|  
|**internet_password**|**nvarchar (524)**|Contraseña para el Inicio de sesión que utiliza el Agente de mezcla al conectarse al servidor web que hospeda la sincronización web utilizando autenticación básica.|  
|**internet_security_mode**|**int**|Modo de autenticación utilizado al conectarse al servidor web que hospeda la sincronización web. Un valor de **1** significa autenticación de Windows y un valor de **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**internet_timeout**|**int**|Período de tiempo, en segundos, antes de que expire una solicitud de sincronización Web.|  
|**Nombre de host**|**nvarchar(128)**|Especifica un valor sobrecargado para [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) cuando esta función se utiliza en la cláusula WHERE de un filtro de fila con parámetros.|  
|**job_login**|**nvarchar(512)**|Es la cuenta de Windows bajo la que se ejecuta el agente de mezcla, que se devuelve en el formato *dominio*\\*nombre de usuario*.|  
|**job_password**|**sysname**|Por motivos de seguridad, un valor de "**\*\*\*\*\*\*\*\*\*\***" es siempre se devuelven.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpmergepullsubscription** se utiliza en la replicación de mezcla. En el conjunto de resultados, la fecha devuelta en **last_updated** tenga el mismo formato *DDMMAAAA ss. fff*.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor y el **db_owner** rol fijo de base de datos puede ejecutar **sp_helpmergepullsubscription**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
