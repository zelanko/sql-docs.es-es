---
title: sys.dm_clr_tasks (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_tasks
- sys.dm_clr_tasks_TSQL
- dm_clr_tasks
- dm_clr_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_tasks dynamic management view
ms.assetid: 462b9061-09fa-4858-9707-03d6cc19c769
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a3c99ffd172c97c5738ed2dd19bc8b07f303470
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmclrtasks-transact-sql"></a>sys.dm_clr_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila de todas las tareas CLR (Common Language Runtime) que se están ejecutando actualmente. Un lote de [!INCLUDE[tsql](../../includes/tsql-md.md)] que contiene una referencia a una rutina CLR crea una tarea independiente para la ejecución de todo el código administrado en ese lote. Muchas instrucciones del lote que requieren la ejecución del código administrado utilizan la misma tarea CLR. La tarea CLR es responsable del mantenimiento de objetos y el estado relativo a la ejecución de código administrado y también de las transacciones entre la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y CLR.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|Dirección de la tarea CLR.|  
|**sos_task_address**|**varbinary(8)**|Dirección de la tarea del lote [!INCLUDE[tsql](../../includes/tsql-md.md)] subyacente.|  
|**appdomain_address**|**varbinary(8)**|Dirección del dominio de la aplicación en la que se ejecuta esta tarea.|  
|**state**|**nvarchar(128)**|Estado actual de la tarea.|  
|**abort_state**|**nvarchar(128)**|Estado en el que está actualmente la cancelación (si la tarea se ha cancelado). Hay varios estados implicados en la anulación de tareas.|  
|**Tipo**|**nvarchar(128)**|Tipo de tarea.|  
|**affinity_count**|**int**|Afinidad de la tarea.|  
|**forced_yield_count**|**int**|Número de veces que se forzó a la tarea a producir.|  
  
## <a name="permissions"></a>Permissions  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere el permiso VIEW SERVER STATE en el servidor.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles Premium requieren el permiso VIEW DATABASE STATE en la base de datos. En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles estándar y básico requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Common Language Runtime relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  

