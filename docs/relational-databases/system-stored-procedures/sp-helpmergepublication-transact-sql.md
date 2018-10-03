---
title: sp_helpmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepublication
- sp_helpmergepublication_TSQL
helpviewer_keywords:
- sp_helpmergepublication
ms.assetid: dfe1e1e1-9a65-406a-aced-6385a078e135
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26c19d33b9834d2a8cdf1ee0b05530138c3fa006
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717933"
---
# <a name="sphelpmergepublication-transact-sql"></a>sp_helpmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre una publicación de combinación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpmergepublication [ [ @publication = ] 'publication' ]  
    [ , [ @found = ] 'found' OUTPUT ]  
    [ , [ @publication_id = ] 'publication_id' OUTPUT ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication **=** ] **'***publicación***'**  
 Nombre de la publicación. *publicación*es **sysname**, su valor predeterminado es **%**, que devuelve información sobre todas las publicaciones de mezcla en la base de datos actual.  
  
 [ @found **=** ] **'***encuentra***'** salida  
 Marca que indica las filas devueltas. *se encontró*es **int** y un parámetro OUTPUT y su valor predeterminado es null. **1** indica que se encuentra la publicación. **0** indica que no se encuentra la publicación.  
  
 [ @publication_id **=**] **'***publication_id***'** salida  
 El número de identificación de la publicación. *publication_id* es **uniqueidentifier** y un parámetro OUTPUT y su valor predeterminado es null.  
  
 [ @reserved **=**] **'***reservada***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *reservado* es **nvarchar (20)**, su valor predeterminado es null.  
  
 [ @publisher **=** ] **'***publisher***'**  
 El nombre del publicador. *publicador* es **sysname**, su valor predeterminado es null.  
  
 [@publisher_db **=** ] **'***publisher_db***'**  
 El nombre de la base de datos de publicación. *publisher_db* es **sysname**, su valor predeterminado es null.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**int**|Orden secuencial de la publicación en la lista del conjunto de resultados.|  
