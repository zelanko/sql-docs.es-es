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
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: "4"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: b7250943f4e92d60888a75d9e577388f3cc6b1ed
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbloginfo-transact-sql"></a>Sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Devuelve `VLF` información de los archivos de registro de transacciones. (Todos los archivos de registro se combinan en la salida de la tabla). Cada fila de la salida representa un `VLF` en el registro de transacciones y se proporciona información relevante para esa VLF en el registro.

## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>Argumentos  
 *database_id* | NULL | VALOR PREDETERMINADO  
 Es el identificador de la base de datos. *database_id* es **int**. Las entradas válidas son el número de identificación de una base de datos, NULL o DEFAULT. El valor predeterminado es NULL. NULL y DEFAULT son valores equivalentes en el contexto de base de datos actual.
 
 Especifique NULL para devolver `VLF` información de la base de datos actual.

 La función integrada [DB_ID](../../t-sql/functions/db-id-transact-sql.md) puede especificarse. Al usar DB_ID sin especificar ningún nombre de base de datos, el nivel de compatibilidad de la base de datos actual debe ser 90 o superior.  

## <a name="table-returned"></a>Tabla devuelta  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Id. de la base de datos.|
|file_id|**smallint**|Id. de archivo del registro de transacciones.|  
|vlf_begin_offset|**bigint** |Desplazar la ubicación de la `VLF` desde el principio del archivo de registro de transacciones.|
|vlf_size_mb |**float** |`VLF`tamaño en MB se redondea a 2 posiciones decimales.|     
|vlf_sequence_number|**bigint** |`VLF`número de secuencia en el orden creado. Usar para identificar de forma exclusiva `VLFs` en archivo de registro.|
|vlf_active|**bit** |Indica si VLF está en uso o no. <br />0 - vlf no está en uso.<br />1 - `VLF` está activo.|
|vlf_status|**int** |Estado de la `VLF`. Los valores posibles incluyen <br />0 - `VLF` está inactivo <br />1 - vlf está inicializado, pero sin utilizar <br /> 2 - `VLF` está activo.|
|vlf_parity|**tinyint** |Paridad de `VLF`. Se usa internamente para determinar el final del registro dentro de un `VLF`.|
|vlf_first_lsn|**nvarchar(48)** |LSN de la primera entrada del registro en el `VLF`.|
|vlf_create_lsn|**nvarchar(48)** |Registro con el LSN del registro que creó el `VLF`.|

## <a name="remarks"></a>Comentarios
 El `sys.dm_db_log_info` función de administración dinámica reemplaza el `DBCC LOGINFO` instrucción. 
 
## <a name="permissions"></a>Permissions  
 Requiere la `VIEW DATABASE STATE` permiso en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. Determinación bases de datos en una instancia de SQL Server con un gran número de`VLFs`
La siguiente consulta determina las bases de datos con más de 100 `VLFs` en los archivos de registro, que puede afectar a la hora de inicio, restauración y recuperación de la base de datos.

```sql
SELECT name,count(l.database_id) as 'vlf_count' from sys.databases s
cross apply sys.dm_db_log_info(s.database_id) l
group by name
having count(l.database_id)> 100
```

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Determinar el estado de la última `VLF` en el registro de transacciones antes de reducir el archivo de registro

La siguiente consulta se puede utilizar para determinar el estado de la última `VLF` antes de ejecutar shrinkfile en el registro de transacciones para determinar si puede reducir el registro de transacciones.

```sql
USE <database name>
GO

SELECT top 1 DB_NAME(database_id) as "Database Name",file_id,vlf_size_mb,vlf_sequence_number, vlf_active, vlf_status
from sys.dm_db_log_info(DEFAULT)
order by vlf_sequence_number desc
```


## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Base de datos relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  



