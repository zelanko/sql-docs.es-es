---
title: Sys.Databases (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- databases
- databases_TSQL
- sys.databases
- sys.databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.databases catalog view
ms.assetid: 46c288c1-3410-4d68-a027-3bbf33239289
caps.latest.revision: 152
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fd67499570aec52824789d72ddf8333899e9ade7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566199"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si una base de datos no es `ONLINE`, o `AUTO_CLOSE` está establecido en `ON` y se cierra la base de datos, los valores de algunas columnas pueden ser `NULL`. Si una base de datos es `OFFLINE`, la fila correspondiente no es visible para los usuarios con pocos privilegios. Para ver la fila correspondiente si la base de datos `OFFLINE`, un usuario debe tener al menos el `ALTER ANY DATABASE` permiso de nivel de servidor, o el `CREATE DATABASE` permiso en el `master` base de datos.  
  

  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de base de datos, único en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dentro de un servidor de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**database_id**|**int**|Identificador de la base de datos, único en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dentro de un servidor de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**source_database_id**|**int**|Distinto de NULL = Id. de la base de datos de origen de esta instantánea de base de datos.<br /> NULL = No es una instantánea de base de datos.|  
|**owner_sid**|**varbinary(85)**|SID (identificador de seguridad) del propietario externo de la base de datos, según se ha registrado en el servidor. Para obtener información sobre quién puede poseer una base de datos, vea el **ALTER AUTHORIZATION para bases de datos** sección de [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).|  
|**create_date**|**datetime**|Fecha en que se creó o se cambió de nombre la base de datos. Para **tempdb**, este valor cambia cada vez que se reinicie el servidor.|  
|**COMPATIBILITY_LEVEL**|**tinyint**|Entero que corresponde a la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la que el comportamiento es compatible:<br /> **Valor** : **se aplica a**<br /> 70: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 80: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 90: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /> 100: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 110: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 120: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 130: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] |  
|**collation_name**|**sysname**|Intercalación de la base de datos. Actúa como la intercalación predeterminada en la base de datos.<br /> NULL = base de datos no está en línea o AUTO_CLOSE se establece en ON y se cierra la base de datos.|  
|**user_access**|**tinyint**|Configuración de acceso del usuario:<br /> 0 = Se ha especificado MULTI_USER<br /> 1 = Se ha especificado SINGLE_USER<br /> 2 = Se ha especificado RESTRICTED_USER|  
|**user_access_desc**|**nvarchar(60)**|Descripción de la configuración de acceso del usuario.|  
|**is_read_only**|**bit**|1 = La base de datos es READ_ONLY<br /> 0 = La base de datos es READ_WRITE|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE es ON<br /> 0 = AUTO_CLOSE es OFF|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK es ON<br /> 0 = AUTO_SHRINK es OFF|  
|**state**|**tinyint**|**Valor &#124; se aplica a**<br /> 0 = Con conexión  <br /> 1 = En restauración  <br /> 2 = en recuperación: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 3 = RECOVERY_PENDING: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 4 = Sospechoso  <br /> 5 = emergencia: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 6 = sin conexión: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 7 = LA COPIA: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /> 10 = OFFLINE_SECONDARY: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /><br /> **Nota:** siempre en las bases de datos, consultar el `database_state` o `database_state_desc` columnas de [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).|  
|**state_desc**|**nvarchar(60)**|Descripción del estado de la base de datos. Vea el estado.|  
|**is_in_standby**|**bit**|La base de datos es de solo lectura para RESTORE LOG.|  
|**is_cleanly_shutdown**|**bit**|1 = La base de datos se ha cerrado correctamente; no es necesaria la recuperación en el inicio<br /> 0 = La base de datos no se cerró correctamente; es necesaria la recuperación en el inicio|  
|**is_supplemental_logging_enabled**|**bit**|1 = SUPPLEMENTAL_LOGGING es ON<br /> 0 = SUPPLEMENTAL_LOGGING es OFF|  
|**snapshot_isolation_state**|**tinyint**|Estado permitido para las transacciones de aislamiento de instantánea, tal como se define en la opción ALLOW_SNAPSHOT_ISOLATION:<br /> 0 = El estado de aislamiento de instantánea es OFF (valor predeterminado). No se permite el aislamiento de instantánea.<br /> 1 = El estado de aislamiento de instantánea es ON. Se permite el aislamiento de instantánea.<br /> 2 = El estado de aislamiento de instantánea se encuentra en estado de transición a OFF. Se controlan las versiones de las modificaciones de todas las transacciones. No se pueden iniciar nuevas transacciones con aislamiento de instantánea. La base de datos permanece en estado de transición a OFF hasta que puedan completarse todas las transacciones que estaban activas cuando se ejecutó ALTER DATABASE.<br /> 3 = El estado de aislamiento de instantánea se encuentra en estado de transición a ON. Se controlan las versiones de las modificaciones de las transacciones nuevas. Las transacciones no pueden utilizar el aislamiento de instantánea hasta que el estado de aislamiento de instantánea sea 1 (ON). La base de datos permanece en estado de transición a ON hasta que puedan completarse todas las transacciones de actualización que estaban activas cuando se ejecutó ALTER DATABASE.|  
|**snapshot_isolation_state_desc**|**nvarchar(60)**|Descripción del estado de las transacciones de aislamiento de instantánea que se permiten, tal como se define en la opción ALLOW_SNAPSHOT_ISOLATION.|  
|**is_read_committed_snapshot_on**|**bit**|1 = la opción READ_COMMITTED_SNAPSHOT está en ON. Las operaciones de lectura en el nivel de aislamiento READ COMMITTED se basan en exámenes de instantáneas y no adquieren bloqueos.<br /> 0 = la opción READ_COMMITTED_SNAPSHOT está en OFF (valor predeterminado). Las operaciones de lectura en el nivel de aislamiento READ COMMITTED utilizan bloqueos compartidos.|  
|**recovery_model**|**tinyint**|Modelo de recuperación seleccionado:<br /> 1 = FULL<br /> 2 = BULK_LOGGED<br /> 3 = SIMPLE|  
|**recovery_model_desc**|**nvarchar(60)**|Descripción del modelo de recuperación seleccionado.|  
|**page_verify_option**|**tinyint**|Valor de la opción PAGE_VERIFY:<br /> 0 = NONE<br /> 1 = TORN_PAGE_DETECTION<br /> 2 = CHECKSUM|  
|**page_verify_option_desc**|**nvarchar(60)**|Descripción del valor de la opción PAGE_VERIFY.|  
|**is_auto_create_stats_on**|**bit**|1 = AUTO_CREATE_STATISTICS es ON<br /> 0 = AUTO_CREATE_STATISTICS es OFF|  
|**is_auto_create_stats_incremental_on**|**bit**|Indica la configuración predeterminada para la opción incremental de auto stats.<br /> 0 = auto create stats no es incremental<br /> 1 = auto crear estadísticas son incrementales si es posible<br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**is_auto_update_stats_on**|**bit**|1 = AUTO_UPDATE_STATISTICS es ON<br /> 0 = AUTO_UPDATE_STATISTICS es OFF|  
|**is_auto_update_stats_async_on**|**bit**|1 = AUTO_UPDATE_STATISTICS_ASYNC es ON<br /> 0 = AUTO_UPDATE_STATISTICS_ASYNC es OFF|  
|**is_ansi_null_default_on**|**bit**|1 = ANSI_NULL_DEFAULT es ON<br /> 0 = ANSI_NULL_DEFAULT is OFF|  
|**is_ansi_nulls_on**|**bit**|1 = ANSI_NULLS es ON<br /> 0 = ANSI_NULLS es OFF|  
|**is_ansi_padding_on**|**bit**|1 = ANSI_PADDING es ON<br /> 0 = ANSI_PADDING es OFF|  
|**is_ansi_warnings_on**|**bit**|1 = ANSI_WARNINGS es ON<br /> 0 = ANSI_WARNINGS es OFF|  
|**is_arithabort_on**|**bit**|1 = ARITHABORT es ON<br /> 0 = ARITHABORT es OFF|  
|**is_concat_null_yields_null_on**|**bit**|1 = CONCAT_NULL_YIELDS_NULL es ON<br /> 0 = CONCAT_NULL_YIELDS_NULL es OFF|  
|**is_numeric_roundabort_on**|**bit**|1 = NUMERIC_ROUNDABORT es ON<br /> 0 = NUMERIC_ROUNDABORT es OFF|  
|**is_quoted_identifier_on**|**bit**|1 = QUOTED_IDENTIFIER es ON<br /> 0 = QUOTED_IDENTIFIER es OFF|  
|**is_recursive_triggers_on**|**bit**|1 = RECURSIVE_TRIGGERS es ON<br /> 0 = RECURSIVE_TRIGGERS es OFF|  
|**is_cursor_close_on_commit_on**|**bit**|1 = CURSOR_CLOSE_ON_COMMIT es ON<br /> 0 = CURSOR_CLOSE_ON_COMMIT es OFF|  
|**is_local_cursor_default**|**bit**|1 = CURSOR_DEFAULT es local<br /> 0 = CURSOR_DEFAULT es global|  
|**is_fulltext_enabled**|**bit**|1 = La búsqueda de texto completo está habilitada para la base de datos<br /> 0 = La búsqueda de texto completo está deshabilitada para la base de datos|  
|**is_trustworthy_on**|**bit**|1 = La base de datos se ha marcado como de confianza<br /> 0 = La base de datos no se ha marcado como de confianza|  
|**is_db_chaining_on**|**bit**|1 = El encadenamiento de propiedad entre bases de datos es ON<br /> 0 = El encadenamiento de propiedad entre bases de datos es OFF|  
|**is_parameterization_forced**|**bit**|1 = La parametrización es FORCED<br /> 0 = La parametrización es SIMPLE|  
|**is_master_key_encrypted_by_server**|**bit**|1 = La base de datos tiene una clave maestra cifrada<br /> 0 = La base de datos no tiene una clave maestra cifrada|  
|**is_query_store_on**|**bit**|1 = la consulta de almacén está habilitado para esta base de datos. Comprobar [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) para ver el estado del almacén de consultas.<br /> 0 = la consulta de almacén no está habilitado<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
|**is_published**|**bit**|1 = La base de datos es una base de datos de publicación en una topología de replicación transaccional o de instantáneas<br /> 0 = No es una base de datos de publicación|  
|**is_subscribed**|**bit**|Esta columna no se utiliza. Devolverá siempre 0, cualquiera que sea el estado de suscriptor de la base de datos.|  
|**is_merge_published**|**bit**|1 = La base de datos es una base de datos de publicación en una topología de replicación de mezcla<br /> 0 = No es una base de datos de publicación en una topología de replicación de mezcla|  
|**is_distributor**|**bit**|1 = La base de datos es la base de datos de distribución para una topología de replicación<br /> 0 = No es la base de datos de distribución para una topología de replicación|  
|**is_sync_with_backup**|**bit**|1 = La base de datos está marcada para la sincronización de replicación con la copia de seguridad<br /> 0 = No está marcada para la sincronización de replicación con la copia de seguridad|  
|**service_broker_guid**|**uniqueidentifier**|Identificador de Service Broker de esta base de datos. Usar como el **broker_instance** del destino en la tabla de enrutamiento.|  
|**is_broker_enabled**|**bit**|1 = Service Broker envía y recibe mensajes para esta base de datos.<br /> 0 = Todos los mensajes enviados permanecerán en la cola de transmisión y los mensajes recibidos no se enviarán a ninguna cola en esta base de datos.<br /> De manera predeterminada, las bases de datos restauradas o adjuntadas tienen Service Broker deshabilitado. La excepción es la creación de reflejo de bases de datos, donde el agente se habilita tras una conmutación por error.|  
|**log_reuse_wait**|**tinyint**|Reutilización del espacio de registro de transacciones está a la espera en uno de los siguientes a partir del último punto de comprobación. (Para obtener explicaciones detalladas de estos valores, consulte [el registro de transacciones](../../relational-databases/logs/the-transaction-log-sql-server.md).)<br /> 0 = Nada<br />   1 = Checkpoint (cuando una base de datos utiliza un modelo de recuperación y tiene un grupo de archivos de datos optimizados para memoria, debe esperar que la columna log_reuse_wait indique checkpoint o xtp_checkpoint). **Se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  2 = copia del registro **se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  3 = copia de seguridad activa o restaurar **se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  4 = transacción activa **se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  5 = la creación de reflejo de base de datos **se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  6 = replicación **se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  7 = creación de instantáneas de base de datos **se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  8 = examen del registro **se aplica a**<br />  9 = una grupos de disponibilidad AlwaysOn réplica secundaria está aplicando entradas del registro de transacciones de esta base de datos a una base de datos secundaria correspondiente. **Se aplica a** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. En versiones anteriores de SQL Server, 9 = Otra (transitoria).<br />  10 = solo para uso interno **se aplica a** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  11 = solo para uso interno **se aplica a** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 12 = solo para uso interno **se aplica a** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />13 = página más antigua **se aplica a** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 14 = otra **se aplica a** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  16 = XTP_CHECKPOINT (cuando una base de datos utiliza un modelo de recuperación y tiene un grupo de archivos de datos optimizados para memoria, debe esperar que la columna log_reuse_wait indique checkpoint o xtp_checkpoint). **Se aplica a** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**log_reuse_wait_desc**|**nvarchar(60)**|Descripción de las situaciones debido a las cuales el proceso de reutilización del espacio del registro de transacciones está a la espera como último punto de comprobación:|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION es ON<br /> 0 = DATE_CORRELATION_OPTIMIZATION es OFF|  
|**is_cdc_enabled**|**bit**|1 = La base de datos está habilitada para la captura de datos modificados. Para obtener más información, consulte [sys.sp_cdc_enable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md).|  
|**is_encrypted**|**bit**|Indica si la base de datos está cifrada (refleja el último estado establecido mediante la cláusula ALTER DATABASE SET ENCRYPTION). Puede ser uno de los siguientes valores:<br /> 1 = Cifrada<br /> 0 = No cifrada<br /> Para obtener más información sobre el cifrado de bases de datos, vea [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).<br /> Si la base de datos está en proceso de descifrado, **is_encrypted** muestra un valor de 0. Puede ver el estado del proceso de cifrado mediante la [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) vista de administración dinámica.|  
|**is_honor_broker_priority_on**|**bit**|Indica si la base de datos sigue las prioridades de conversación (refleja el último estado establecido mediante la cláusula ALTER DATABASE SET HONOR_BROKER_PRIORITY). Puede ser uno de los siguientes valores:<br /> 1 = HONOR_BROKER_PRIORITY es ON<br /> 0 = HONOR_BROKER_PRIORITY es OFF|  
|**replica_id**|**uniqueidentifier**|Identificador único de la réplica de disponibilidad [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] local del grupo de disponibilidad, si existe, en el que la base de datos está participando.<br /> NULL = la base de datos no forma parte de una réplica de disponibilidad en el grupo de disponibilidad.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|Identificador único de la base de datos dentro de un grupo disponibilidad AlwaysOn, si hay alguno, en el que participa la base de datos. **group_database_id** es el mismo para esta base de datos en la réplica principal y en cada réplica secundaria en el que la base de datos se ha unido al grupo de disponibilidad.<br /> NULL = la base de datos no forma parte de una réplica de disponibilidad en ningún grupo de disponibilidad.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|Identificador del grupo de recursos de servidor asignado a esta base de datos. Este grupo de recursos de servidor controla la memoria total disponible para las tablas optimizadas para memoria en esta base de datos.<br /> **Se aplica a**: de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**default_language_lcid**|**smallint**|Indica el identificador local (LCID) del idioma predeterminado de una base de datos independiente.<br /> **Tenga en cuenta** funciona como el [configurar el idioma predeterminado Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) de **sp_configure**. Este valor es **null** para una base de datos dependiente.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|Indica el idioma predeterminado de una base de datos independiente.<br /> Este valor es **null** para una base de datos dependiente.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|Indica el identificador local (lcid) del idioma de texto completo predeterminado de la base de datos independiente.<br /> **Tenga en cuenta** funciona como el valor predeterminado [configurar el idioma de texto completo predeterminado Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) de **sp_configure**. Este valor es **null** para una base de datos dependiente.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|Indica el idioma de texto completo predeterminado de la base de datos independiente.<br /> Este valor es **null** para una base de datos dependiente.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|Indica si se permiten o no desencadenadores anidados en la base de datos independiente.<br /> 0 = no se permiten desencadenadores anidados<br /> 1 = se permiten desencadenadores anidados<br /> **Tenga en cuenta** funciona como el [establecer la opción de configuración del servidor de desencadenadores anidados](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) de **sp_configure**. Este valor es **null** para una base de datos dependiente. Consulte [sys.configurations &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obtener más información.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|Indica si las palabras irrelevantes deben transformarse o no en la base de datos independiente.<br /> 0 = las palabras irrelevantes no deben transformarse.<br /> 1 = las palabras irrelevantes deben transformarse.<br /> **Tenga en cuenta** funciona como el [transformar palabras irrelevantes Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) de **sp_configure**. Este valor es **null** para una base de datos dependiente. Consulte [sys.configurations &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obtener más información.<br /> **Se aplica a**: de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**two_digit_year_cutoff**|**smallint**|Indica un valor de un número comprendido entre 1753 y 9999 que representa el año límite para interpretar años de dos dígitos como años de cuatro dígitos.<br /> **Tenga en cuenta** funciona como el [configurar two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) de **sp_configure**. Este valor es **null** para una base de datos dependiente. Consulte [sys.configurations &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obtener más información.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**containment**|**tinyint no null**|Indica el estado de contención de la base de datos.<br />  0 = el estado de contención de la base de datos es off. **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = base de datos está en estado de contención parcial **se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**containment_desc**|**nvarchar (60) no es null**|Indica el estado de contención de la base de datos.<br /> NONE = base de datos heredada (contención cero)<br /> PARTIAL = base de datos parcialmente independiente<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|Tiempo estimado para recuperar la base de datos, en segundos. Acepta valores NULL.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|El valor de durabilidad diferida:<br /> 0 = DESHABILITADO<br /> 1 = PERMITIDO<br /> 2 = FORZADA<br /> Para saber más, vea [Control de la durabilidad de las transacciones](../../relational-databases/logs/control-transaction-durability.md).<br /> **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**delayed_durability_desc**|**nvarchar(60)**|El valor de durabilidad diferida:<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> **Se aplica a**: de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**memory_optimized_elevate_to_snapshot**|**bit**|Se tiene acceso a las tablas con optimización en memoria mediante el aislamiento de instantánea cuando el valor de configuración TRANSACTION ISOLATION LEVEL de la sesión se establece en un nivel de aislamiento inferior, READ COMMITTED o READ UNCOMMITTED.<br /> 1 = El nivel de aislamiento mínimo es SNAPSHOT.<br /> 0 = El nivel de aislamiento no se eleva.|  
|**is_federation_member**|**bit**|Indica si la base de datos es miembro de una federación.<br /> **Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|Indica si la base de datos se ajusta.<br /> 0 = la base de datos no está habilitada para Stretch.<br /> 1 = la base de datos está habilitada para Stretch.<br /> **Se aplica a**: de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> Para obtener más información, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).|  
|**is_mixed_page_allocation_on**|**bit**|Indica si las tablas e índices en la base de datos pueden asignar páginas iniciales desde extensiones mixtas.<br /> 0 = las tablas y los índices de la base de datos siempre asignan páginas iniciales desde extensiones uniformes.<br /> 1 = las tablas y los índices de la base de datos pueden asignar páginas iniciales desde extensiones mixtas.<br /> **Se aplica a**: de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> Para obtener más información, vea la opción SET MIXED_PAGE_ALLOCATION de [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**is_temporal_retention_enabled**|**bit**|Indica si la tarea de limpieza de directiva de retención temporal está habilitada.<br /> **Se aplica a**: base de datos SQL Azure|
|**catalog_collation_type**|**int**|La configuración de intercalación de catálogo:<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **Se aplica a**: base de datos SQL Azure|
|**catalog_collation_type_desc**|**nvarchar(60)**|La configuración de intercalación de catálogo:<br />DATABASE_DEFAULT<br />SQL_Latin_1_General_CP1_CI_AS<br /> **Se aplica a**: base de datos SQL Azure|
  
## <a name="permissions"></a>Permisos  
 Si el llamador de `sys.databases` no es el propietario de la base de datos y la base de datos no es `master` o `tempdb`, los permisos mínimos necesarios para ver la fila correspondiente son `ALTER ANY DATABASE` o `VIEW ANY DATABASE` permiso de nivel de servidor o `CREATE DATABASE` permiso en el `master` base de datos. Siempre puede verse en la base de datos al que está conectado el autor de llamada `sys.databases`.  
  
> [!IMPORTANT]  
>  De forma predeterminada, el rol público tiene el `VIEW ANY DATABASE` permiso, lo que permite todos los inicios de sesión ver información de la base de datos. Para bloquear el inicio de sesión de la capacidad para detectar una base de datos, `REVOKE` el `VIEW ANY DATABASE` permiso desde `public`, o `DENY` el ' permiso VIEW ANY DATABASE para inicios de sesión individuales.  
  
## <a name="includesssdsincludessssds-mdmd-remarks"></a>Comentarios para [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], esta vista está disponible en el `master` base de datos y en las bases de datos de usuario. En el `master` base de datos, esta vista devuelve la información sobre la `master` base de datos y todas las bases de datos de usuario en el servidor. En una base de datos de usuario, esta vista solo devuelve información sobre la base de datos actual y la base de datos maestra.  
  
 Utilice la vista `sys.databases` de la base de datos `master` del servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] donde ser va a crear la nueva base de datos. Cuando se inicia la copia de base de datos, puede consultar el `sys.databases` y `sys.dm_database_copies` vistas desde el `master` base de datos del servidor de destino para recuperar más información sobre el progreso de la copia.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-query-the-sysdatabases-view"></a>A. Consultar la vista sys.databases  
 El ejemplo siguiente devuelve algunas de las columnas disponibles en la `sys.databases` vista.  
  
```  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-includesssdsincludessssds-mdmd"></a>B. Comprobar el estado de copia en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 El ejemplo siguiente se consulta el `sys.databases` y `sys.dm_database_copies` vistas para devolver información sobre una base de datos de la operación de copia.  
  
**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
  
```  
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```  
### <a name="c-check-the-temporal-retention-policy-status-in-includesssdsincludessssds-mdmd"></a>C. Comprobar el estado de la directiva de retención temporal en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 El ejemplo siguiente se consulta el `sys.databases` para devolver información si la tarea de limpieza de retención temporal está habilitada. Tenga en cuenta que después de la operación de restauración de retención temporal está deshabilitada de forma predeterminada. Use `ALTER DATABASE` para habilitar de forma explícita.
  
**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [Sys.database_recovery_status &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)   
 [Vistas de catálogo de archivos y bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [sys.dm_database_copies &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
  
  
