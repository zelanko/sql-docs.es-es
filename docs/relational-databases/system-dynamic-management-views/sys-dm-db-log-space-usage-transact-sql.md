---
title: Sys.dm_db_log_space_usage (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_space_usage
- sys.dm_db_log_space_usage_TSQL
- dm_db_log_space_usage
- dm_db_log_space_usage_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_space_usage dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: "4"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7e0e14e96c3581b7a66fad23e21ac7a15808a1f
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmdblogspaceusage-transact-sql"></a>Sys.dm_db_log_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve el espacio de información de uso para el registro de base de datos. (Se combinan todos los archivos de registro). 
  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|Id. de la base de datos.|  
|total_log_size_in_bytes |**bigint** |El tamaño del registro  |
|used_log_space_in_bytes |**bigint** |El tamaño del registro de ocupado  |     
|used_log_space_in_percent |**real** |El tamaño del registro como un porcentaje del tamaño total de registro esté ocupado |
|log_space_in_bytes_since_last_backup |**bigint** |La cantidad de espacio utilizado desde la última copia de seguridad del registro <br />**Se aplica a:** [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)] a través de [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|
    
  
## <a name="permissions"></a>Permissions  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere `VIEW SERVER STATE` permiso en el servidor.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles Premium requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles estándar y básico requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-determine-the-amount-of-free-log-space-in-tempdb"></a>A. Determinar la cantidad de registro de espacio libre en tempdb   
La consulta siguiente devuelve el espacio de registro total en megabytes (MB) que están disponibles en tempdb.

```sql
USE tempdb;  
GO  

SELECT (total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024 AS [free log space in MB]  
FROM sys.dm_db_log_space_usage;  
```
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Base de datos relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)    
 [Sys.dm_db_task_space_usage &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) 



