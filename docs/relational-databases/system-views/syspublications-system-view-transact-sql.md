---
title: syspublications (vista del sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications view
ms.assetid: e5f57c32-efc0-4455-a74f-684dc2ae51f8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf2c03c08d6653756fa9a65cc0dbe5be8ec2e173
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780503"
---
# <a name="syspublications-system-view-transact-sql"></a>syspublications (Vista del sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **syspublications** vista expone información de publicación. Esta vista se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Descripción**|**nvarchar(255)**|La entrada descriptiva para la publicación.|  
|**Nombre**|**sysname**|Nombre único asociado a la publicación.|  
|**pubid**|**int**|Columna de identidad que proporciona un id. único para la publicación.|  
|**repl_freq**|**tinyint**|Frecuencia de replicación:<br /><br /> **0** = basada en transacciones (transaccional).<br /><br /> **1** = actualización programada de tabla (instantánea).|  
|**status**|**tinyint**|Estado de la publicación:<br /><br /> **0** = inactivo.<br /><br /> **1** = activo.|  
|**sync_method**|**tinyint**|Método de sincronización:<br /><br /> **0** = programa de copia masiva en modo nativo (bcp).<br /><br /> **1** = carácter BCP.<br /><br /> **3** = concurrent, que significa que se utiliza BCP nativo pero no se bloquean las tablas durante la instantánea.<br /><br /> **4** = Concurrent_c, que significa que se utiliza BCP de caracteres, pero las tablas no se bloquean durante la instantánea.|  
|**snapshot_jobid**|**binary (16)**|Identifica el trabajo del agente programado para generar la instantánea inicial.|  
|**independent_agent**|**bit**|Especifica si hay un Agente de distribución independiente para esta publicación.<br /><br /> **0** = la publicación utiliza un agente de distribución compartido, y cada par de base de datos de publicador y suscriptor de base de datos tiene un único agente compartido.<br /><br /> **1** = hay un agente de distribución independiente para esta publicación.|  
|**immediate_sync**|**bit**|Indica si los archivos de sincronización se crean o vuelven a crear cada vez que se ejecuta el agente de instantáneas, donde **1** significa que se crean cada vez que se ejecuta el agente.|  
|**enabled_for_internet**|**bit**|Indica si los archivos de sincronización para la publicación se exponen en Internet a través del protocolo de transferencia de archivos (FTP) y otros servicios, donde **1** significa que puede obtenerse desde Internet.|  
|**allow_push**|**bit**|Indica si se permiten suscripciones de inserción en la publicación, donde **1** significa que están permitidas.|  
|**allow_pull**|**bit**|Indica si se permiten suscripciones de extracción en la publicación, donde **1** significa que están permitidas.|  
|**allow_anonymous**|**bit**|Indica si se admiten suscripciones anónimas en la publicación, donde **1** significa que están permitidas.|  
|**immediate_sync_ready**|**bit**|Indica si el Agente de instantáneas ha generado la instantánea y está lista para que la utilicen las nuevas suscripciones. Es significativo únicamente para publicaciones de actualización inmediata. **1** indica que la instantánea está lista.|  
|**allow_sync_tran**|**bit**|Especifica si se permiten suscripciones de actualización inmediata en la publicación. **1** significa que se permiten suscripciones de actualización inmediata.|  
|**autogen_sync_procs**|**bit**|Especifica si se ha generado en el publicador un procedimiento almacenado de sincronización para suscripciones de actualización inmediata. **1** significa que se ha generado en el publicador.|  
|**retención**|**int**|Cantidad de tiempo, en horas, que los cambios hechos a la publicación se guardan en la base de datos de distribución.|  
|**allow_queued_tran**|**bit**|Especifica si se ha habilitado la colocación en cola de los cambios del suscriptor hasta que se puedan aplicar en el publicador. Si **1**, se ponen en cola los cambios del suscriptor.|  
|**snapshot_in_defaultfolder**|**bit**|Especifica si los archivos de instantánea se almacenan en la carpeta predeterminada. Si **0**, los archivos de instantáneas se han almacenado en la ubicación alternativa especificada por *alternate_snapshot_folder*. Si es 1, los archivos de instantáneas se encuentran en la carpeta predeterminada.|  
|**alt_snapshot_folder**|**nvarchar(510)**|Especifica la ubicación de la carpeta alternativa de la instantánea.|  
|**pre_snapshot_script**|**nvarchar(510)**|Especifica un puntero a un **.sql** ubicación del archivo. El Agente de distribución ejecuta el script previo a la instantánea antes de la ejecución de cualquiera de los scripts de los objetos replicados al aplicar la instantánea en un suscriptor.|  
|**post_snapshot_script**|**nvarchar(510)**|Especifica un puntero a un **.sql** ubicación del archivo. El Agente de distribución ejecuta el script posterior a la instantánea después de que se aplique el resto de scripts de objetos replicados y datos durante la sincronización inicial.|  
|**compress_snapshot**|**bit**|Especifica que la instantánea que se escribe en el *alt_snapshot_folder* ubicación está comprimida en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **1** significa que se comprimirá la instantánea.|  
|**ftp_address**|**sysname**|Dirección de red del servicio FTP para el distribuidor. Especifica dónde se encuentran los archivos de instantánea de la publicación para que los recoja el Agente de distribución.|  
|**ftp_port**|**int**|El número de puerto del servicio FTP para el distribuidor. Especifica dónde se encuentra el agente de distribución recoger los archivos de instantáneas de publicación.|  
|**ftp_subdirectory**|**nvarchar(510)**|Especifica dónde están disponibles los archivos de instantánea para que los recoja el Agente de distribución si la publicación admite la propagación de instantáneas mediante FTP.|  
|**ftp_login**|**nvarchar(256)**|El nombre de usuario usada para conectarse al servicio FTP.|  
|**ftp_password**|**nvarchar(1048)**|La contraseña de usuario usada para conectarse al servicio FTP.|  
|**allow_dts**|**bit**|Especifica si la publicación permite transformaciones de los Servicios de transformación de datos (DTS) de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. **1** especifica que se permiten transformaciones DTS.|  
|**allow_subscription_copy**|**bit**|Especifica si se ha habilitado la capacidad de copiar las bases de datos de suscripciones que se suscriben a esta publicación. **1** significa que se permite la copia.|  
|**centralized_conflicts**|**bit**|Especifica si los registros de conflicto se almacenan en el publicador.<br /><br /> **0** = conflicto entre los registros se almacenan tanto en el publicador y en el suscriptor que provocó el conflicto.<br /><br /> **1** = conflicto entre los registros se almacenan en el publicador.|  
|**conflict_retention**|**int**|Especifica el período de retención de registros de conflictos, en días.|  
|**conflict_policy**|**int**|Especifica la directiva de resolución de conflictos seguida cuando se utiliza la opción de suscriptor de actualización en cola. Puede ser uno de estos valores:<br /><br /> **1** = el publicador gana el conflicto.<br /><br /> **2** = el suscriptor gana el conflicto.<br /><br /> **3** = se reinicializa la suscripción.|  
|**queue_type**|**int**|Especifica el tipo de cola utilizado. Puede ser uno de estos valores:<br /><br /> **1** = .msmq, que utiliza [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server para almacenar las transacciones.<br /><br /> **2** =. SQL, que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar las transacciones.<br /><br /> Nota: El uso de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server ha quedado desusado y ya no se admite.|  
|**ad_guidname**|**sysname**|Especifica si la información de publicación se publica en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Un identificador exclusivo global (GUID) especifica que la publicación se ha publicado en Active Directory, y el GUID es el objectGUID del objeto de publicación de Active Directory correspondiente. Si es NULL, la publicación no se publica en Active Directory.<br /><br /> Nota: Ya no se admite la publicación en Active Directory.|  
|**backward_comp_level**|**int**|Nivel de compatibilidad de la base de datos, que puede ser uno de los valores siguientes:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**allow_initialize_from_backup**|**bit**|Indica si los suscriptores pueden inicializar una suscripción a esta publicación desde una copia de seguridad en lugar de una instantánea inicial. **1** significa que se pueden inicializar suscripciones desde una copia de seguridad y **0** significa que no. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).|  
|**min_autonosync_lsn**|**binary(1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|Indica si se admite la replicación de esquemas para la publicación.<br /><br /> **1** = DDL las instrucciones que se ejecuta en el publicador se replican.<br /><br /> **0** = indica que no se replican las instrucciones de DDL. Para más información, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|**options**|**int**|Mapa de bits que especifica opciones de publicación adicionales. Los valores de opciones binarias son los siguientes:<br /><br /> **0 x 1** : habilitado para replicación punto a punto.<br /><br /> **0 x 2** -publicar solo cambios locales para la replicación punto a punto.<br /><br /> **0 x 4** : habilitado para que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.<br /><br /> **0 x 8** : habilitado para la detección de conflictos punto a punto.|  
|**originator_id**|**smallint**|Identifica cada nodo en una topología de replicación punto a punto para detectar conflictos. Para obtener más información, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
