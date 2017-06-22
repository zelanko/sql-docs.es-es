---
title: "Objeto SQL Server, Características en desuso | Microsoft Docs"
ms.custom: 
ms.date: 05/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:Deprecated Features
- performance counters [SQL Server], deprecated features
- deprecation [SQL Server], performance counters
- Deprecated Features object
ms.assetid: e95de9d6-c950-41cd-8aaa-be529c6de198
caps.latest.revision: 61
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1cbdf2dde41142d1b674e71df3a34756e8fcce99
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-deprecated-features-object"></a>Objeto SQL Server, Características en desuso
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  El objeto SQLServer:Características desusadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un contador para supervisar las características designadas como desusadas. En cada caso, el contador proporciona un recuento de la utilización que muestra el número de veces que la característica desusada se encontró desde que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez.  
  
 El valor de estos contadores también está disponible si se ejecuta la siguiente instrucción:  
  
```  
SELECT * FROM sys.dm_os_performance_counters   
WHERE object_name = 'SQLServer:Deprecated Features';  
```  

En la tabla siguiente se describe el objeto de rendimiento **Características desusadas** de SQL Server.

|**Contador SQL Server, Características en desuso**|Description|  
|-------------|-----------------|  
|**Uso**|Uso de la característica desde que la última vez que se inició SQL Server.|
  
 En la tabla siguiente se describen las instancias del contador Características desusadas de SQL Server.  
  
