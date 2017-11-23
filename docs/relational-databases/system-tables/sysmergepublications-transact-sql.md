---
title: sysmergepublications (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysmergepublications
- sysmergepublications_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmergepublications system table
ms.assetid: 7f82c6c3-22d1-47c0-a92b-4d64b98cc455
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95059187ddd567212027d73dbd361e1ee9d2e7a7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergepublications-transact-sql"></a>sysmergepublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada publicación de combinación definida en la base de datos. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|Nombre del servidor predeterminado.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador predeterminado.|  
|**Nombre**|**sysname**|Nombre de la publicación.|  
|**Descripción**|**nvarchar(255)**|Descripción breve de la publicación.|  
|**retención**|**int**|El período de retención para el conjunto de toda la publicación, donde la unidad se indica mediante el valor de la **retention_period_unit** columna.|  
|**publication_type**|**tinyint**|Indica si la publicación se filtra:<br /><br /> **0** = no filtrada.<br /><br /> **1** = filtradas.|  
|**pubid**|**uniqueidentifier**|Número de identificación único para esta publicación. Se genera cuando se agrega la publicación.|  
|**DesignMasterID**|**uniqueidentifier**|Reservado para uso futuro.|  
|**parentid**|**uniqueidentifier**|Indica la publicación primaria a partir de la cual se creó la publicación del mismo nivel o subconjunto actual (utilizado en las topologías jerárquicas de publicación).|  
|**sync_mode**|**tinyint**|Modo de sincronización de esta publicación:<br /><br /> **0** = nativo.<br /><br /> **1** = carácter.|  
|**allow_push**|**int**|Indica si la publicación admite suscripciones de inserción.<br /><br /> **0** = no se admiten suscripciones de inserción.<br /><br /> **1** = se admiten suscripciones de inserción.|  
|**allow_pull**|**int**|Indica si la publicación admite suscripciones extracción.<br /><br /> **0** = no se admiten suscripciones de extracción.<br /><br /> **1** = se permiten suscripciones de extracción.|  
|**allow_anonymous**|**int**|Indica si la publicación admite suscripciones anónimas.<br /><br /> **0** = suscripciones anónimas no permitidas.<br /><br /> **1** = anónimo se permiten las suscripciones.|  
|**centralized_conflicts**|**int**|Indica si los registros de conflictos se almacenan en el publicador:<br /><br /> **0** = conflictos registros no se almacenan en el publicador.<br /><br /> **1** = los registros de conflictos se almacenan en el publicador.|  
|**status**|**tinyint**|Reservado para uso futuro.|  
|**snapshot_ready**|**tinyint**|Indica el estado de la instantánea de la publicación:<br /><br /> **0** = instantánea no está lista para su uso.<br /><br /> **1** = la instantánea está lista para su uso.<br /><br /> **2** = una nueva instantánea para esta publicación debe crearse.|  
|**enabled_for_internet**|**bit**|Indica si los archivos de sincronización de la publicación se exponen en Internet a través de FTP u otros servicios.<br /><br /> **0** = sincronización pueden tener acceso a archivos desde Internet.<br /><br /> **1** = la sincronización no se pueden tener acceso a archivos desde Internet.|  
|**dynamic_filters**|**bit**|Indica si la publicación se filtra utilizando un filtro de fila con parámetros.<br /><br /> **0** = la publicación se filtran por filas no.<br /><br /> **1** = la publicación se filtran por filas.|  
|**snapshot_in_defaultfolder**|**bit**|Especifica si los archivos de instantánea se almacenan en la carpeta predeterminada:<br /><br /> **0** = la instantánea de archivos se encuentran en la carpeta predeterminada.<br /><br /> **1** = la instantánea de archivos se almacenan en la ubicación especificada por **alt_snapshot_folder**.|  
|**alt_snapshot_folder**|**nvarchar(255)**|La ubicación de la carpeta alternativa de la instantánea.|  
|**pre_snapshot_script**|**nvarchar(255)**|Puntero a una. **sql** scripts de archivo que se ejecuta el agente de mezcla antes de cualquier objeto de replicación al aplicar la instantánea en el suscriptor.|  
|**post_snapshot_script**|**nvarchar(255)**|El puntero a una. **sql** archivo que el agente de mezcla se ejecuta después de que todos la demás replicación scripts de objetos y datos se aplicaron durante una sincronización inicial.|  
|**compress_snapshot**|**bit**|Especifica si la instantánea escrita en la **alt_snapshot_folder** ubicación se comprime en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** especifica que el archivo no está comprimido.|  
|**ftp_address**|**sysname**|Dirección de red del servicio de protocolo de transferencia de archivos (FTP) para el distribuidor. Especifica dónde se encuentran los archivos de instantánea de la publicación para que los recoja el Agente de mezcla, si se ha habilitado FTP.|  
|**ftp_port**|**int**|El número de puerto del servicio FTP para el distribuidor.|  
|**ftp_subdirectory**|**nvarchar(255)**|Subdirectorio en el que están disponibles los archivos de instantánea para que los recoja el Agente de mezcla.|  
|**ftp_login**|**sysname**|Nombre de usuario que se utiliza para conectarse al servicio FTP.|  
|**ftp_password**|**nvarchar (524)**|La contraseña de usuario utilizada para conectar con el servicio FTP.|  
|**conflict_retention**|**int**|Especifica el período de retención, expresado en días, durante el que se conservan los conflictos. Transcurrido ese tiempo, la fila del conflicto se limpia de la tabla de conflictos.|  
|**keep_before_values**|**int**|Especifica si se está optimizando la sincronización para esta publicación:<br /><br /> **0** = la sincronización no se optimiza y las particiones enviadas a todos los suscriptores se comprobarán cuando cambian los datos de una partición.<br /><br /> **1** = la sincronización se optimiza y solo los suscriptores que tienen filas en la partición modificada se ven afectados.|  
|**allow_subscription_copy**|**bit**|Especifica si se ha habilitado la capacidad para copiar la base de datos de suscripciones. **0** significa que no se permite la copia.|  
|**allow_synctoalternate**|**bit**|Especifica si se permite un asociado de sincronización alternativo para sincronizar con este publicador. **0** significa que no se permite un asociado de sincronización.|  
|**validate_subscriber_info**|**nvarchar (500)**|Enumera las funciones que se están utilizando para recuperar información del suscriptor y validar los criterios de filtrado de filas con parámetros del suscriptor.|  
|**ad_guidname**|**sysname**|Especifica si la información de publicación se publica en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Un GUID válido especifica que la publicación se publica en Active Directory, y el GUID es el objeto de publicación de Active Directory correspondiente **objectGUID**. Si es NULL, la publicación no se publica en Active Directory.|  
|**backward_comp_level**|**int**|Nivel de compatibilidad de base de datos. Puede ser uno de los siguientes valores:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**max_concurrent_merge**|**int**|Número máximo de procesos de mezcla simultáneos permitido. Un valor de **0** para esta propiedad significa que no hay ningún límite en el número de procesos de mezcla simultáneos que se ejecutan en un momento dado. Esta propiedad establece un límite en el número de procesos de mezcla simultáneos que se pueden ejecutar con una publicación de combinación en un momento determinado. Si hay más procesos de instantánea programados al mismo tiempo que los que permite ejecutar el valor, los trabajos sobrantes se colocarán en una cola y esperarán hasta que finalice el proceso de mezcla que se está ejecutando actualmente.|  
|**max_concurrent_dynamic_snapshots**|**int**|Número máximo de sesiones de instantánea de datos filtrados simultáneas que se pueden ejecutar con la publicación de combinación. Si **0**, no hay ningún límite para el número máximo de sesiones de instantánea de datos filtrados simultáneas que se pueden ejecutar simultáneamente con la publicación en un momento dado. Esta propiedad establece un límite en el número de procesos de instantánea simultáneos que se pueden ejecutar con una publicación de combinación en un momento determinado. Si hay más procesos de instantánea programados al mismo tiempo que los que permite ejecutar el valor, los trabajos sobrantes se colocarán en una cola y esperarán hasta que finalice el proceso de mezcla que se está ejecutando actualmente.|  
|**use_partition_groups**|**smallint**|Especifica si la publicación utiliza particiones precalculadas.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|Lista de funciones separadas por punto y coma que se utiliza en los filtros de fila con parámetros de la publicación.|  
|**partition_id_eval_proc**|**sysname**|Especifica el nombre del procedimiento ejecutado por el Agente de mezcla de un suscriptor para determinar su Id. de partición asignada.|  
|**publication_number**|**smallint**|Especifica la columna de identidad que proporciona una asignación de 2 bytes a **pubid**. **pubid** es un identificador único global para una publicación, mientras que el número de publicación solo es único en una base de datos especificada.|  
|**replicate_ddl**|**int**|Indica si se admite la replicación de esquemas para la publicación.<br /><br /> **0** = DDL no se replican las instrucciones.<br /><br /> **1** = DDL las instrucciones que se ejecuta en el publicador se replican.<br /><br /> Para más información, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|**allow_subscriber_initiated_snapshot**|**bit**|Indica que los suscriptores pueden iniciar el proceso que genera la instantánea para una publicación utilizando filtros con parámetros. **1** indica que los suscriptores pueden iniciar el proceso de instantáneas.|  
|**dynamic_snapshot_queue_timeout**|**int**|Especifica cuántos minutos debe esperar en la cola un suscriptor para que empiece el proceso de generación de instantáneas al utilizar filtros con parámetros.|  
|**dynamic_snapshot_ready_timeout**|**int**|Especifica cuántos minutos debe esperar un suscriptor para que empiece el proceso de generación de instantáneas al utilizar filtros con parámetros.|  
|**distribuidor**|**sysname**|Nombre del distribuidor de la publicación.|  
|**snapshot_jobid**|**binary (16)**|Identifica el trabajo de agente que genera la instantánea cuando el suscriptor puede iniciar el proceso de generación correspondiente.|  
|**allow_web_synchronization**|**bit**|Especifica si la publicación está habilitada para la sincronización Web, donde **1** significa que la sincronización Web está habilitada para la publicación.|  
|**web_synchronization_url**|**nvarchar (500)**|Especifica el valor predeterminado de la dirección URL de Internet utilizada para la sincronización web.|  
|**allow_partition_realignment**|**bit**|Indica si se envían eliminaciones al suscriptor cuando una modificación de la fila del publicador provoca que se modifique su partición.<br /><br /> **0** = datos desde una antigua partición se quedará en el suscriptor, donde no se replicarán los cambios realizados en estos datos en el publicador al suscriptor, pero los cambios realizados en el suscriptor se replicarán al publicador.<br /><br /> **1** = las eliminaciones al suscriptor para reflejar los resultados de un cambio en la partición mediante la eliminación de datos que no sea dejado de formar parte de la partición del suscriptor.<br /><br /> Para obtener más información, vea [sp_addmergepublication &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).<br /><br /> Nota: Los datos que permanecen en el suscriptor cuando este valor es **0** deben tratarse como si fueran de solo lectura; sin embargo, no aplica esta directriz estrictamente por el sistema de replicación.|  
|**retention_period_unit**|**tinyint**|Define la unidad utilizada al definir *retención*, que puede ser uno de estos valores:<br /><br /> **0** = día.<br /><br /> **1** = semana.<br /><br /> **2** = mes.<br /><br /> **3** = año.|  
|**decentralized_conflicts**|**int**|Indica si los registros de conflictos se almacenan en el suscriptor que provocó el conflicto:<br /><br /> **0** = conflictos registros no se almacenan en el suscriptor.<br /><br /> **1** = los registros de conflictos se almacenan en el suscriptor.|  
|**generation_leveling_threshold**|**int**|Especifica el número de cambios contenidos en una generación. Una generación es un conjunto de cambios que se entregan a un publicador o suscriptor.|  
|**automatic_reinitialization_policy**|**bit**|Indica si se cargan los cambios desde el suscriptor antes de que se produzca una reinicialización automática.<br /><br /> **1** = se cargan cambios desde el suscriptor antes de que se produzca una reinicialización automática.<br /><br /> **0** = cambios no se cargan antes una reinicialización automática.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)  
  
  
