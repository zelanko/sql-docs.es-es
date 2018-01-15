---
title: Sys.dm_exec_query_parallel_workers (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_query_parallel_workers_TSQL
- dm_exec_query_parallel_workers
- sys.dm_exec_query_parallel_workers_TSQL
- sys.dm_exec_query_parallel_workers
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_query_parallel_workers dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9f
caps.latest.revision: "1"
author: pelopes
ms.author: pelopes
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: 99165e38dc4f1ad0b25a754f2c0f38b4ae413e84
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>Sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Devuelve información de disponibilidad de trabajo por nodo.  
  
|Nombre|Tipo de datos|Description|  
|----------|---------------|-----------------|  
|**node_id**|**int**|Identificador de nodo NUMA.|  
|**scheduler_count**|**int**|Número de programadores en este nodo.|  
|**max_worker_count**|**int**|Número máximo de trabajadores para las consultas en paralelo.|  
|**reserved_worker_count**|**int**|Número de trabajos reservados por las consultas en paralelo, más el número de trabajos principales usados por todas las solicitudes.| 
|**free_worker_count**|**int**|Número de trabajadores disponibles para las tareas.<br /><br />**Nota:** todas las solicitudes entrantes consume al menos 1 trabajo, que se resta del recuento de trabajo disponible.  Es posible que el recuento de trabajo disponible puede ser un número negativo en un servidor con mucha cargado.| 
|**used_worker_count**|**int**|Número de trabajos usados por las consultas en paralelo.|  
  
## <a name="permissions"></a>Permissions  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere el permiso VIEW SERVER STATE en el servidor.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles Premium requieren el permiso VIEW DATABASE STATE en la base de datos. En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles estándar y básico requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. Ver la disponibilidad actual de trabajo paralelo  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica &#40; relacionada con la ejecución Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sys.dm_os_workers &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
