---
title: Sys.dm_os_memory_cache_entries (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_memory_cache_entries
- sys.dm_os_memory_cache_entries
- dm_os_memory_cache_entries_TSQL
- sys.dm_os_memory_cache_entries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_entries dynamic management view
ms.assetid: dd32be6b-10d1-4059-b4fd-0bf817f40d54
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77385cfc2a48ed584a404fc2d79ca1e3eeaff966
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmosmemorycacheentries-transact-sql"></a>sys.dm_os_memory_cache_entries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de todas las entradas en las memorias caché de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilice esta vista para realizar el seguimiento de las entradas de memoria caché con sus objetos asociados. También puede utilizarla para obtener estadísticas sobre entradas de caché.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_memory_cache_entries**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|Dirección de la caché. No admite valores NULL.|  
|**Nombre**|**nvarchar(256)**|Nombre de la caché. No admite valores NULL.|  
|**Tipo**|**varchar(60)**|Tipo de caché. No admite valores NULL.|  
|**entry_address**|**varbinary (8)**|Dirección del descriptor de la entrada de caché. No admite valores NULL.|  
|**entry_data_address**|**varbinary (8)**|Dirección de los datos de usuario en la entrada de caché.<br /><br /> 0x00000000 = No está disponible la dirección de datos de entrada.<br /><br /> No admite valores NULL.|  
|**in_use_count**|**int**|Número de usuarios simultáneos de esta entrada de caché. No admite valores NULL.|  
|**is_dirty**|**bit**|Indica si esta entrada de caché está marcada para su eliminación. 1 = marcado para eliminación. No admite valores NULL.|  
|**disk_ios_count**|**int**|Número de operaciones de E/S producidas al crearse esta entrada. No admite valores NULL.|  
|**context_switches_count**|**int**|Número de cambios de contexto producidos al crearse esta entrada. No admite valores NULL.|  
|**original_cost**|**int**|Costo original de la entrada. Este valor es una aproximación del número de operaciones de E/S producidas, el costo de instrucciones de CPU y la cantidad de memoria consumida por entrada. Cuanto mayor sea el costo, menor será la probabilidad de que se quite el elemento de la memoria caché. No admite valores NULL.|  
|**current_cost**|**int**|Costo actual de la entrada de caché. Este valor se actualiza durante el purgado de entradas. El costo actual se restablece a su valor original cuando se vuelve a utilizar la entrada. No admite valores NULL.|  
|**memory_object_address**|**varbinary (8)**|Dirección del objeto de memoria asociado. Acepta valores NULL.|  
|**pages_allocated_count**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Número de páginas de 8 KB que almacenan esta entrada de caché. No admite valores NULL.|  
|**pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Cantidad de memoria en kilobytes (KB) que esta entrada de caché usa.  No admite valores NULL.|  
|**entry_data**|**nvarchar(2048)**|Representación en serie de la entrada de caché. Esta información es dependiente del almacén de caché. Acepta valores NULL.|  
|**pool_id**|**int**|**Se aplica a**: desde [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Identificador del grupo de recursos de servidor asociado a la entrada. Acepta valores NULL.<br /><br /> no katmai|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions 

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="see-also"></a>Vea también  
 
  [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


