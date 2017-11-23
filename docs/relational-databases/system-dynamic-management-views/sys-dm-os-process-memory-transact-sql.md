---
title: Sys.dm_os_process_memory (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2941cc2e290d08f8c634dc38634544f036aea79c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  La mayoría de las asignaciones de memoria que se atribuyen al espacio de proceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se controlan a través de interfaces que permiten realizar el seguimiento y las estimaciones de esas asignaciones. Sin embargo, las asignaciones de memoria se puede realizar en el espacio de direcciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que omite las rutinas de administración de memoria interna. Los valores se obtienen a través de las llamadas al sistema operativo base. No están manipuladas por métodos internos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], excepto cuando se ajusta para bloquear o las asignaciones de página grande.  
  
 Todos los valores devueltos que indican tamaños de memoria se muestran en kilobytes (KB). La columna **total_virtual_address_space_reserved_kb** es un duplicado de **virtual_memory_in_bytes** de **sys.dm_os_sys_info**.  
  
 La tabla siguiente proporciona una imagen completa del espacio de direcciones del proceso.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_process_memory**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|Indica el conjunto de trabajo de procesos, en KB, tal y como informa el sistema operativo, así como las asignaciones realizadas utilizando las API de página grande. No acepta valores NULL.|  
|**large_page_allocations_kb**|**bigint**|Especifica la memoria física asignada por medio de las API de página grande. No acepta valores NULL.|  
|**locked_page_allocations_kb**|**bigint**|Especifica las páginas de memoria bloqueadas en memoria. No acepta valores NULL.|  
|**total_virtual_address_space_kb**|**bigint**|Indica el tamaño total de la parte del modo usuario del espacio de direcciones virtuales. No acepta valores NULL.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indica la cantidad total de espacio de direcciones virtuales reservada por el proceso. No acepta valores NULL.|  
|**virtual_address_space_committed_kb**|**bigint**|Indica la cantidad de espacio de direcciones virtuales reservada que se ha confirmado o asignado a las páginas físicas. No acepta valores NULL.|  
|**virtual_address_space_available_kb**|**bigint**|Indica la cantidad de espacio de direcciones virtuales que está actualmente libre. No acepta valores NULL.<br /><br /> **Nota:** libre regiones que sea menores que puede existir la granularidad de asignación. Estas regiones no están disponibles para las asignaciones.|  
|**page_fault_count**|**bigint**|Indica el número de errores de página en los que incurre el proceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No acepta valores NULL.|  
|**memory_utilization_percentage**|**int**|Especifica el porcentaje de memoria confirmada que se encuentra en el conjunto de trabajo. No acepta valores NULL.|  
|**available_commit_limit_kb**|**bigint**|Indica la cantidad de memoria que está disponible para la confirmación por parte del proceso. No acepta valores NULL.|  
|**process_physical_memory_low**|**bit**|Indica que el proceso responde a una notificación de memoria física baja. No acepta valores NULL.|  
|**process_virtual_memory_low**|**bit**|Indica que se ha detectado una condición de memoria virtual baja. No acepta valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere el permiso VIEW SERVER STATE en el servidor.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles Premium requieren el permiso VIEW DATABASE STATE en la base de datos. En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles estándar y básico requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operativo SQL Server relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


