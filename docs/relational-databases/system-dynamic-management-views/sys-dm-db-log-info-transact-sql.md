---
title: Sys.dm_db_log_info (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: 
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: 661647715d2fcff3a4821250dfaa65e0fea07d6e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="sysdmdbloginfo-transact-sql"></a>Sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Devuelve [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) información del registro de transacciones. Tenga en cuenta que todos los archivos de registro de transacciones se combinan en la salida de la tabla. Cada fila de la salida representa un VLF en el registro de transacciones y proporciona información relevante para esa VLF en el registro.

## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>Argumentos  
 *database_id* | NULL | VALOR PREDETERMINADO  
 Es el identificador de la base de datos. *database_id* es **int**. Las entradas válidas son el número de identificación de una base de datos, NULL o DEFAULT. El valor predeterminado es NULL. NULL y DEFAULT son valores equivalentes en el contexto de base de datos actual.
 
 Especifique NULL para devolver información de VLF de la base de datos actual.

 La función integrada [DB_ID](../../t-sql/functions/db-id-transact-sql.md) puede especificarse. Cuando se usa `DB_ID` sin especificar un nombre de base de datos, el nivel de compatibilidad de la base de datos actual debe ser 90 o superior.  

## <a name="table-returned"></a>Tabla devuelta  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Id. de la base de datos.|
|file_id|**smallint**|Id. de archivo del registro de transacciones.|  
|vlf_begin_offset|**bigint** |Desplazar la ubicación de la [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) desde el principio del archivo de registro de transacciones.|
|vlf_size_mb |**float** |[archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) tamaño en MB, se redondea a 2 posiciones decimales.|     
|vlf_sequence_number|**bigint** |[archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) de secuencia de número en el orden creado. Se utiliza para identificar de forma única VLF en archivo de registro.|
|vlf_active|**bit** |Indica si [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) está en uso o no. <br />0 - VLF no está en uso.<br />1 - VLF está activo.|
|vlf_status|**int** |Estado de la [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Los valores posibles incluyen <br />0 - VLF está inactivo <br />1 - VLF está inicializado, pero sin utilizar <br /> 2 - VLF está activo.|
|vlf_parity|**tinyint** |Paridad de [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Se usa internamente para determinar el final del registro dentro de un VLF.|
|vlf_first_lsn|**nvarchar(48)** |[Secuencia número de registro (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) de la primera entrada del registro en el [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|
|vlf_create_lsn|**nvarchar(48)** |[Secuencia número de registro (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) del registro de registro con el que creó el [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|

## <a name="remarks"></a>Comentarios
 El `sys.dm_db_log_info` función de administración dinámica reemplaza el `DBCC LOGINFO` instrucción. 
 
## <a name="permissions"></a>Permissions  
 Requiere la `VIEW DATABASE STATE` permiso en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. Determinación bases de datos en una instancia de SQL Server con un gran número de VLF
La siguiente consulta determina las bases de datos con más de 100 VLF en los archivos de registro, lo que pueden afectar a la hora de inicio, restauración y recuperación de la base de datos.

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Determinar el estado de la última `VLF` en el registro de transacciones antes de reducir el archivo de registro

La consulta siguiente puede utilizarse para determinar el estado del último VLF antes de ejecutar shrinkfile en el registro de transacciones para determinar si puede reducir el registro de transacciones.

```sql
USE AdventureWorks2016
GO

SELECT TOP 1 DB_NAME(database_id) AS "Database Name", file_id, vlf_size_mb, vlf_sequence_number, vlf_active, vlf_status
FROM sys.dm_db_log_info(DEFAULT)
ORDER BY vlf_sequence_number DESC
```


## <a name="see-also"></a>Vea también  
[Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Base de datos relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[Sys.dm_db_log_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

