---
title: Sys.dm_exec_session_wait_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d5932d5fa878f3816c636b6106c2723a40834be
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34465081"
---
# <a name="sysdmexecsessionwaitstats-transact-sql"></a>Sys.dm_exec_session_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de todas las esperas encontradas por los subprocesos ejecutados para cada sesión. Puede usar esta vista para diagnosticar problemas de rendimiento con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sesión y también con lotes y consultas específicas.  Esta vista devuelve la sesión de la misma información que se agrega a [sys.dm_os_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) , pero proporciona la **session_id** número así.  
  
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|El identificador de la sesión.|  
|wait_type|**nvarchar(60)**|Nombre del tipo de espera. Para obtener más información, vea [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|waiting_tasks_count|**bigint**|Número de esperas de este tipo de espera. Este recuento se incrementa al inicio de cada espera.|  
|wait_time_ms|**bigint**|Tiempo total de espera de este tipo en milisegundos. Este tiempo incluye el tiempo de signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tiempo de espera máximo de este tipo de espera.|  
|signal_wait_time_ms|**bigint**|Diferencia entre el momento en que se indicó el subproceso en espera y el momento en que empezó a ejecutarse.|  
  
## <a name="remarks"></a>Comentarios  
 Esta DMV restablece la información de una sesión cuando se abre la sesión o cuando se restablece la sesión (si la agrupación de conexiones),  
  
 Para obtener información acerca de los tipos de espera, vea [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Si el usuario tiene **VIEW SERVER STATE** permiso en el servidor, el usuario verá las sesiones en ejecución todo en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; de lo contrario, el usuario verá solo la sesión actual.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
