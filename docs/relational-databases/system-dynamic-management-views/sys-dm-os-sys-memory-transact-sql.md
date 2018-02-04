---
title: sys.dm_os_sys_memory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_sys_memory
- sys.dm_os_sys_memory_TSQL
- sys.dm_os_sys_memory
- dm_os_sys_memory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_memory dynamic management view
ms.assetid: 1ca58814-1caa-44c1-b307-ff0bdcbbef62
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5ac5e7d7fad2ceabdbfbfe30b73529ffb8d960d2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmossysmemory-transact-sql"></a>sys.dm_os_sys_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Devuelve información sobre la memoria del sistema operativo.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está limitado por y responde a las condiciones de memoria externa en el nivel de sistema operativo y los límites físicos del hardware subyacente. Determinar el estado general del sistema es una parte importante de la evaluación del uso de la memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_sys_memory**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**total_physical_memory_kb**|**bigint**|Tamaño total de la memoria física disponible para el sistema operativo, en kilobytes (KB).|  
|**available_physical_memory_kb**|**bigint**|Tamaño de la memoria física disponible, en KB.|  
|**total_page_file_kb**|**bigint**|Tamaño del límite de confirmación indicado por el sistema operativo, en KB|  
|**available_page_file_kb**|**bigint**|Cantidad total del archivo de paginación que no se usa, en KB.|  
|**system_cache_kb**|**bigint**|Cantidad total de la memoria caché del sistema, en KB.|  
|**kernel_paged_pool_kb**|**bigint**|Cantidad total del bloque de kernel paginado, en KB.|  
|**kernel_nonpaged_pool_kb**|**bigint**|Cantidad total del bloque de kernel no paginado, en KB.|  
|**system_high_memory_signal_state**|**bit**|Estado de la notificación de recursos de memoria alta del sistema. Un valor de 1 indica que Windows ha establecido la señal de memoria alta. Para obtener más información, consulte [CreateMemoryResourceNotification](http://go.microsoft.com/fwlink/?LinkId=82427) en MSDN library.|  
|**system_low_memory_signal_state**|**bit**|Estado de la notificación de recursos de memoria baja del sistema. Un valor de 1 indica que Windows ha establecido la señal de memoria baja. Para obtener más información, consulte [CreateMemoryResourceNotification](http://go.microsoft.com/fwlink/?LinkId=82427) en MSDN library.|  
|**system_memory_state_desc**|**nvarchar(256)**|Descripción del estado de la memoria. Vea la siguiente tabla.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
|Condición|Value|  
|---------------|-----------|  
|system_high_memory_signal_state = 1<br /><br /> y<br /><br /> system_low_memory_signal_state = 0|La memoria física disponible es alta.|  
|system_high_memory_signal_state = 0<br /><br /> y<br /><br /> system_low_memory_signal_state = 1|La memoria física disponible es baja.|  
|system_high_memory_signal_state = 0<br /><br /> y<br /><br /> system_low_memory_signal_state = 0|El uso de la memoria física es continuo|  
|system_high_memory_signal_state = 1<br /><br /> y<br /><br /> system_low_memory_signal_state = 1|El estado de la memoria física está cambiando<br /><br /> Las señales alta y baja nunca deben estar activas de manera simultánea. Sin embargo, los cambios rápidos que se realizan en el sistema operativo pueden hacer que ambos valores parezcan estar activos en una aplicación de modo usuario. El que ambas señales aparezcan activas se interpretará como un estado de transición.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operativo SQL Server relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


