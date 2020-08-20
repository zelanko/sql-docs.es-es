---
description: Sys. dm_db_log_space_usage (Transact-SQL)
title: Sys. dm_db_log_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_space_usage
- sys.dm_db_log_space_usage_TSQL
- dm_db_log_space_usage
- dm_db_log_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_space_usage dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 62bb7d8d5aef48e8516ce74721b38f3c7003c6b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498416"
---
# <a name="sysdm_db_log_space_usage-transact-sql"></a>Sys. dm_db_log_space_usage (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Devuelve información de uso de espacio para el registro de transacciones. 
  
> [!NOTE]
> Se combinan todos los archivos de registro de transacciones.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|Id. de la base de datos.|  
|total_log_size_in_bytes |**bigint** |Tamaño del registro  |
|used_log_space_in_bytes |**bigint** |Tamaño ocupado del registro  |     
|used_log_space_in_percent |**real** |Tamaño ocupado del registro como porcentaje del tamaño total del registro |
|log_space_in_bytes_since_last_backup |**bigint** |La cantidad de espacio que se usa desde la última copia de seguridad de registros <br />**Se aplica a:** [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)] a través [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] de,  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .|
    
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiere el `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el  **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-determine-the-amount-of-free-log-space-in-tempdb"></a>A. Determinar la cantidad de espacio libre en el registro de tempdb   
La siguiente consulta devuelve el espacio de registro libre total en megabytes (MB) disponible en tempdb.

```sql
USE tempdb;  
GO  

SELECT (total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024 AS [free log space in MB]  
FROM sys.dm_db_log_space_usage;  
```
  
## <a name="see-also"></a>Vea también  
[Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Vistas de administración dinámica relacionadas con bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[Sys. dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)    
[Sys. dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
[sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) 