|Instancias del contador Características desusadas de SQL Server|Description|  
|------------------------------------------------------|-----------------|  
|'#' y '##' como el nombre de tablas temporales y procedimientos almacenados|Se encontró un identificador que no contenía ningún carácter a parte de #. Utilice al menos un carácter adicional. Se produce una vez por cada compilación.|  
|'::' function calling syntax|Se encontró la sintaxis de llamada a función :: para una función con valores de tabla. Reemplace por `SELECT column_list FROM` *< nombre_función>*`()`. Por ejemplo, reemplace `SELECT * FROM ::fn_virtualfilestats(2,1)` con `SELECT * FROM sys.fn_virtualfilestats(2,1)`. Se produce una vez por cada compilación.|  
|'@' y nombres que comiencen por '@@' como identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]|Se encontró un identificador que comenzaba por @ o @@. No utilice @ o @@, o nombres que comiencen por @@ como identificadores. Se produce una vez por cada compilación.|  
|ADDING TAPE DEVICE|Se encontró la característica en desuso sp_addumpdevice'**tape**'. Use sp_addumpdevice'**disk**' en su lugar. Se produce una vez en cada uso.|  
|ALL Permission|Número total de veces que se encontró la sintaxis GRANT ALL, DENY ALL o REVOKE ALL. Modifique la sintaxis para denegar permisos concretos. Se produce una vez por cada consulta.|  
|ALTER DATABASE WITH TORN_PAGE_DETECTION|Número total de veces que la opción TORN_PAGE_DETECTION de ALTER DATABASE, una característica obsoleta, se ha usado desde que se inició la instancia del servidor. Utilice la sintaxis PAGE_VERIFY en su lugar. Se produce una vez por cada uso en una instrucción DDL.|  
|ALTER LOGIN WITH SET CREDENTIAL|Se encontró la sintaxis de la característica obsoleta ALTER LOGIN WITH SET CREDENTIAL o ALTER LOGIN WITH NO CREDENTIAL. Utilice en su lugar la sintaxis ADD o DROP CREDENTIAL. Se produce una vez por cada compilación.|  
|Azeri_Cyrilllic_90|El evento se produce una vez por cada inicio de base de datos y una vez por cada uso de la intercalación. Prevea modificar las aplicaciones que usen esta intercalación.|  
|Azeri_Latin_90|El evento se produce una vez por cada inicio de base de datos y una vez por cada uso de la intercalación. Prevea modificar las aplicaciones que usen esta intercalación.|  
|BACKUP DATABASE or LOG TO TAPE|Se encontró la característica en desuso BACKUP { DATABASE &#124; LOG } TO TAPE o BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape*.<br /><br /> Use BACKUP { DATABASE &#124; LOG } TO DISK o BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk* en su lugar. Se produce una vez en cada uso.|  
|BACKUP DATABASE or LOG WITH MEDIAPASSWORD|Se encontró la característica obsoleta BACKUP DATABASE WITH MEDIAPASSWORD o BACKUP LOG WITH MEDIAPASSWORD. No utilice WITH MEDIAPASSWORD.|  
|BACKUP DATABASE o LOG WITH PASSWORD|Se encontró la característica obsoleta BACKUP DATABASE WITH PASSWORD o BACKUP LOG WITH PASSWORD. No utilice una contraseña WITH PASSWORD.|  
|COMPUTE [BY]|Se encontró la sintaxis de COMPUTE o COMPUTE BY. Vuelva a escribir la consulta para utilizar GROUP BY con ROLLUP. Se produce una vez por cada compilación.|  
|CREATE FULLTEXT CATLOG IN PATH|Se encontró una instrucción CREATE FULLTEXT CATLOG con la cláusula IN PATH. Esta cláusula no tiene ningún efecto en esta versión de SQL Server. Se produce una vez en cada uso.|  
|CREATE TRIGGER WITH APPEND|Se encontró una instrucción CREATE TRIGGER con la cláusula WITH APPEND. Vuelva a crear el desencadenador entero en su lugar. Se produce una vez por cada uso en una instrucción DDL.|  
|CREATE_DROP_DEFAULT|Se encontró la sintaxis CREATE DEFAULT o DROP DEFAULT. Vuelva a escribir el comando utilizando la opción DEFAULT de CREATE TABLE o ALTER TABLE. Se produce una vez por cada compilación.|  
|CREATE_DROP_RULE|Se encontró la sintaxis CREATE RULE. Reescriba el comando utilizando las restricciones. Se produce una vez por cada compilación.|  
|Data types: text ntext or image|Se encontraron los tipos de datos **text**, **ntext**o **image** . Reescriba las aplicaciones para usar el tipo de datos **varchar(max)** y quite la sintaxis de los tipos de datos **text**, **ntext**y **image** . Se produce una vez por cada consulta.|  
||Número total de veces que una base de datos se cambió al nivel de compatibilidad 80. Planee actualizar la base de datos y la aplicación antes de la versión siguiente. También se produce cuando se inicia una base de datos en el nivel de compatibilidad 80.|  
|Niveles de compatibilidad de la base de datos 100, 110. 120|Número total de veces que el nivel de compatibilidad de una base de datos ha cambiado. Planee actualizar la base de datos y la aplicación en una versión futura. También se produce cuando se inicia una base de datos situada en un nivel de compatibilidad en desuso.|  
|DATABASE_MIRRORING|Se encontraron referencias a la característica de creación de reflejo de la base de datos. Planee la actualización a Grupos de disponibilidad AlwaysOn, o si ejecuta una edición de SQL Server que no admite Grupos de disponibilidad AlwaysOn, planee la migración al trasvase de registros.|  
|database_principal_aliases|Se encontraron referencias a sys.database_principal_aliases desusados. Utilice roles en lugar de alias. Se produce una vez por cada compilación.|  
|DATABASEPROPERTY|Una instrucción hizo referencia a DATABASEPROPERTY. Actualice la instrucción DATABASEPROPERTY con DATABASEPROPERTYEX. Se produce una vez por cada compilación.|  
|DATABASEPROPERTYEX('IsFullTextEnabled')|Una instrucción hizo referencia a la propiedad DATABASEPROPERTYEX IsFullTextEnabled. El valor de esta propiedad no tiene ningún efecto. En las bases de datos de usuario siempre está habilitada la búsqueda de texto completo. No utilice esta propiedad. Se produce una vez por cada compilación.|  
|DBCC [UN]PINTABLE|Se encontró la instrucción DBCC UNPINTABLE o DBCC PINTABLE. Esta instrucción no tiene ningún efecto y se debería quitar. Se produce una vez por cada consulta.|  
|DBCC DBREINDEX|Se encontró la instrucción DBCC DBREINDEX. Reescriba la instrucción para utilizar la opción REBUILD de ALTER INDEX. Se produce una vez por cada consulta.|  
|DBCC INDEXDEFRAG|Se encontró la instrucción DBCC INDEXDEFRAG. Reescriba la instrucción para utilizar la opción REORGANIZE de ALTER INDEX. Se produce una vez por cada consulta.|  
|DBCC SHOWCONTIG|Se encontró la instrucción DBCC SHOWCONTIG. Consulte esta información en sys.dm_db_index_physical_stats. Se produce una vez por cada consulta.|  
|Palabra clave DEFAULT como valor predeterminado|Se encontró una sintaxis que utiliza la palabra clave DEFAULT como valor predeterminado. No debe usarse. Se produce una vez por cada compilación.|  
|Algoritmo de cifrado desusado|El algoritmo de cifrado RC4 desusado se quitará en la próxima versión de SQL Server. Evite usar esta característica en los nuevos trabajos de desarrollo y piense en modificar las aplicaciones que la usan actualmente. El algoritmo RC4 no es seguro y se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.|  
|Algoritmo hash en desuso|Use los algoritmos MD2, MD4, MD5, SHA, o SHA1.|  
|Algoritmo DESX|Se encontró sintaxis que utiliza el algoritmo de cifrado DESX. Utilice otro algoritmo de cifrado. Se produce una vez por cada compilación.|  
|dm_fts_active_catalogs|El contador dm_fts_active_catalogs siempre es 0 porque algunas columnas de la vista sys.dm_fts_active_catalogs no están desusadas. Para supervisar una columna desusada, use el contador específico de la columna; por ejemplo, dm_fts_active_catalogs.is_paused.|  
|dm_fts_active_catalogs.is_paused|Se encontró la columna is_paused de la vista de administración dinámica [sys.dm_fts_active_catalogs](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md) . Procure no utilizar esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|dm_fts_active_catalogs.previous_status|Se encontró la columna previous_status de la vista de administración dinámica sys.dm_fts_active_catalogs. Procure no utilizar esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|dm_fts_active_catalogs.previous_status_description|Se encontró la columna previous_status_description de la vista de administración dinámica sys.dm_fts_active_catalogs. Procure no utilizar esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|dm_fts_active_catalogs.row_count_in_thousands|Se encontró la columna row_count_in_thousands de la vista de administración dinámica sys.dm_fts_active_catalogs. Procure no utilizar esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|dm_fts_active_catalogs.status|Se encontró la columna de estado de la vista de administración dinámica sys.dm_fts_active_catalogs. Procure no utilizar esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|dm_fts_active_catalogs.status_description|Se encontró la columna status_description de la vista de administración dinámica sys.dm_fts_active_catalogs. Procure no utilizar esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|dm_fts_active_catalogs.worker_count|Se encontró la columna worker_count de la vista de administración dinámica sys.dm_fts_active_catalogs. Procure no utilizar esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|dm_fts_memory_buffers|El contador dm_fts_memory_buffers siempre es 0 porque la mayoría de las columnas de la vista sys.dm_fts_memory_buffers no están desusadas. Para supervisar la columna desusada, utilice el contador específico de la columna: dm_fts_memory_buffers.row_count.|  
|dm_fts_memory_buffers.row_count|Se encontró la columna row_count de la vista de administración dinámica [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md) . Procure no utilizar esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|DROP INDEX con nombre de dos partes|La sintaxis de DROP INDEX contenía el formato de la sintaxis *table_name.index_name* en DROP INDEX. Reemplace por la sintaxis *index_name* ON *table_name* en la instrucción DROP INDEX. Se produce una vez por cada compilación.|  
|EXT_CREATE_ALTER_SOAP_ENDPOINT|Se encontró la instrucción CREATE o ALTER ENDPOINT con la opción FOR SOAP. Servicios web XML nativos están desusados. Utilice Windows Communications Foundation (WCF) o ASP.NET en su lugar.|  
|EXT_endpoint_webmethods|Se encontró sys.endpoint_webmethods. Servicios web XML nativos están desusados. Utilice Windows Communications Foundation (WCF) o ASP.NET en su lugar.|  
|EXT_soap_endpoints|Se encontró sys.soap_endpoints. Servicios web XML nativos están desusados. Utilice Windows Communications Foundation (WCF) o ASP.NET en su lugar.|  
|EXTPROP_LEVEL0TYPE|TYPE se encontró en un level0type. Use SCHEMA como level0type y TYPE como level1type. Se produce una vez por cada consulta.|  
|EXTPROP_LEVEL0USER|Un level0typeUSER cuando también se especificó level1type. Utilice únicamente USER como level0type para las propiedades extendidas en un usuario. Se produce una vez por cada consulta.|  
|FASTFIRSTROW|Se encontró la sintaxis FASTFIRSTROW. Reescriba las instrucciones para usar la sintaxis (FAST *n*). Se produce una vez por cada compilación.|  
|FILE_ID|Se encontró la sintaxis de FILE_ID. Reescriba las instrucciones para utilizar FILE_IDEX. Se produce una vez por cada compilación.|  
|fn_get_sql|Se compiló la función fn_get_sql. Use sys.dm_exec_sql_text en su lugar. Se produce una vez por cada compilación.|  
|fn_servershareddrives|Se compiló la función fn_servershareddrives. Utilice en su lugar sys.dm_io_cluster_shared_drives. Se produce una vez por cada compilación.|  
|fn_virtualservernodes|Se compiló la función fn_virtualservernodes. Utilice en su lugar sys.dm_os_cluster_nodes. Se produce una vez por cada compilación.|  
|fulltext_catalogs|El contador fulltext_catalogs siempre es 0 porque algunas columnas de la vista sys.fulltext_catalogs no están desusadas. Para supervisar una columna desusada, use su contador específico de la columna; por ejemplo, fulltext_catalogs.data_space_id. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|fulltext_catalogs.data_space_id|Se encontró la columna data_space_id de la vista de catálogo [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) . No utilice esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|fulltext_catalogs.file_id|Se encontró la columna file_id de la vista de catálogo sys.fulltext_catalogs. No utilice esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|fulltext_catalogs.path|Se encontró la columna path de la vista de catálogo sys.fulltext_catalogs. No utilice esta columna. Se produce cada vez que la instancia del servidor detecta una referencia a la columna.|  
|FULLTEXTCATALOGPROPERTY('LogSize')|Se encontró la propiedad LogSize de la función FULLTEXTCATALOGPROPERTY. Procure no utilizar esta propiedad.|  
|FULLTEXTCATALOGPROPERTY('PopulateStatus')|Se encontró la propiedad PopulateStatus de la función FULLTEXTCATALOGPROPERTY. Procure no utilizar esta propiedad.|  
|FULLTEXTSERVICEPROPERTY('ConnectTimeout')|Se encontró la propiedad ConnectTimeout de la función FULLTEXTSERVICEPROPERTY. Procure no utilizar esta propiedad.|  
|FULLTEXTSERVICEPROPERTY('DataTimeout')|Se encontró la propiedad DataTimeout de la función FULLTEXTSERVICEPROPERTY. Procure no utilizar esta propiedad.|  
|FULLTEXTSERVICEPROPERTY('ResourceUsage')|Se encontró la propiedad ResourceUsage de la función FULLTEXTSERVICEPROPERTY. Procure no utilizar esta propiedad.|  
|GROUP BY ALL|Número total de veces que se encontró la sintaxis de GROUP BY ALL. Modifique la sintaxis para agrupar por tablas concretas.|  
|Hindi|El evento se produce una vez por cada inicio de base de datos y una vez por cada uso de la intercalación. Prevea modificar las aplicaciones que usen esta intercalación. Utilice en su lugar Indic_General_90.|  
|Sugerencia de la tabla HOLDLOCK sin paréntesis||  
|IDENTITYCOL|Se encontró la sintaxis INDENTITYCOL. Rescriba las instrucciones para utilizar la sintaxis de $identity. Se produce una vez por cada compilación.|  
|Lista de selección de índice de la vista sin COUNT_BIG(*)|La lista de selección de una vista indizada de agregado debe contener COUNT_BIG (*).|  
|INDEX_OPTION|Se encontró la sintaxis de CREATE TABLE, ALTER TABLE o CREATE INDEX sin paréntesis alrededor de las opciones. Reescriba la instrucción para utilizar la sintaxis actual. Se produce una vez por cada consulta.|  
|INDEXKEY_PROPERTY|Se encontró la sintaxis de INDEXKEY_PROPERTY. Rescriba las instrucciones para consultar sys.index_columns. Se produce una vez por cada compilación.|  
|Sugerencias TVF indirectas|La aplicación indirecta, a través de una vista, de sugerencias de tabla a una invocación de una función con valores de tabla de múltiples instrucciones se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|INSERT NULL en columnas TIMESTAMP|Se insertó un valor NULL en una columna TIMESTAMP. Utilice en su lugar un valor predeterminado. Se produce una vez por cada compilación.|  
|INSERT_HINTS||  
|Korean_Wansung_Unicode|El evento se produce una vez por cada inicio de base de datos y una vez por cada uso de la intercalación. Prevea modificar las aplicaciones que usen esta intercalación.|  
|Lithuanian_Classic|El evento se produce una vez por cada inicio de base de datos y una vez por cada uso de la intercalación. Prevea modificar las aplicaciones que usen esta intercalación.|  
|Macedonian|El evento se produce una vez por cada inicio de base de datos y una vez por cada uso de la intercalación. Prevea modificar las aplicaciones que usen esta intercalación. Use en su lugar Macedonian_FYROM_90.|  
|MODIFY FILEGROUP READONLY|Se encontró la sintaxis de MODIFY FILEGROUP READONLY. Reescriba las instrucciones para utilizar la sintaxis de READ_ONLY. Se produce una vez por cada compilación.|  
|MODIFY FILEGROUP READWRITE|Se encontró la sintaxis de MODIFY FILEGROUP READWRITE. Rescriba las instrucciones para utilizar la sintaxis de READ_WRITE. Se produce una vez por cada compilación.|  
|Nombre de columna de varias partes|Una consulta utilizó un nombre de 3 ó 4 partes en la lista de columnas. Cambie la consulta para que use nombres de 2 partes que cumplen el estándar. Se produce una vez por cada compilación.|  
|Varias sugerencias de tabla sin coma|Se utilizó un espacio como separador entre las sugerencias de la tabla. Utilice en su lugar una coma. Se produce una vez por cada compilación.|  
|NOLOCK or READUNCOMMITTED in UPDATE or DELETE|Se encontró NOLOCK o READUNCOMMITTED en la cláusula FROM de una instrucción UPDATE o DELETE. Quite las sugerencias de tabla NOLOCK o READUNCOMMITTED de la cláusula FROM.|  
|Operadores de combinación externa no ANSI *= o =\*|Se encontró una instrucción que usa la sintaxis de combinación *= o =\* . Reescriba la instrucción para que use la sintaxis de unión de ANSI. Se produce una vez por cada compilación.|  
|numbered_stored_procedures||  
|numbered_procedure_parameters|Hace referencia que se encontraron sys.numbered_procedure_parameters desusados. No debe usarse. Se produce una vez por cada compilación.|  
|numbered_procedures|Hace referencia a que se encontraron sys.numbered_procedures desusados. No debe usarse. Se produce una vez por cada compilación.|  
|Oldstyle RAISEERROR|Se encontró la sintaxis de RAISERROR obsoleta (Formato: RAISERROR integer string). Reescriba la instrucción usando la sintaxis de RAISERROR actual. Se produce una vez por cada compilación.|  
|OLEDB para conexiones ad hoc|SQLOLEDB no es un proveedor admitido. Utilice [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para las conexiones ad hoc.|  
|PERMISSIONS|Se encontraron referencias a la función intrínseca PERMISSIONS. Consulte en su lugar sys.fn_my_permissions. Se produce una vez por cada consulta.|  
|ProcNums|Se encontró la sintaxis de ProcNums desusada. Reescriba las instrucciones para quitar las referencias. Se produce una vez por cada compilación.|  
|READTEXT|Se encontró la sintaxis de READTEXT. Reescriba las aplicaciones para usar el tipo de datos **varchar(max)** y quite la sintaxis del tipo de datos **text** . Se produce una vez por cada consulta.|  
|RESTORE DATABASE o LOG WITH DBO_ONLY|Se encontró la sintaxis RESTORE … WITH DBO_ONLY. En su lugar, use RESTORE … RESTRICTED_USER.|  
|RESTORE DATABASE or LOG WITH MEDIAPASSWORD|Se encontró la sintaxis RESTORE … WITH MEDIAPASSWORD. WITH MEDIAPASSWORD proporciona poca seguridad y se debería quitar.|  
|RESTORE DATABASE or LOG WITH PASSWORD|Se encontró la sintaxis RESTORE … WITH PASSWORD. WITH PASSWORD proporciona poca seguridad y se debería quitar.|  
|Devolver resultados del desencadenador|Este evento se produce una vez por cada invocación del desencadenador. Reescriba el desencadenador para que no devuelva conjuntos de resultados.|  
|ROWGUIDCOL|Se encontró la sintaxis de ROWGUIDCOL. Reescriba las instrucciones para que usen la sintaxis de $rowguid. Se produce una vez por cada compilación.|  
|SET ANSI_NULLS OFF|Se encontró la sintaxis de SET ANSI_NULLS OFF. Quite esta sintaxis desusada. Se produce una vez por cada compilación.|  
|SET ANSI_PADDING OFF|Se encontró la sintaxis de SET ANSI_PADDING OFF. Quite esta sintaxis desusada. Se produce una vez por cada compilación.|  
|SET CONCAT_NULL_YIELDS_NULL OFF|Se encontró la sintaxis de SET CONCAT_NULL_YIELDS_NULL OFF. Quite esta sintaxis desusada. Se produce una vez por cada compilación.|  
|SET DISABLE_DEF_CNST_CHK|Se encontró la sintaxis de SET DISABLE_DEF_CNST_CHK. No tiene ningún efecto. Quite esta sintaxis desusada. Se produce una vez por cada compilación.|  
|SET FMTONLY ON|Se encontró la sintaxis de SET FMTONLY. Quite esta sintaxis desusada. Se produce una vez por cada compilación.|  
|SET OFFSETS|Se encontró la sintaxis de SET OFFSETS. Quite esta sintaxis desusada. Se produce una vez por cada compilación.|  
|SET REMOTE_PROC_TRANSACTIONS|Se encontró la sintaxis de SET REMOTE_PROC_TRANSACTIONS. Quite esta sintaxis desusada. Utilice en su lugar linked servers y sp_serveroption.|  
|SET ROWCOUNT|Se encontró la sintaxis de SET ROWCOUNT en una instrucción DELETE, INSERT o UPDATE. Reescriba la instrucción utilizando TOP. Se produce una vez por cada compilación.|  
|SETUSER|Se encontró la instrucción SET USER. Utilice la cláusula EXECUTE AS en su lugar. Se produce una vez por cada consulta.|  
|sp_addapprole|Se encontró el procedimiento sp_addapprole. En su lugar, use CREATE APPLICATION ROLE. Se produce una vez por cada consulta.|  
|sp_addextendedproc|Se encontró el procedimiento sp_addextendedproc. Utilice CLR en su lugar. Se produce una vez por cada compilación.|  
|sp_addlogin|Se encontró el procedimiento sp_addlogin. Utilice CREATE LOGIN en su lugar. Se produce una vez por cada consulta.|  
|sp_addremotelogin|Se encontró el procedimiento sp_addremotelogin. Use en su lugar servidores vinculados.|  
|sp_addrole|Se encontró el procedimiento sp_addrole. Utilice CREATE ROLE en su lugar. Se produce una vez por cada consulta.|  
|sp_addserver|Se encontró el procedimiento sp_addserver. Use en su lugar servidores vinculados.|  
|sp_addtype|Se encontró el procedimiento sp_addtype. En su lugar, utilice CREATE TYPE. Se produce una vez por cada compilación.|  
|sp_adduser|Se encontró el procedimiento sp_adduser. En su lugar, use CREATE USER. Se produce una vez por cada consulta.|  
|sp_approlepassword|Se encontró el procedimiento sp_approlepassword. En su lugar, use ALTER APPLICATION ROLE. Se produce una vez por cada consulta.|  
|sp_attach_db|Se encontró el procedimiento sp_attach_db. Utilice en su lugar CREATE DATABASE FOR ATTACH. Se produce una vez por cada consulta.|  
|sp_attach_single_file_db|Se encontró el procedimiento sp_single_file_db. Utilice en su lugar CREATE DATABASE FOR ATTACH_REBUILD_LOG. Se produce una vez por cada consulta.|  
|sp_bindefault|Se encontró el procedimiento sp_bindefault. Use la palabra clave DEFAULT de ALTER TABLE o CREATE TABLE en su lugar. Se produce una vez por cada compilación.|  
|sp_bindrule|Se encontró el procedimiento sp_bindrule. En su lugar, utilice restricciones CHECK. Se produce una vez por cada compilación.|  
|sp_bindsession|Se encontró el procedimiento sp_bindesession. En su lugar, utilice conjuntos de resultados activos múltiples (MARS) o transacciones distribuidas. Se produce una vez por cada compilación.|  
|sp_certify_removable|Se encontró el procedimiento sp_certify_removable. Utilice en su lugar sp_detach_db. Se produce una vez por cada consulta.|  
|sp_changeobjectowner|Se encontró el procedimiento sp_changeobjectowner. Use ALTER SCHEMA o ALTER AUTHORIZATION en su lugar. Se produce una vez por cada consulta.|  
|sp_change_users_login|Se encontró el procedimiento sp_change_users_login. Utilice en su lugar ALTER USER. Se produce una vez por cada consulta.|  
|sp_configure 'allow updates'|Se encontró la opción allow updates de sp_configure. Las tablas del sistema ya no son actualizables. No debe usarse. Se produce una vez por cada consulta.|  
|sp_configure 'disallow results from triggers'|Se encontró la opción disallow result sets from triggers de sp_configure. Para denegar los conjuntos de resultados de los desencadenadores, utilice sp_configure para establecer la opción en 1. Se produce una vez por cada consulta.|  
|sp_configure 'ft crawl bandwidth (max)'|Se encontró la opción ft crawl bandwidth (max) de sp_configure. No debe usarse. Se produce una vez por cada consulta.|  
|sp_configure 'ft crawl bandwidth (min)'|Se encontró la opción ft crawl bandwidth (min) de sp_configure. No debe usarse. Se produce una vez por cada consulta.|  
|sp_configure 'ft notify bandwidth (max)'|Se encontró la opción ft notify bandwidth (max) de sp_configure. No debe usarse. Se produce una vez por cada consulta.|  
|sp_configure 'ft notify bandwidth (min)'|Se encontró la opción ft notify bandwidth (min) de sp_configure. No debe usarse. Se produce una vez por cada consulta.|  
|sp_configure 'locks'|Se encontró la opción locks de sp_configure. Los bloqueos ya no son configurables. No debe usarse. Se produce una vez por cada consulta.|  
|sp_configure 'open objects'|Se encontró la opción open objects de sp_configure. El número de objetos abiertos ya no es configurable. No debe usarse. Se produce una vez por cada consulta.|  
|sp_configure 'priority boost'|Se encontró la opción Aumento de prioridad de sp_configure. No debe usarse. Se produce una vez por cada consulta. Use en su lugar la opción start/high … program.exe de Windows.|  
|sp_configure 'remote proc trans'|Se encontró la opción remote proc trans de sp_configure. No debe usarse. Se produce una vez por cada consulta.|  
|sp_configure 'set working set size'|Se encontró la opción set working set size de sp_configure. El tamaño del espacio de trabajo ya no es configurable. No debe usarse. Se produce una vez por cada consulta.|  
|sp_control_dbmasterkey_password|El procedimiento almacenado sp_control_dbmasterkey_password no comprueba si existe una clave maestra. Esto se admite por cuestiones de compatibilidad con versiones anteriores, pero muestra una advertencia. Este comportamiento se ha desaprobado. En una futura versión, la clave maestra debe existir y la contraseña utilizada en el procedimiento almacenado sp_control_dbmasterkey_password debe coincidir con una de las utilizadas para cifrar la clave maestra de base de datos.|  
|sp_create_removable|Se encontró el procedimiento sp_create_removable. Utilice CREATE DATABASE en su lugar. Se produce una vez por cada consulta.|  
|sp_db_vardecimal_storage_format|Se encontró que se usa el de formato de almacenamiento **vardecimal** . En su lugar, use la compresión de datos.|  
|sp_dbcmptlevel|Se encontró el procedimiento sp_dbcmptlevel. En su lugar, use ALTER DATABASE … SET COMPATIBILITY_LEVEL. Se produce una vez por cada consulta.|  
|sp_dbfixedrolepermission|Se encontró el procedimiento sp_dbfixedrolepermission. No debe usarse. Se produce una vez por cada consulta.|  
|sp_dboption|Se encontró el procedimiento sp_dboption. Use ALTER DATABASE y DATABASEPROPERTYEX en su lugar. Se produce una vez por cada compilación.|  
|sp_dbremove|Se encontró el procedimiento sp_dbremove. Use DROP DATABASE en su lugar. Se produce una vez por cada consulta.|  
|sp_defaultdb|Se encontró el procedimiento sp_defaultdb. En su lugar, use ALTER LOGIN. Se produce una vez por cada compilación.|  
|sp_defaultlanguage|Se encontró el procedimiento sp_defaultlanguage. En su lugar, use ALTER LOGIN. Se produce una vez por cada compilación.|  
|sp_denylogin|Se encontró el procedimiento sp_denylogin. Use ALTER LOGIN DISABLE en su lugar. Se produce una vez por cada consulta.|  
|sp_depends|Se encontró el procedimiento sp_depends. Use sys.dm_sql_referencing_entities y sys.dm_sql_referenced_entities en su lugar. Se produce una vez por cada consulta.|  
|sp_detach_db @keepfulltextindexfile|Se encontró el argumento @keepfulltextindexfile en una instrucción sp_detach_db. No utilice este argumento.|  
|sp_dropalias|Se encontró el procedimiento sp_dropalias. Reemplace los alias por una combinación de cuentas de usuario y roles de la base de datos. Use sp_dropalias para quitar los alias de las bases de datos actualizadas. Se produce una vez por cada compilación.|  
|sp_dropapprole|Se encontró el procedimiento sp_dropapprole. Utilice DROP APPLICATION ROLE en su lugar. Se produce una vez por cada consulta.|  
|sp_dropextendedproc|Se encontró el procedimiento sp_dropextendedproc. Utilice CLR en su lugar. Se produce una vez por cada compilación.|  
|sp_droplogin|Se encontró el procedimiento sp_droplogin. En su lugar, use DROP LOGIN. Se produce una vez por cada consulta.|  
|sp_dropremotelogin|Se encontró el procedimiento sp_dropremotelogin. Use en su lugar servidores vinculados.|  
|sp_droprole|Se encontró el procedimiento sp_droprole. Utilice DROP ROLE en su lugar. Se produce una vez por cada consulta.|  
|sp_droptype|Se encontró el procedimiento sp_droptype. Utilice DROP TYPE en su lugar.|  
|sp_dropuser|Se encontró el procedimiento sp_dropuser. Utilice DROP USER en su lugar. Se produce una vez por cada consulta.|  
|sp_estimated_rowsize_reduction_for_vardecimal|Se encontró que se usa el de formato de almacenamiento **vardecimal** . Utilice en su lugar la compresión de datos y sp_estimate_data_compression_savings.|  
|sp_fulltext_catalog|Se encontró el procedimiento sp_fulltext_catalog. Use CREATE/ALTER/DROP FULLTEXT CATALOG en su lugar. Se produce una vez por cada compilación.|  
|sp_fulltext_column|Se encontró el procedimiento sp_fulltext_column. Utilice ALTER FULLTEXT INDEX en su lugar. Se produce una vez por cada compilación.|  
|sp_fulltext_database|Se encontró el procedimiento sp_fulltext_database. Use ALTER DATABASE en su lugar. Se produce una vez por cada compilación.|  
|sp_fulltext_service @action=clean_up|Se encontró la opción clean_up del procedimiento sp_fulltext_service. Se produce una vez por cada consulta.|  
|sp_fulltext_service @action=connect_timeout|Se encontró la opción connect_timeout del procedimiento sp_fulltext_service. Se produce una vez por cada consulta.|  
|sp_fulltext_service @action=data_timeout|Se encontró la opción data_timeout del procedimiento sp_fulltext_service. Se produce una vez por cada consulta.|  
|sp_fulltext_service @action=resource_usage|Se encontró la opción resource_usage del procedimiento sp_fulltext_service. Esta opción no tiene ninguna función. Se produce una vez por cada consulta.|  
|sp_fulltext_table|Se encontró el procedimiento sp_fulltext_table. Use CREATE/ALTER/DROP FULLTEXT INDEX en su lugar. Se produce una vez por cada compilación.|  
|sp_getbindtoken|Se encontró el procedimiento sp_getbindtoken. En su lugar, utilice conjuntos de resultados activos múltiples (MARS) o transacciones distribuidas. Se produce una vez por cada compilación.|  
|sp_grantdbaccess|Se encontró el procedimiento sp_grantdbaccess. En su lugar, use CREATE USER. Se produce una vez por cada consulta.|  
|sp_grantlogin|Se encontró el procedimiento sp_grantlogin. Utilice CREATE LOGIN en su lugar. Se produce una vez por cada consulta.|  
|sp_help_fulltext_catalog_components|Se encontró el procedimiento sp_help_fulltext_catalog_components. Este procedimiento devuelve las filas vacías. No utilice este procedimiento. Se produce una vez por cada compilación.|  
|sp_help_fulltext_catalogs|Se encontró el procedimiento sp_help_fulltext_catalogs. Consulte en su lugar sys.fulltext_catalogs. Se produce una vez por cada compilación.|  
|sp_help_fulltext_catalogs_cursor|Se encontró el procedimiento sp_help_fulltext_catalogs_cursor. Consulte en su lugar sys.fulltext_catalogs. Se produce una vez por cada compilación.|  
|sp_help_fulltext_columns|Se encontró el procedimiento sp_help_fulltext_columns. Consulte en su lugar sys.fulltext_index_columns. Se produce una vez por cada compilación.|  
|sp_help_fulltext_columns_cursor|Se encontró el procedimiento sp_help_fulltext_columns_cursor. Consulte en su lugar sys.fulltext_index_columns. Se produce una vez por cada compilación.|  
|sp_help_fulltext_tables|Se encontró el procedimiento sp_help_fulltext_tables. Consulte en su lugar sys.fulltext_indexes. Se produce una vez por cada compilación.|  
|sp_help_fulltext_tables_cursor|Se encontró el procedimiento sp_help_fulltext_tables_cursor. Consulte en su lugar sys.fulltext_indexes. Se produce una vez por cada compilación.|  
|sp_helpdevice|Se encontró el procedimiento sp_helpdevice. Consulte en su lugar sys.backup_devices. Se produce una vez por cada consulta.|  
|sp_helpextendedproc|Se encontró el procedimiento sp_helpextendedproc. Utilice CLR en su lugar. Se produce una vez por cada compilación.|  
|sp_helpremotelogin|Se encontró el procedimiento sp_helpremotelogin. Use en su lugar servidores vinculados.|  
|sp_indexoption|Se encontró el procedimiento sp_indexoption. Utilice ALTER INDEX en su lugar. Se produce una vez por cada compilación.|  
|sp_lock|Se encontró el procedimiento sp_lock. Consulte en su lugar sys.dm_tran_locks. Se produce una vez por cada consulta.|  
|sp_password|Se encontró el procedimiento sp_password. En su lugar, use ALTER LOGIN. Se produce una vez por cada consulta.|  
|sp_remoteoption|Se encontró el procedimiento sp_remoteoption. Use en su lugar servidores vinculados.|  
|sp_renamedb|Se encontró el procedimiento sp_renamedb. Use ALTER DATABASE en su lugar. Se produce una vez por cada consulta.|  
|sp_resetstatus|Se encontró el procedimiento sp_resetstatus. Use ALTER DATABASE en su lugar. Se produce una vez por cada consulta.|  
|sp_revokedbaccess|Se encontró el procedimiento sp_revokedbaccess. Utilice DROP USER en su lugar. Se produce una vez por cada consulta.|  
|sp_revokelogin|Se encontró el procedimiento sp_revokelogin. En su lugar, use DROP LOGIN. Se produce una vez por cada consulta.|  
|sp_srvrolepermission|Se encontró el procedimiento sp_srvrolepermission desusado. No debe usarse. Se produce una vez por cada consulta.|  
|sp_unbindefault|Se encontró el procedimiento sp_unbindefault. Utilice en su lugar la palabra clave DEFAULT en las instrucciones CREATE TABLE o ALTER TABLE. Se produce una vez por cada compilación.|  
|sp_unbindrule|Se encontró el procedimiento sp_unbindrule. Use restricciones CHECK en lugar de reglas. Se produce una vez por cada compilación.|  
|SQL_AltDiction_CP1253_CS_AS|El evento se produce una vez por cada inicio de base de datos y una vez por cada uso de la intercalación. Prevea modificar las aplicaciones que usen esta intercalación.|  
|Literales de cadena como alias de columna|Se encontró la sintaxis que contiene una cadena que se utiliza como un alias de columna en una instrucción SELECT, como `'string' = expression`. No debe usarse. Se produce una vez por cada compilación.|  
|sys.sql_dependencies|Se encontraron referencias a sys.sql_dependencies. Use sys.sql_expression_dependencies en su lugar. Se produce una vez por cada compilación.|  
|sysaltfiles|Se encontraron referencias a sysaltfiles. Utilice en su lugar sys.master_files. Se produce una vez por cada compilación.|  
|syscacheobjects|Se encontraron referencias a syscacheobjects. Utilice en su lugar sys.dm_exec_cached_plans, sys.dm_exec_plan_attributes y  sys.dm_exec_sql_text. Se produce una vez por cada compilación.|  
|syscolumns|Se encontraron referencias a syscolumns. Utilice en su lugar sys.columns. Se produce una vez por cada compilación.|  
|syscomments|Se encontraron referencias a syscomments. Utilice en su lugar sys.sql_modules. Se produce una vez por cada compilación.|  
|sysconfigures|Se encontraron referencias a la tabla sysconfigures. Haga referencia a la vista sys.sysconfigures en su lugar. Se produce una vez por cada compilación.|  
|sysconstraints|Se encontraron referencias a sysconstraints . Use sys.check_constraints, sys.default_constraints, sys.key_constraints o sys.foreign_keys en su lugar. Se produce una vez por cada compilación.|  
|syscurconfigs|Se encontraron referencias a syscurconfigs. Utilice en su lugar sys.configurations. Se produce una vez por cada compilación.|  
|sysdatabases|Se encontraron referencias a sysdatabases. Utilice en su lugar sys.databases. Se produce una vez por cada compilación.|  
|sysdepends|Se encontraron referencias a sysdepends. Utilice en su lugar sys.sql_dependencies. Se produce una vez por cada compilación.|  
|sysdevices|Se encontraron referencias a sysdevices. Utilice en su lugar sys.backup_devices. Se produce una vez por cada compilación.|  
|sysfilegroups|Se encontraron referencias a sysfilegroups. Utilice en su lugar sys.filegroups. Se produce una vez por cada compilación.|  
|sysfiles|Se encontraron referencias a sysfiles. Use sys.database_files en su lugar. Se produce una vez por cada compilación.|  
|sysforeignkeys|Se encontraron referencias a sysforeignkeys. Utilice en su lugar sys.foreign_keys. Se produce una vez por cada compilación.|  
|sysfulltextcatalogs|Se encontraron referencias a sysfulltextcatalogs. Utilice en su lugar sys.fulltext_catalogs. Se produce una vez por cada compilación.|  
|sysindexes|Se encontraron referencias a sysindexes. Utilice en su lugar sys.indexes, sys.partitions, sys.allocation_unitsy sys.dm_db_partition_stats. Se produce una vez por cada compilación.|  
|sysindexkeys|Se encontraron referencias a sysindexkeys. En su lugar, use sys.index_columns. Se produce una vez por cada compilación.|  
|syslockinfo|Se encontraron referencias a syslockinfo. Use sys.dm_tran_locks en su lugar. Se produce una vez por cada compilación.|  
|syslogins|Se encontraron referencias a syslogins. Utilice en su lugar sys.server_principals y sys.sql_logins. Se produce una vez por cada compilación.|  
|sysmembers|Se encontraron referencias a sysmembers. Utilice en su lugar sys.database_role_members. Se produce una vez por cada compilación.|  
|sysmessages|Se encontraron referencias a sysmessages. Utilice en su lugar sys.messages. Se produce una vez por cada compilación.|  
|sysobjects|Se encontraron referencias a sysobjects. Utilice en su lugar sys.objects. Se produce una vez por cada compilación.|  
|sysoledbusers|Se encontraron referencias a sysoledbusers. Utilice en su lugar sys.linked_logins. Se produce una vez por cada compilación.|  
|sysopentapes|Se encontraron referencias a sysopentapes. Utilice en su lugar sys.dm_io_backup_tapes. Se produce una vez por cada compilación.|  
|sysperfinfo|Se encontraron referencias a sysperfinfo. Use sys.dm_os_performance_counters. en su lugar. Se produce una vez por cada compilación.|  
|syspermissions|Se encontraron referencias a syspermissions. Use sys.database_permissions y sys.server_permissions en su lugar. Se produce una vez por cada compilación.|  
|sysprocesses|Se encontraron referencias a sysprocesses. Utilice en su lugar sys.dm_exec_connections, sys.dm_exec_sessions y sys.dm_exec_requests. Se produce una vez por cada compilación.|  
|sysprotects|Se encontraron referencias a sysprotects. Use sys.database_permissions y sys.server_permissions en su lugar. Se produce una vez por cada compilación.|  
|sysreferences|Se encontraron referencias a sysreferences. Utilice en su lugar sys.foreign_keys. Se produce una vez por cada compilación.|  
|sysremotelogins|Se encontraron referencias a sysremotelogins. Utilice en su lugar sys.remote_logins. Se produce una vez por cada compilación.|  
|sysservers|Se encontraron referencias a sysservers. Utilice en su lugar sys.servers. Se produce una vez por cada compilación.|  
|systypes|Se encontraron referencias a systypes. Utilice en su lugar sys.types. Se produce una vez por cada compilación.|  
|sysusers|Se encontraron referencias a sysusers. Utilice en su lugar sys.database_principals. Se produce una vez por cada compilación.|  
|Sugerencia de table sin WITH|Se encontró una instrucción que utilizaba sugerencias de tabla pero no usaba la palabra clave WITH. Modifique las instrucciones para incluir la palabra WITH. Se produce una vez por cada compilación.|  
|Opción de tabla Text in row|Se encontraron referencias a la opción de tabla 'text in row'. Utilice sp_tableoption 'large value types out of row' en su lugar. Se produce una vez por cada consulta.|  
|TEXTPTR|Se encontraron referencias a la función TEXTPTR. Reescriba las aplicaciones para usar el tipo de datos **varchar(max)** y quite la sintaxis de los tipos de datos **text**, **ntext**y **image** . Se produce una vez por cada consulta.|  
|TEXTVALID|Se encontraron referencias a la función TEXTVALID. Reescriba las aplicaciones para usar el tipo de datos **varchar(max)** y quite la sintaxis de los tipos de datos **text**, **ntext**y **image** . Se produce una vez por cada consulta.|  
|TIMESTAMP|Número total de veces que el tipo de datos **timestamp** obsoleto se encontró en una instrucción DDL. En su lugar, use el tipo de datos **rowversion** .|  
|UPDATETEXT o WRITETEXT|Se encontró la instrucción WRITETEXT o UPDATETEXT. Reescriba las aplicaciones para usar el tipo de datos **varchar(max)** y quite la sintaxis de los tipos de datos **text**, **ntext**y **image** . Se produce una vez por cada consulta.|  
|USER_ID|Se encontraron referencias a la función USER_ID. Utilice en su lugar la función DATABASE_PRINCIPAL_ID. Se produce una vez por cada compilación.|  
|Uso de OLEDB para servidores vinculados||  
|Formato de almacenamiento vardecimal|Se encontró que se usa el de formato de almacenamiento **vardecimal** . En su lugar, use la compresión de datos.|  
|XMLDATA|Se encontró la sintaxis de FOR XML. Utilice la generación XSD para los modos AUTO y RAW. No hay sustituto para el modo explícito. Se produce una vez por cada compilación.|  
|XP_API|Se encontró una instrucción de procedimiento almacenado extendido. No debe usarse.|  
|xp_grantlogin|Se encontró el procedimiento xp_grantlogin. Utilice CREATE LOGIN en su lugar. Se produce una vez por cada compilación.|  
|xp_loginconfig|Se encontró el procedimiento xp_loginconfig. Utilice en su lugar el argumento IsIntegratedSecurityOnly de SERVERPROPERTY. Se produce una vez por cada consulta.|  
|xp_revokelogin|Se encontró el procedimiento xp_revokelogin. Use ALTER LOGIN DISABLE o DROP LOGIN en su lugar. Se produce una vez por cada compilación.|  
  
## <a name="see-also"></a>Vea también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Características en desuso de búsqueda de texto completo en SQL Server 2016](../../relational-databases/search/deprecated-full-text-search-features-in-sql-server-2016.md)   
 [Deprecation Announcement (clase de eventos)](../../relational-databases/event-classes/deprecation-announcement-event-class.md)   
 [Deprecation Final Support (clase de eventos)](../../relational-databases/event-classes/deprecation-final-support-event-class.md)   
 [Funcionalidad del motor de base de datos no incluida en SQL Server 2016](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Características descontinuadas de la búsqueda de texto completo incluidas en SQL Server 2016](http://msdn.microsoft.com/library/70587b3c-cc77-4681-924d-a1df7cdf1517)   
 [Usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md)  
  
  

