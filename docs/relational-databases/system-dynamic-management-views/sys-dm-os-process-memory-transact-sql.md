---
title: Sys.dm_os_process_memory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 03830b00df02332069383e496c0b22d198b95d7a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597031"
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  La mayoría de las asignaciones de memoria que se atribuyen al espacio de proceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se controlan a través de interfaces que permiten realizar el seguimiento y las estimaciones de esas asignaciones. Sin embargo, las asignaciones de memoria se puede realizar en el espacio de direcciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que omite las rutinas de administración de memoria interna. Los valores se obtienen a través de las llamadas al sistema operativo base. No están manipuladas por métodos internos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], excepto cuando se ajusta para bloqueado o asignaciones de páginas grandes.  
  
 Todos los valores devueltos que indican tamaños de memoria se muestran en kilobytes (KB). La columna **total_virtual_address_space_reserved_kb** es un duplicado de **virtual_memory_in_bytes** desde **sys.dm_os_sys_info**.  
  
 La tabla siguiente proporciona una imagen completa del espacio de direcciones del proceso.  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_process_memory**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|Indica el conjunto de trabajo de procesos, en KB, tal y como informa el sistema operativo, así como las asignaciones realizadas utilizando las API de página grande. No acepta valores NULL.|  
|**large_page_allocations_kb**|**bigint**|Especifica la memoria física asignada por medio de las API de página grande. No acepta valores NULL.|  
|**locked_page_allocations_kb**|**bigint**|Especifica las páginas de memoria bloqueadas en memoria. No acepta valores NULL.|  
|**total_virtual_address_space_kb**|**bigint**|Indica el tamaño total de la parte del modo usuario del espacio de direcciones virtuales. No acepta valores NULL.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indica la cantidad total de espacio de direcciones virtuales reservada por el proceso. No acepta valores NULL.|  
|**virtual_address_space_committed_kb**|**bigint**|Indica la cantidad de espacio de direcciones virtuales reservada que se ha confirmado o asignado a las páginas físicas. No acepta valores NULL.|  
|**virtual_address_space_available_kb**|**bigint**|Indica la cantidad de espacio de direcciones virtuales que está actualmente libre. No acepta valores NULL.<br /><br /> **Nota:** libre regiones que sea menores que la granularidad de asignación puede existir. Estas regiones no están disponibles para las asignaciones.|  
|**page_fault_count**|**bigint**|Indica el número de errores de página en los que incurre el proceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No acepta valores NULL.|  
|**memory_utilization_percentage**|**int**|Especifica el porcentaje de memoria confirmada que se encuentra en el conjunto de trabajo. No acepta valores NULL.|  
|**available_commit_limit_kb**|**bigint**|Indica la cantidad de memoria que está disponible para la confirmación por parte del proceso. No acepta valores NULL.|  
|**process_physical_memory_low**|**bit**|Indica que el proceso responde a una notificación de memoria física baja. No acepta valores NULL.|  
|**process_virtual_memory_low**|**bit**|Indica que se ha detectado una condición de memoria virtual baja. No acepta valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere el permiso VIEW SERVER STATE en el servidor.  
  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


