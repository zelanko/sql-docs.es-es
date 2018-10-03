---
title: sp_helppublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c1293084c422c73bba83ee66e2242b9416368db6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624223"
---
# <a name="sphelppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de una publicación. Para un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicación, este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. En el caso de una publicación Oracle, se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación que se va a consultar. *publicación* es de tipo sysname y su valor predeterminado es **%**, que devuelve información sobre todas las publicaciones.  
  
 [  **@found =** ] **'***encuentra***'** salida  
 Es una marca para indicar que se devuelven filas. *se encontró*es **int** y un parámetro OUTPUT y su valor predeterminado es **23456**. **1** indica que se encuentra la publicación. **0** indica que no se encuentra la publicación.  
  
 [ **@publisher** =] **'***publisher***'**  
 Especifica que no es[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *publicador* es de tipo sysname y su valor predeterminado es NULL.  
  
> [!NOTE]  
>  *publicador* no se debe especificar al solicitar información de publicación de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|pubid|**int**|Id. de la publicación.|  
|NAME|**sysname**|Nombre de la publicación.|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**tinyint**|Estado actual de la publicación.<br /><br /> **0** = inactivo.<br /><br /> **1** = activo.|  
|tarea||Se utiliza para mantener la compatibilidad con versiones anteriores.|  
|replication frequency|**tinyint**|Tipo de frecuencia de replicación:<br /><br /> **0** = transaccional<br /><br /> **1** = instantánea|  
|synchronization method|**tinyint**|Modo de sincronización:<br /><br /> **0** = programa de copia masiva en modo nativo (**bcp** utilidad)<br /><br /> **1** = copia masiva de caracteres<br /><br /> **3** = concurrent, que significa que dicha copia masiva en modo nativo (**bcp**utilidad) se usa, pero no se bloquean las tablas durante la instantánea<br /><br /> **4** = Concurrent_c, que significa que se utiliza la copia masiva de caracteres pero no se bloquean las tablas durante la instantánea|  
|description|**nvarchar(255)**|Descripción opcional de la publicación.|  
|immediate_sync|**bit**|Indica si los archivos de sincronización se crean, o se vuelven a crear, cada vez que se ejecuta el Agente de instantáneas.|  
|enabled_for_internet|**bit**|Indica si los archivos de sincronización de la publicación se exponen en Internet a través del protocolo de transferencias de archivos (FTP) u otros servicios.|  
|allow_push|**bit**|Indica si se admiten suscripciones de inserción a la publicación.|  
|allow_pull|**bit**|Indica si se admiten suscripciones de extracción a la publicación.|  
|allow_anonymous|**bit**|Indica si se admiten suscripciones anónimas a la publicación.|  
|independent_agent|**bit**|Indica si hay un Agente de distribución independiente para esta publicación.|  
|immediate_sync_ready|**bit**|Indica si el Agente de instantáneas generó o no una instantánea que está lista para que la utilicen las nuevas suscripciones. Este parámetro se define únicamente si la publicación se define para tener siempre una instantánea disponible para las suscripciones nuevas o reinicializadas.|  
|allow_sync_tran|**bit**|Indica si se permiten suscripciones de actualización inmediata a la publicación.|  
|autogen_sync_procs|**bit**|Indica si se generan automáticamente procedimientos almacenados para admitir las suscripciones de actualización inmediata.|  
|snapshot_jobid|**binary (16)**|Id. de tarea programada.|  
|retention|**int**|Volumen de cambio, en horas, que se debe guardar para la publicación indicada.|  
|has subscription|**bit**|Indica si la publicación tiene suscripciones activas. **1** significa que la publicación tiene suscripciones activas, y **0** significa que la publicación no tiene ninguna suscripción.|  
|allow_queued_tran|**bit**|Especifica si se han habilitado las deshabilitaciones de colocación en cola de los cambios del suscriptor hasta que se puedan aplicar en el publicador. Si **0**, los cambios del suscriptor no se ponen en cola.|  
|snapshot_in_defaultfolder|**bit**|Especifica si los archivos de instantánea se almacenan en la carpeta predeterminada. Si **0**, los archivos de instantáneas se han almacenado en la ubicación alternativa especificada por *alternate_snapshot_folder*. Si **1**, los archivos de instantáneas pueden encontrarse en la carpeta predeterminada.|  
|alt_snapshot_folder|**nvarchar(255)**|Especifica la ubicación de la carpeta alternativa de la instantánea.|  
|pre_snapshot_script|**nvarchar(255)**|Especifica un puntero a un **.sql** ubicación del archivo. El Agente de distribución ejecutará el script previo a la instantánea antes de la ejecución de cualquiera de los scripts de objetos replicados al aplicar la instantánea en un suscriptor.|  
|post_snapshot_script|**nvarchar(255)**|Especifica un puntero a un **.sql** ubicación del archivo. El Agente de distribución ejecutará el script posterior a la instantánea después de que se apliquen el resto de scripts de objetos replicados y datos durante la sincronización inicial.|  
|compress_snapshot|**bit**|Especifica que la instantánea que se escribe en el *alt_snapshot_folder* ubicación está comprimida en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** especifica que no se comprimirá la instantánea.|  
|ftp_address|**sysname**|Dirección de red del servicio FTP para el distribuidor. Especifica dónde se encuentran los archivos de instantánea de una publicación para que los recoja el Agente de distribución o el Agente de mezcla de un suscriptor.|  
|ftp_port|**int**|El número de puerto del servicio FTP para el distribuidor.|  
|ftp_subdirectory|**nvarchar(255)**|Especifica dónde estarán disponibles los archivos de instantánea para que los recoja el Agente de distribución o el Agente de mezcla del suscriptor si la publicación admite la propagación de instantáneas mediante FTP.|  
|ftp_login|**sysname**|El nombre de usuario usada para conectarse al servicio FTP.|  
|allow_dts|**bit**|Especifica que la publicación permite transformaciones de datos. **0** especifica que no se permiten transformaciones DTS.|  
|allow_subscription_copy|**bit**|Especifica si se ha habilitado la capacidad de copiar las bases de datos de suscripciones que se suscriben a esta publicación. **0** significa que no se permite la copia.|  
|centralized_conflicts|**bit**|Especifica si los registros de conflicto se almacenan en el publicador.<br /><br /> **0** = conflicto entre los registros se almacenan tanto en el publicador y en el suscriptor que provocó el conflicto.<br /><br /> **1** = conflicto entre los registros se almacenan en el publicador.|  
|conflict_retention|**int**|Especifica el período de retención de conflictos, en días.|  
|conflict_policy|**int**|Especifica la directiva de resolución de conflictos seguida cuando se utiliza la opción de suscriptor de actualización en cola. Puede ser uno de estos valores:<br /><br /> **1** = el publicador gana el conflicto.<br /><br /> **2** = el suscriptor gana el conflicto.<br /><br /> **3** = se reinicializa la suscripción.|  
|queue_type||Especifica el tipo de cola utilizado. Puede ser uno de estos valores:<br /><br /> **MSMQ** = Use [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server para almacenar las transacciones.<br /><br /> **SQL** = Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar las transacciones.<br /><br /> Nota: Se ha interrumpido la compatibilidad con Message Queue Server.|  
|backward_comp_level||Nivel de compatibilidad de la base de datos, que puede ser uno de los que se especifican a continuación:<br /><br /> **90** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|Especifica si la información de publicación se publica en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory™. Un valor de **1** indica que se publica y un valor de **0** indica que no se publica.|  
|allow_initialize_from_backup|**bit**|Indica si los suscriptores pueden inicializar una suscripción a esta publicación a partir de una copia de seguridad en lugar de una instantánea inicial. **1** significa que se pueden inicializar suscripciones desde una copia de seguridad y **0** significa que no. Para obtener más información, consulte [inicializar una suscripción transaccional sin una instantánea](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) una suscripción transaccional sin una instantánea.|  
|replicate_ddl|**int**|Indica si la publicación admite replicación de esquema. **1** indica que se replican instrucciones de DDL (lenguaje) de definición de datos ejecutadas en el publicador, y **0** indica que no se replican las instrucciones de DDL. Para más información, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|enabled_for_p2p|**int**|Indica si la publicación se puede utilizar en una topología de replicación punto a punto. **1** indica que la publicación admite la replicación punto a punto. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|Especifica si la publicación admite suscriptores que no son [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un valor de **1** significa es que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admiten los suscriptores. Un valor de **0** significa que solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admiten los suscriptores. Para más información, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).|  
|enabled_for_p2p_conflictdetection|**int**|Especifica si el Agente de distribución detecta los conflictos para una publicación que está habilitada para la replicación punto a punto. Un valor de **1** significa que los conflictos se detectan. Para obtener más información, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|originator_id|**int**|Especifica un Id. para un nodo en una topología punto a punto. Este identificador se utiliza para la detección de conflictos si **enabled_for_p2p_conflictdetection** está establecido en **1**. Para obtener una lista de identificadores que ya se hayan utilizado, consulte la tabla del sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .|  
|p2p_continue_onconflict|**int**|Especifica si el Agente de distribución continúa procesando los cambios cuando se detecta un conflicto. Un valor de **1** significa que el agente continúa procesando los cambios.<br /><br /> **\*\* Precaución \* \***  se recomienda que use el valor predeterminado de **0**. Cuando esta opción se establece en **1**, el agente de distribución intenta converger los datos en la topología aplicando la fila en conflicto del nodo que tiene el identificador de originador más alto. Este método no garantiza la convergencia. Debe asegurarse de que la topología sea coherente una vez detectado un conflicto. Para obtener más información, vea "Controlar los conflictos" en [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|allow_partition_switch|**int**|Especifica si las instrucciones ALTER TABLE...SWITCH se pueden ejecutar con la base de datos publicada. Para obtener más información, vea [Replicar tablas e índices con particiones](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
|replicate_partition_switch|**int**|Especifica si las instrucciones ALTER TABLE...SWITCH que se ejecutan con la base de datos publicada se deben replicar en los suscriptores. Esta opción es válida solo si *allow_partition_switch* está establecido en **1**.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 El procedimiento sp_helppublication se utiliza en la replicación de instantáneas y transaccional.  
  
 sp_helppublication devolverá información sobre todas las publicaciones que son propiedad del usuario que ejecuta este procedimiento.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor sysadmin en el publicador o los miembros del rol fijo de base de datos db_owner en la base de datos de publicación o los usuarios de la lista de acceso a la publicación (PAL) pueden ejecutar sp_helppublication.  
  
 En el caso de un publicador que no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], únicamente los miembros del rol fijo de servidor sysadmin en el distribuidor, los miembros del rol fijo de base de datos db_owner en la base de datos de distribución o los usuarios de PAL pueden ejecutar sp_helppublication.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
