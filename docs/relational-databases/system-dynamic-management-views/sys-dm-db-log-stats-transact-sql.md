---
title: Sys.dm_db_log_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_stats dynamic management function
ms.assetid: 
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba933bad47beead99ea5f645a910b1783caa280e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdblogstats-transact-sql"></a>Sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Devuelve los atributos de nivel de resumen e información en archivos de registro de transacciones de bases de datos. Utilice esta información para la supervisión y diagnóstico de estado de registro de transacciones.   
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>Argumentos  

*database_id* | NULL | **Predeterminado**

Es el identificador de la base de datos. `database_id` es `int`. Las entradas válidas son el número de identificación de una base de datos, `NULL`, o `DEFAULT`. El valor predeterminado es `NULL`. `NULL`y `DEFAULT` son valores equivalentes en el contexto de base de datos actual.  
La función integrada `DB_ID` puede especificarse. Cuando se usa `DB_ID` sin especificar un nombre de base de datos, el nivel de compatibilidad de la base de datos actual debe ser 90 o superior.

  
## <a name="tables-returned"></a>Tablas devueltas  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |Id. de base de datos |  
|recovery_model |**nvarchar (60)**   |   Modelo de recuperación de la base de datos. Los valores posibles incluyen: <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   LSN de inicio actual del registro de transacciones. |  
|log_end_lsn    |**nvarchar(24)**   |   LSN de la última entrada de registro en el registro de transacciones. |  
|current_vlf_sequence_number    |**bigint** |   VLF número de secuencia actual en el tiempo de ejecución. |  
|current_vlf_size_mb    |**float**  |   Tamaño actual de VLF en MB. |   
|total_vlf_count    |**bigint** |   Número total de VLF en el registro de transacciones. |  
|total_log_size_mb  |**float**  |   Tamaño de registro de transacciones total en MB. |  
|active_vlf_count   |**bigint** |   Número total de VLF activo en el registro de transacciones. |  
|active_log_size_mb |**float**  |   Tamaño del registro de transacciones activo total en MB. |  
|log_truncation_holdup_reason   |**nvarchar (60)**   |   Motivo de parada de truncamiento de registro. El valor es igual a `log_reuse_wait_desc` columna de `sys.databases`.  (Para obtener más explicaciones de estos valores, consulte [el registro de transacciones](../../relational-databases/logs/the-transaction-log-sql-server.md)). <br />Los valores posibles incluyen: <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />Replicación<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />OTRA TRANSITORIA |  
|log_backup_time    |**datetime**   |   Transacción copia de seguridad hora del último log. |   
|log_backup_lsn |**nvarchar(24)**   |   Última copia de seguridad LSN. |   
|log_since_last_log_backup_mb   |**float**  |   Tamaño en MB del registro desde la última copia de seguridad LSN. |  
|log_checkpoint_lsn |**nvarchar(24)**   |   Último punto de comprobación LSN. |  
|log_since_last_checkpoint_mb   |**float**  |   Tamaño en MB del registro desde el último LSN de punto de comprobación. |  
|log_recovery_lsn   |**nvarchar(24)**   |   LSN de la base de datos de recuperación. Si `log_recovery_lsn` se produce antes del punto de comprobación LSN, `log_recovery_lsn` es la transacción activa más antigua LSN, de lo contrario, `log_recovery_lsn` es el LSN de punto de control. |  
|log_recovery_size_mb   |**float**  |   Tamaño en MB del registro desde LSN de recuperación de registro. |  
|recovery_vlf_count |**bigint** |   Número total de VLF se deben recuperar, si no hay reinicio del servidor o de conmutación por error. |  


## <a name="permissions"></a>Permissions  
Requiere la `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="examples"></a>Ejemplos  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. Determinar las bases de datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia con un gran número de VLF   
La siguiente consulta devuelve las bases de datos con más de 100 VLF en los archivos de registro. Gran número de VLF puede afectar a la hora de inicio, restauración y recuperación de la base de datos.

``` t-sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. Determinar las bases de datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia con copias de seguridad del registro de transacciones anteriores a 4 horas   
La siguiente consulta determina las últimas veces de copia de seguridad de registro para las bases de datos en la instancia.

``` t-sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>Vea también  
[Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Base de datos relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  

  