|NAME|**sysname**|Nombre de la publicación.|  
|description|**nvarchar(255)**|Descripción de la publicación.|  
|status|**tinyint**|Indica cuándo están disponibles los datos de la publicación.|  
|retention|**int**|Tiempo durante el que guardar los metadatos sobre los cambios de los artículos de la publicación. Las unidades de este período pueden ser días, semanas, meses o años. Para obtener información sobre las unidades, vea la columna retention_period_unit.|  
|sync_mode|**tinyint**|Modo de sincronización de esta publicación:<br /><br /> **0** = programa de copia masiva en modo nativo (**bcp** utilidad)<br /><br /> **1** = copia masiva de caracteres|  
|allow_push|**int**|Determina si es posible crear suscripciones de inserción para la publicación indicada. **0** significa que no se permite una suscripción de inserción.|  
|allow_pull|**int**|Determina si es posible crear suscripciones de extracción para la publicación indicada. **0** significa que no se permite una suscripción de extracción.|  
|allow_anonymous|**int**|Determina si es posible crear suscripciones anónimas para la publicación indicada. **0** significa que no se permite una suscripción anónima.|  
|centralized_conflicts|**int**|Determina si los registros de los conflictos se almacenan en el publicador dado:<br /><br /> **0** = conflicto entre los registros se almacenan tanto en el publicador y en el suscriptor que provocó el conflicto.<br /><br /> **1** = conflicto entre todos los registros se almacenan en el publicador.|  
|priority|**float(8)**|Prioridad de la suscripción en bucle invertido.|  
|snapshot_ready|**tinyint**|Indica si la instantánea de esta publicación está lista:<br /><br /> **0** = instantánea está lista para su uso.<br /><br /> **1** = instantánea no está lista para su uso.|  
|publication_type|**int**|Tipo de publicación:<br /><br /> **0** = la instantánea.<br /><br /> **1** = transaccional.<br /><br /> **2** = la mezcla.|  
|pubid|**uniqueidentifier**|Identificador único de esta publicación.|  
|snapshot_jobid|**binary (16)**|Identificador de trabajo del Agente de instantáneas. Para obtener la entrada del trabajo de instantánea en la [sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md) tabla del sistema, debe convertir este valor hexadecimal a **uniqueidentifier**.|  
|enabled_for_internet|**int**|Determina si la publicación está habilitada para Internet. Si **1**, los archivos de sincronización para la publicación se colocan en el `C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\Ftp` directory. El usuario debe crear el directorio FTP (Protocolo de transferencia de archivos). Si **0**, la publicación no está habilitada para el acceso a Internet.|  
|dynamic_filter|**int**|Indica si se debe usar el filtro de filas con parámetros. **0** significa que no se utiliza un filtro de fila con parámetros.|  
|has_subscription|**bit**|Indica si la publicación tiene alguna suscripción. **0** significa que actualmente no hay ninguna suscripción a esta publicación.|  
|snapshot_in_default_folder|**bit**|Especifica si los archivos de instantáneas se almacenan en la carpeta predeterminada.<br /><br /> Si **1**, los archivos de instantáneas pueden encontrarse en la carpeta predeterminada.<br /><br /> Si **0**, los archivos de instantánea se almacenan en la ubicación alternativa especificada por **alt_snapshot_folder**. Las ubicaciones alternativas pueden encontrarse en otro servidor, en una unidad de red o en medios extraíbles (como CD-ROM o discos extraíbles). También puede guardar los archivos de instantáneas a un sitio FTP, para la recuperación por el suscriptor en un momento posterior.<br /><br /> Nota: Este parámetro puede ser true y seguir teniendo una ubicación la **alt_snapshot_folder** parámetro. Esta combinación especifica que los archivos de instantánea se almacenan tanto en la ubicación predeterminada como en la alternativa.|  
|alt_snapshot_folder|**nvarchar(255)**|Especifica la ubicación de la carpeta alternativa de la instantánea.|  
|pre_snapshot_script|**nvarchar(255)**|Especifica un puntero a un **.sql** scripts de archivo que el agente de mezcla se ejecuta antes que cualquiera de los objetos replicados al aplicar la instantánea en el suscriptor.|  
|post_snapshot_script|**nvarchar(255)**|Especifica un puntero a un **.sql** que el agente de mezcla se ejecuta después de todo el otro archivo de scripts de objetos replicados y datos se han aplicado durante la sincronización inicial.|  
|compress_snapshot|**bit**|Especifica que la instantánea que se escribe en el **alt_snapshot_folder** ubicación se comprime en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB.|  
|ftp_address|**sysname**|Es la dirección de red del servicio FTP para el distribuidor. Especifica dónde se encuentran el agente de mezcla recoger los archivos de instantánea de publicación.|  
|ftp_port|**int**|Es el número de puerto del servicio FTP para el distribuidor. **ftp_port** tiene un valor predeterminado de **21**. Especifica dónde se encuentran los archivos de instantánea de la publicación para que los recoja el Agente de mezcla.|  
|ftp_subdirectory|**nvarchar(255)**|Especifica dónde se encuentran los archivos de instantánea para que los recoja el Agente de mezcla cuando se envía la instantánea mediante FTP.|  
|ftp_login|**sysname**|Se usa el nombre de usuario para conectarse al servicio FTP.|  
|conflict_retention|**int**|Especifica el período de retención, expresado en días, durante el que se conservan los conflictos. Transcurrido el número de días especificado, se purga la fila del conflicto de la tabla de conflictos.|  
|keep_partition_changes|**int**|Especifica si se está optimizando la sincronización para esta publicación. **keep_partition_changes** tiene un valor predeterminado de **0**. Un valor de **0** significa que la sincronización no se optimiza y las particiones enviadas a todos los suscriptores se comprueban cuando cambian los datos en una partición.<br /><br /> **1** significa que la sincronización se optimiza y solo los suscriptores con filas en la partición modificada se ven afectados.<br /><br /> Nota: De forma predeterminada, las publicaciones de combinación utilizan particiones precalculadas, que proporciona un mayor grado de optimización que esta opción. Para obtener más información, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) y [optimizar el rendimiento de filtro con parámetros con particiones calculadas previamente](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).|  
|allow_subscription_copy|**int**|Especifica si se ha habilitado la capacidad de copiar las bases de datos de suscripciones que se suscriben a esta publicación. Un valor de **0** significa que no se permite la copia.|  
|allow_synctoalternate|**int**|Especifica si se permite un asociado de sincronización alternativo para sincronizar con este publicador. Un valor de **0** significa que no se permite un asociado de sincronización.|  
|validate_subscriber_info|**nvarchar(500)**|Enumera las funciones que se están utilizando para recuperar información del suscriptor y validar los criterios de filtrado de filas con parámetros del suscriptor. Ayuda a comprobar que se hayan creado particiones de la información de manera coherente con cada combinación.|  
|backward_comp_level|**int**|Nivel de compatibilidad de la base de datos, que puede ser uno de los que se especifican a continuación:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_activedirectory|**bit**|Especifica si la información de publicación se publica en Active Directory. Un valor de **0** significa que la información de publicación no está disponible desde Active Directory.<br /><br /> Este parámetro ha quedado desusado y solo se admite para la compatibilidad de scripts con versiones anteriores. Ya no es posible agregar información de publicación a Active Directory.|  
|max_concurrent_merge|**int**|Número de procesos de combinación simultáneos. Si **0**, no hay ningún límite al número de procesos de mezcla simultáneos que se ejecutan en un momento dado.|  
|max_concurrent_dynamic_snapshots|**int**|Número máximo de sesiones de instantáneas de datos filtrados simultáneas que se pueden ejecutar con la publicación de combinación. Si **0**, no hay ningún límite en el número máximo de sesiones de instantánea de datos filtrados simultáneas que se pueden ejecutar simultáneamente con la publicación en un momento dado.|  
|use_partition_groups|**int**|Determina si se utilizan particiones precalculadas. Un valor de **1** significa que las particiones precalculadas se utiliza.|  
|num_of_articles|**int**|Número de artículos de la publicación.|  
|replicate_ddl|**int**|Indica si se replican los cambios de esquema realizados en tablas publicadas. Un valor de **1** significa que se replican los cambios de esquema.|  
|publication_number|**smallint**|Número asignado a esta publicación.|  
|allow_subscriber_initiated_snapshot|**bit**|Determina si los suscriptores pueden iniciar el proceso de generación de instantáneas de datos filtrados. Un valor de **1** significa que los suscriptores pueden iniciar el proceso de instantáneas.|  
|allow_web_synchronization|**bit**|Determina si se habilita la publicación para sincronización web. Un valor de **1** significa que está habilitada la sincronización Web.|  
|web_synchronization_url|**nvarchar(500)**|Dirección URL de Internet que se usa para la sincronización web.|  
|allow_partition_realignment|**bit**|Determina si las eliminaciones se envían al suscriptor cuando la modificación de la fila en el publicador hace que se cambie su partición. Un valor de **1** significa que se envían eliminaciones al suscriptor.  Para obtener más información, consulte [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).|  
|retention_period_unit|**tinyint**|Define la unidad que se utiliza al definir la retención. Esto puede ser uno de los siguientes valores:<br /><br /> **0** = día<br /><br /> **1** = semana<br /><br /> **2** = mes<br /><br /> **3** = año|  
|has_downloadonly_articles|**bit**|Indica si alguno de los artículos pertenecientes a la publicación son artículos de solo descarga. Un valor de **1** indica que hay artículos de sólo descarga.|  
|decentralized_conflicts|**int**|Indica si los registros de los conflictos se almacenan en el suscriptor que provocó el conflicto. Un valor de **0** indica que no se almacenan los registros de conflictos en el suscriptor. El valor 1 indica que los registros de los conflictos se almacenan en el suscriptor.|  
|generation_leveling_threshold|**int**|Especifica el número de cambios que se encuentran en una generación. Una generación es un conjunto de cambios que se entregan a un publicador o a un suscriptor|  
|automatic_reinitialization_policy|**bit**|Indica si se cargan los cambios desde el suscriptor antes de que se produzca una reinicialización automática. Un valor de **1** indica que los cambios se cargan desde el suscriptor antes de que se produzca una reinicialización automática. El valor 0 indica que los cambios no se cargan antes de una reinicialización automática.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_helpmergepublication se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Los miembros de la lista de acceso a la publicación pueden ejecutar sp_helpmergepublication para esa publicación. Los miembros del rol fijo de base de datos db_owner en la base de datos de publicaciones pueden ejecutar sp_helpmergepublication para obtener información de todas las publicaciones.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_helpmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-helpmergepublication-_1.sql)]  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
