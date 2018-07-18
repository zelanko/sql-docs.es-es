---
title: Sys.dm_exec_query_parallel_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_parallel_workers_TSQL
- dm_exec_query_parallel_workers
- sys.dm_exec_query_parallel_workers_TSQL
- sys.dm_exec_query_parallel_workers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_parallel_workers dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9f
caps.latest.revision: 1
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f2bc4634a5e2fddb4a3c8eda009eb28019089596
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036313"
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Devuelve información de disponibilidad de trabajo por nodo.  
  
|Nombre|Tipo de datos|Descripción|  
|----------|---------------|-----------------|  
|**node_id**|**int**|Identificador de nodo NUMA.|  
|**scheduler_count**|**int**|Número de programadores en este nodo.|  
|**max_worker_count**|**int**|Número máximo de trabajadores para consultas en paralelo.|  
|**reserved_worker_count**|**int**|Número de trabajadores reservados por las consultas en paralelo, además del número de trabajadores principales que usan todas las solicitudes.| 
|**free_worker_count**|**int**|Número de trabajadores disponibles para las tareas.<br /><br />**Nota:** todas las solicitudes entrantes consume al menos 1 trabajo, que se resta el recuento de trabajo disponible.  Es posible que el recuento de trabajo disponible puede ser un número negativo en un servidor con mucha cargado.| 
|**used_worker_count**|**int**|Número de trabajos usados por las consultas en paralelo.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
 
## <a name="examples"></a>Ejemplos  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. Ver la disponibilidad actual de trabajo en paralelo  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
