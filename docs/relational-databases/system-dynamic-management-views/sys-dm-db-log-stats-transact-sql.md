---
title: Sys.dm_db_log_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_stats dynamic management function
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43e5b145122f5b2586d8eb976162afb0615f89d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846323"
---
# <a name="sysdmdblogstats-transact-sql"></a>Sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Devuelve los atributos de nivel de resumen e información en archivos de registro de transacciones de bases de datos. Utilice esta información para la supervisión y diagnóstico de mantenimiento del registro de transacciones.   
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>Argumentos  

*database_id* | NULL | **Predeterminado**

Es el identificador de la base de datos. El valor de `database_id` es `int`. Las entradas válidas son el número de Id. de una base de datos, `NULL`, o `DEFAULT`. De manera predeterminada, es `NULL`. `NULL` y `DEFAULT` son valores equivalentes en el contexto de base de datos actual.  
La función integrada [DB_ID](../../t-sql/functions/db-id-transact-sql.md) se pueden especificar. Cuando se usa `DB_ID` sin especificar un nombre de base de datos, el nivel de compatibilidad de la base de datos actual debe ser 90 o superior.

  
## <a name="tables-returned"></a>Tablas devueltas  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |Id. de base de datos |  
|recovery_model |**nvarchar(60)**   |   Modelo de recuperación de la base de datos. Los valores posibles incluyen: <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   Inicio actual [(LSN) del número de secuencia de registro](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) en el registro de transacciones.|  
|log_end_lsn    |**nvarchar(24)**   |   [secuencia número de registro (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) de la última entrada de registro en el registro de transacciones.|  
|current_vlf_sequence_number    |**bigint** |   Actual [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) número de secuencia al tiempo de ejecución.|  
|current_vlf_size_mb    |**float**  |   Actual [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) tamaño en MB.|   
|total_vlf_count    |**bigint** |   Número total de [archivos de registro virtuales (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) en el registro de transacciones. |  
|total_log_size_mb  |**float**  |   Tamaño de registro de transacciones total en MB. |  
|active_vlf_count   |**bigint** |   Número total de activos [archivos de registro virtuales (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) en el registro de transacciones.|  
|active_log_size_mb |**float**  |   Tamaño del registro de transacciones activo total en MB.|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   Motivo de parada de truncamiento de registro. El valor es igual que `log_reuse_wait_desc` columna de `sys.databases`.  (Para obtener explicaciones detalladas de estos valores, consulte [el registro de transacciones](../../relational-databases/logs/the-transaction-log-sql-server.md)). <br />Los valores posibles incluyen: <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />Replicación<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />OTRA TRANSITORIA |  
|log_backup_time    |**datetime**   |   Última transacción registro hora copia de seguridad.|   
|log_backup_lsn |**nvarchar(24)**   |   Última copia de seguridad de registro de transacciones [(LSN) del número de secuencia de registro](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|   
|log_since_last_log_backup_mb   |**float**  |   Tamaño del registro en MB desde la última copia de seguridad de registro de transacciones [(LSN) del número de secuencia de registro](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_checkpoint_lsn |**nvarchar(24)**   |   Último punto de comprobación [(LSN) del número de secuencia de registro](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_since_last_checkpoint_mb   |**float**  |   Tamaño del registro en MB desde el último punto de comprobación [(LSN) del número de secuencia de registro](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_recovery_lsn   |**nvarchar(24)**   |   Recuperación [(LSN) del número de secuencia de registro](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) de la base de datos. Si `log_recovery_lsn` se produce antes que el punto de comprobación LSN, `log_recovery_lsn` es la transacción activa más antigua LSN, de lo contrario, `log_recovery_lsn` es el LSN de punto de control.|  
|log_recovery_size_mb   |**float**  |   Tamaño del registro en MB desde la recuperación del registro [(LSN) del número de secuencia de registro](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|recovery_vlf_count |**bigint** |   Número total de [archivos de registro virtuales (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) recuperarse si se produjo el reinicio del servidor o de conmutación por error. |  


## <a name="remarks"></a>Comentarios
Cuando se ejecuta `sys.dm_db_log_stats` contra una base de datos que participa en un grupo de disponibilidad como réplica secundaria, se devolverá sólo un subconjunto de los campos que se ha descrito anteriormente.  Actualmente, solo `database_id`, `recovery_model`, y `log_backup_time` se devolverá cuando se ejecuta en una base de datos secundaria.   

## <a name="permissions"></a>Permisos  
Requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="examples"></a>Ejemplos  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. Determinación de las bases de datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia con un gran número de VLF   
La consulta siguiente devuelve las bases de datos con más de 100 VLF en los archivos de registro. Gran número de VLF puede afectar a la hora de inicio, restauración y recuperación de base de datos.

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. Determinación de las bases de datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia con copias de seguridad del registro de transacciones anteriores a 4 horas   
La siguiente consulta determina las últimas veces de copia de seguridad del registro para las bases de datos en la instancia.

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>Vea también  
[Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
