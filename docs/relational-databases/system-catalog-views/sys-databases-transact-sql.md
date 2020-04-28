---
title: Sys. Databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5b9b5147621fb459e419a29e0a31f9ad9381eb77
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "77147400"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Contiene una fila por cada base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Si una base de datos `ONLINE`no es `AUTO_CLOSE` o se establece `ON` en y la base de datos está cerrada, los valores de algunas `NULL`columnas pueden ser. Si una base de `OFFLINE`datos es, la fila correspondiente no es visible para los usuarios con pocos privilegios. Para ver la fila correspondiente si la base de `OFFLINE`datos es, un usuario debe tener al `ALTER ANY DATABASE` menos el permiso de nivel de servidor `CREATE DATABASE` o el permiso `master` en la base de datos.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre de base de datos, único en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dentro de un servidor de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**database_id**|**int**|Identificador de la base de datos, único en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dentro de un servidor de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**source_database_id**|**int**|Distinto de NULL = Id. de la base de datos de origen de esta instantánea de base de datos.<br /> NULL = No es una instantánea de base de datos.|  
|**owner_sid**|**varbinary(85)**|SID (identificador de seguridad) del propietario externo de la base de datos, según se ha registrado en el servidor. Para obtener información sobre quién puede poseer una base de datos, vea la sección **ALTER Authorization for** Databases de [ALTER Authorization](../../t-sql/statements/alter-authorization-transact-sql.md).|  
|**create_date**|**datetime**|Fecha en que se creó o se cambió de nombre la base de datos. En el caso de **tempdb**, este valor cambia cada vez que se reinicia el servidor.|  
|**compatibility_level**|**tinyint**|Entero que corresponde a la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la que el comportamiento es compatible:<br /> **Valor** &#124; **se aplica a**<br /> 70 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 80 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 90 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /> 100 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores y[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 110 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores y[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 120 &#124; [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores y[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 130 &#124; [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones posteriores<br /> 140 &#124; [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] y versiones posteriores <br /> 150 &#124;[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]  |  
|**collation_name**|**sysname**|Intercalación de la base de datos. Actúa como la intercalación predeterminada en la base de datos.<br /> NULL = la base de datos no está en línea o AUTO_CLOSE está establecida en ON y la base de datos está cerrada.|  
|**user_access**|**tinyint**|Configuración de acceso del usuario:<br /> 0 = Se ha especificado MULTI_USER<br /> 1 = Se ha especificado SINGLE_USER<br /> 2 = Se ha especificado RESTRICTED_USER|  
|**user_access_desc**|**nvarchar(60)**|Descripción de la configuración de acceso del usuario.|  
|**is_read_only**|**bit**|1 = La base de datos es READ_ONLY<br /> 0 = La base de datos es READ_WRITE|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE es ON<br /> 0 = AUTO_CLOSE es OFF|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK es ON<br /> 0 = AUTO_SHRINK es OFF|  
|**state**|**tinyint**|**Valor &#124; se aplica a**<br /> 0 = Con conexión  <br /> 1 = En restauración  <br /> 2 = RECUPERAndo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] &#124; y versiones posteriores<br /> 3 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de RECOVERY_PENDING y versiones posteriores<br /> 4 = Sospechoso  <br /> 5 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de emergencia y versiones posteriores<br /> 6 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sin conexión y versiones posteriores<br /> 7 = COPIAndo [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] &#124;[!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /> 10 = &#124; [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] de OFFLINE_SECONDARY[!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /><br /> **Nota:** En el caso de las bases de datos `database_state` de `database_state_desc` Always On, consulte las columnas o de [Sys. dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).|  
|**state_desc**|**nvarchar(60)**|Descripción del estado de la base de datos. Vea estado.|  
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
|**is_auto_create_stats_incremental_on**|**bit**|Indica la configuración predeterminada para la opción incremental de auto stats.<br /> 0 = auto create stats no es incremental<br /> 1 = la creación automática de estadísticas es incremental si es posible<br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.|  
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
|**is_trustworthy_on**|**bit**|1 = La base de datos se ha marcado como de confianza<br /> 0 = La base de datos no se ha marcado como de confianza<br /> De forma predeterminada, las bases de datos restauradas o adjuntas tienen la confianza no habilitada.|  
|**is_db_chaining_on**|**bit**|1 = El encadenamiento de propiedad entre bases de datos es ON<br /> 0 = El encadenamiento de propiedad entre bases de datos es OFF|  
|**is_parameterization_forced**|**bit**|1 = La parametrización es FORCED<br /> 0 = La parametrización es SIMPLE|  
|**is_master_key_encrypted_by_server**|**bit**|1 = La base de datos tiene una clave maestra cifrada<br /> 0 = La base de datos no tiene una clave maestra cifrada|  
|**is_query_store_on**|**bit**|1 = el almacén de consultas está habilitado para esta base de datos. Compruebe [Sys. database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) para ver el estado del almacén de consultas.<br /> 0 = el almacén de consultas no está habilitado<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones posteriores)|  
|**is_published**|**bit**|1 = La base de datos es una base de datos de publicación en una topología de replicación transaccional o de instantáneas<br /> 0 = No es una base de datos de publicación|  
|**is_subscribed**|**bit**|Esta columna no se utiliza. Devolverá siempre 0, cualquiera que sea el estado de suscriptor de la base de datos.|  
|**is_merge_published**|**bit**|1 = La base de datos es una base de datos de publicación en una topología de replicación de mezcla<br /> 0 = No es una base de datos de publicación en una topología de replicación de mezcla|  
|**is_distributor**|**bit**|1 = La base de datos es la base de datos de distribución para una topología de replicación<br /> 0 = No es la base de datos de distribución para una topología de replicación|  
|**is_sync_with_backup**|**bit**|1 = La base de datos está marcada para la sincronización de replicación con la copia de seguridad<br /> 0 = No está marcada para la sincronización de replicación con la copia de seguridad|  
|**service_broker_guid**|**uniqueidentifier**|Identificador de Service Broker de esta base de datos. Se utiliza como **broker_instance** del destino de la tabla de enrutamiento.|  
|**is_broker_enabled**|**bit**|1 = Service Broker envía y recibe mensajes para esta base de datos.<br /> 0 = Todos los mensajes enviados permanecerán en la cola de transmisión y los mensajes recibidos no se enviarán a ninguna cola en esta base de datos.<br /> De manera predeterminada, las bases de datos restauradas o adjuntadas tienen Service Broker deshabilitado. La excepción es la creación de reflejo de bases de datos, donde el agente se habilita tras una conmutación por error.|  
|**log_reuse_wait**|**tinyint**|La reutilización del espacio del registro de transacciones está esperando actualmente uno de los siguientes elementos en el último punto de comprobación. Para obtener explicaciones más detalladas de estos valores, consulte [el registro de transacciones](../../relational-databases/logs/the-transaction-log-sql-server.md).<br /> **Valor &#124; se aplica a**<br /> 0 = Nada<br />   1 = punto de control (cuando una base de datos utiliza un modelo de recuperación y tiene un grupo de archivos de datos optimizados `log_reuse_wait` para memoria, debe ver que la columna [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] indica el punto de control o el xtp_checkpoint). &#124; y versiones posteriores<br />  2 = copia de seguridad [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de registros &#124; y versiones posteriores<br />  3 = copia de seguridad o restauración [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] activa &#124; y versiones posteriores<br />  4 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de transacciones activas y versiones posteriores<br />  5 = creación de reflejo de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] la base de datos &#124; y versiones posteriores<br />  6 = replicación &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores<br />  7 = creación de instantáneas [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de base de datos &#124; y versiones posteriores<br />  8 = Examen de registro <br />  9 = una réplica secundaria de los grupos de disponibilidad Always On está aplicando las entradas del registro de transacciones de esta base de datos a una base de datos secundaria correspondiente. &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores<br />  9 = otros (transitorios) &#124; hasta e incluyendo[!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]<br />  10 = solo para uso interno &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores<br />  11 = solo para uso interno &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores<br /> 12 = solo para uso interno &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores<br />13 = página más antigua [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] &#124; y versiones posteriores<br /> 14 = otros &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores<br />  16 = XTP_CHECKPOINT (cuando una base de datos utiliza un modelo de recuperación y tiene un grupo de archivos de datos optimizados para memoria, debe ver que la columna log_reuse_wait indica el [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] punto de control o xtp_checkpoint). &#124; y versiones posteriores|  
|**log_reuse_wait_desc**|**nvarchar(60)**|Descripción de las situaciones debido a las cuales el proceso de reutilización del espacio del registro de transacciones está a la espera como último punto de comprobación:|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION es ON<br /> 0 = DATE_CORRELATION_OPTIMIZATION es OFF|  
|**is_cdc_enabled**|**bit**|1 = La base de datos está habilitada para la captura de datos modificados. Para obtener más información, vea [Sys. sp_cdc_enable_db &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md).|  
|**is_encrypted**|**bit**|Indica si la base de datos está cifrada (refleja el último estado establecido `ALTER DATABASE SET ENCRYPTION` mediante la cláusula). Puede ser uno de los siguientes valores:<br /> 1 = Cifrada<br /> 0 = No cifrada<br /> Para obtener más información sobre el cifrado de bases de datos, vea [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).<br /> Si la base de datos está en proceso de descifrado, `is_encrypted` muestra un valor de 0. Puede ver el estado del proceso de cifrado mediante la vista de administración dinámica [Sys. dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .|  
|**is_honor_broker_priority_on**|**bit**|Indica si la base de datos respeta las prioridades de conversación (refleja el último estado establecido `ALTER DATABASE SET HONOR_BROKER_PRIORITY` mediante la cláusula). Puede ser uno de los siguientes valores:<br /> 1 = HONOR_BROKER_PRIORITY es ON<br /> 0 = HONOR_BROKER_PRIORITY es OFF<br /> De forma predeterminada, las bases de datos restauradas o adjuntas tienen la prioridad de Broker desactivada.|  
|**replica_id**|**uniqueidentifier**|Identificador único de la réplica de disponibilidad [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] local del grupo de disponibilidad, si existe, en el que la base de datos está participando.<br /> NULL = la base de datos no forma parte de una réplica de disponibilidad en el grupo de disponibilidad.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|Identificador único de la base de datos dentro de un Always On grupo de disponibilidad, si existe, en el que está participando la base de datos. **group_database_id** es el mismo para esta base de datos en la réplica principal y en cada réplica secundaria en la que la base de datos se ha unido al grupo de disponibilidad.<br /> NULL = la base de datos no forma parte de una réplica de disponibilidad en ningún grupo de disponibilidad.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|Identificador del grupo de recursos de servidor asignado a esta base de datos. Este grupo de recursos de servidor controla la memoria total disponible para las tablas optimizadas para memoria en esta base de datos.<br /> **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores|  
|**default_language_lcid**|**smallint**|Indica el identificador local (LCID) del idioma predeterminado de una base de datos independiente.<br /> **Nota:** Funciona como la [opción de configuración del servidor idioma predeterminado](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) de `sp_configure`. Este valor es **null** para una base de datos dependiente.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|Indica el idioma predeterminado de una base de datos independiente.<br /> Este valor es **null** para una base de datos dependiente.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|Indica el ID. de configuración regional (LCID) del idioma de texto completo predeterminado de la base de datos independiente.<br /> **Nota:** Funciona como valor predeterminado de [la opción de configuración del servidor idioma de texto completo predeterminado](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) de `sp_configure`. Este valor es **null** para una base de datos dependiente.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|Indica el idioma de texto completo predeterminado de la base de datos independiente.<br /> Este valor es **null** para una base de datos dependiente.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|Indica si se permiten o no desencadenadores anidados en la base de datos independiente.<br /> 0 = no se permiten desencadenadores anidados<br /> 1 = se permiten desencadenadores anidados<br /> **Nota:** Funciona como la [opción de configuración del servidor desencadenadores anidados](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) de `sp_configure`. Este valor es **null** para una base de datos dependiente. Vea [Sys. configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obtener más información.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|Indica si las palabras irrelevantes deben transformarse o no en la base de datos independiente.<br /> 0 = las palabras irrelevantes no deben transformarse.<br /> 1 = las palabras irrelevantes deben transformarse.<br /> **Nota:** Funciona como la [opción de configuración del servidor transformar palabras irrelevantes](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) de `sp_configure`. Este valor es **null** para una base de datos dependiente. Vea [Sys. configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obtener más información.<br /> **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores|  
|**two_digit_year_cutoff**|**smallint**|Indica un valor de un número comprendido entre 1753 y 9999 que representa el año límite para interpretar años de dos dígitos como años de cuatro dígitos.<br /> **Nota:** Funciona como la [opción de configuración del servidor fecha límite de año de dos dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) de `sp_configure`. Este valor es **null** para una base de datos dependiente. Vea [Sys. configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obtener más información.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**contención**|**tinyint not null**|Indica el estado de contención de la base de datos.<br />  0 = el estado de contención de la base de datos es off. **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = la base de datos está en contención parcial [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] se **aplica a**: y versiones posteriores|  
|**containment_desc**|**nvarchar (60) not null**|Indica el estado de contención de la base de datos.<br /> NONE = base de datos heredada (contención cero)<br /> PARTIAL = base de datos parcialmente independiente<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|Tiempo estimado para recuperar la base de datos, en segundos. Acepta valores NULL.<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|La configuración de durabilidad diferida:<br /> 0 = DESHABILITADO<br /> 1 = PERMITIDO<br /> 2 = FORZADA<br /> Para saber más, vea [Control de la durabilidad de las transacciones](../../relational-databases/logs/control-transaction-durability.md).<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability_desc**|**nvarchar(60)**|La configuración de durabilidad diferida:<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_memory_optimized_elevate_to_snapshot_on**|**bit**|Se tiene acceso a las tablas con optimización en memoria mediante el aislamiento de instantánea cuando el valor de configuración TRANSACTION ISOLATION LEVEL de la sesión se establece en un nivel de aislamiento inferior, READ COMMITTED o READ UNCOMMITTED.<br /> 1 = El nivel de aislamiento mínimo es SNAPSHOT.<br /> 0 = El nivel de aislamiento no se eleva.|  
|**is_federation_member**|**bit**|Indica si la base de datos es miembro de una federación.<br /> **Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|Indica si la base de datos está ajustada.<br /> 0 = la base de datos no está habilitada para Stretch.<br /> 1 = la base de datos está habilitada para Stretch.<br /> **Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones posteriores<br /> Para obtener más información, vea [Stretch Database](../../sql-server/stretch-database/stretch-database.md).|  
|**is_mixed_page_allocation_on**|**bit**|Indica si las tablas e índices de la base de datos pueden asignar páginas iniciales de extensiones mixtas.<br /> 0 = las tablas y los índices de la base de datos siempre asignan páginas iniciales de extensiones uniformes.<br /> 1 = las tablas y los índices de la base de datos pueden asignar páginas iniciales de extensiones mixtas.<br /> **Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones posteriores<br /> Para obtener más información, vea la opción SET MIXED_PAGE_ALLOCATION de [Opciones de ALTER DATABASE set &#40;&#41;de Transact-SQL ](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**is_temporal_retention_enabled**|**bit**|Indica si la tarea de limpieza de directiva de retención temporal está habilitada.<br /> **Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type**|**int**|La configuración de intercalación del catálogo:<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type_desc**|**nvarchar(60)**|La configuración de intercalación del catálogo:<br />DATABASE_DEFAULT<br />SQL_Latin_1_General_CP1_CI_AS<br /> **Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**is_result_set_caching_on**|**bit**|1 = is_result_set_caching_on está activada</br>0 = is_result_set_caching_on está desactivado</br>**Se aplica a**: Azure SQL Data Warehouse de la segunda generación. Aunque esta característica se está implantando en todas las regiones, Compruebe la versión implementada en la instancia de y las notas de la versión más recientes de [Azure SQL DW](/azure/sql-data-warehouse/release-notes-10-0-10106-0) para disponibilidad de características.|
|**is_memory_optimized_enabled**|**bit**|Indica si ciertas características en memoria, como el [grupo de búferes híbridos](../../database-engine/configure-windows/hybrid-buffer-pool.md), están habilitadas para la base de datos. No refleja la disponibilidad o el estado de configuración de [OLTP en memoria](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). <br />**Se aplica a**: SQL Server 2019 (15. x)|
  
## <a name="permissions"></a>Permisos

 Si el autor de la `sys.databases` llamada de no es el propietario de la base de datos y `master` la `tempdb`base de datos no es o, los permisos mínimos necesarios `ALTER ANY DATABASE` para ver `VIEW ANY DATABASE` la fila correspondiente son o el `CREATE DATABASE` permiso de nivel `master` de servidor, o el permiso en la base de datos. La base de datos a la que está conectado el autor de la llamada `sys.databases`siempre se puede ver en.  
  
> [!IMPORTANT]  
> De forma predeterminada, el rol Public tiene `VIEW ANY DATABASE` el permiso, lo que permite que todos los inicios de sesión vean información de base de datos. Bloquear un inicio de sesión de la capacidad de detectar una base `REVOKE` de `VIEW ANY DATABASE` datos, `public`el permiso `DENY` de `VIEW ANY DATABASE` o el permiso para inicios de sesión individuales.  
  
## <a name="azure-sql-database-remarks"></a>Azure SQL Database comentarios

En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] esta vista está disponible en la `master` base de datos y en las bases de datos de usuario. En la `master` base de datos, esta vista devuelve la información `master` de la base de datos y todas las bases de datos de usuario del servidor. En una base de datos de usuario, esta vista solo devuelve información sobre la base de datos actual y la base de datos maestra.  
  
 Utilice la vista `sys.databases` de la base de datos `master` del servidor [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] donde ser va a crear la nueva base de datos. Una vez iniciada la copia de la base de `sys.databases` datos, `sys.dm_database_copies` puede consultar las `master` vistas y desde la base de datos del servidor de destino para recuperar más información sobre el progreso de la copia.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-query-the-sysdatabases-view"></a>A. Consultar la vista sys.databases

En el ejemplo siguiente se devuelven algunas de las columnas `sys.databases` disponibles en la vista.  
  
```sql  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-sssds"></a>B. Comprobar el estado de copia en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

En el ejemplo siguiente se `sys.databases` consultan las vistas y `sys.dm_database_copies` para devolver información sobre una operación de copia de base de datos.  
  
**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```

### <a name="c-check-the-temporal-retention-policy-status-in-sssds"></a>C. Compruebe el estado de la Directiva de retención temporal en[!INCLUDE[ssSDS](../../includes/sssds-md.md)]

En el ejemplo siguiente se `sys.databases` consulta para que devuelva información si está habilitada la tarea de limpieza de retención temporal. Tenga en cuenta que después de la operación de restauración, la retención temporal está deshabilitada de forma predeterminada. Use `ALTER DATABASE` para habilitarlo explícitamente.
  
**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="next-steps"></a>Pasos siguientes

- [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)
- [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [Sys. database_recovery_status &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)
- [Vistas de catálogo de archivos y bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)
- [sys.dm_database_copies &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
