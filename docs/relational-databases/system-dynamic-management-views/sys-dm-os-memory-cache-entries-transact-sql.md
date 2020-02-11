---
title: Sys. dm_os_memory_cache_entries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 737de971ca39cdf8c164787ff7703b87c38e92e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73983121"
---
# <a name="sysdm_os_memory_cache_entries-transact-sql"></a>sys.dm_os_memory_cache_entries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de todas las entradas en las memorias caché de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilice esta vista para realizar el seguimiento de las entradas de memoria caché con sus objetos asociados. También puede utilizarla para obtener estadísticas sobre entradas de caché.  
  
> [!NOTE]  
>  Para llamar a este [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] método [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]desde o, use el nombre **Sys. dm_pdw_nodes_os_memory_cache_entries**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8**|Dirección de la caché. No admite valores NULL.|  
|**Name**|**nvarchar(256)**|Nombre de la caché. No admite valores NULL.|  
|**automáticamente**|**varchar(60)**|Tipo de caché. No admite valores NULL.|  
|**entry_address**|**varbinary(8**|Dirección del descriptor de la entrada de caché. No admite valores NULL.|  
|**entry_data_address**|**varbinary(8**|Dirección de los datos de usuario en la entrada de caché.<br /><br /> 0x00000000 = No está disponible la dirección de datos de entrada.<br /><br /> No admite valores NULL.|  
|**in_use_count**|**int**|Número de usuarios simultáneos de esta entrada de caché. No admite valores NULL.|  
|**is_dirty**|**bit**|Indica si esta entrada de caché está marcada para su eliminación. 1 = marcado para eliminación. No admite valores NULL.|  
|**disk_ios_count**|**int**|Número de operaciones de E/S producidas al crearse esta entrada. No admite valores NULL.|  
|**context_switches_count**|**int**|Número de cambios de contexto producidos al crearse esta entrada. No admite valores NULL.|  
|**original_cost**|**int**|Costo original de la entrada. Este valor es una aproximación del número de operaciones de E/S producidas, el costo de instrucciones de CPU y la cantidad de memoria consumida por entrada. Cuanto mayor sea el costo, menor será la probabilidad de que se quite el elemento de la memoria caché. No admite valores NULL.|  
|**current_cost**|**int**|Costo actual de la entrada de caché. Este valor se actualiza durante el purgado de entradas. El costo actual se restablece a su valor original cuando se vuelve a utilizar la entrada. No admite valores NULL.|  
|**memory_object_address**|**varbinary(8**|Dirección del objeto de memoria asociado. Acepta valores NULL.|  
|**pages_allocated_count**|**BIGINT**|**Se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] : [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]hasta.<br /><br /> Número de páginas de 8 KB que almacenan esta entrada de caché. No admite valores NULL.|  
|**pages_kb**|**BIGINT**|**Válido para** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> Cantidad de memoria en kilobytes (KB) que esta entrada de caché usa.  No admite valores NULL.|  
|**entry_data**|**nvarchar (2048)**|Representación en serie de la entrada de caché. Esta información es dependiente del almacén de caché. Acepta valores NULL.|  
|**pool_id**|**int**|**Válido para** : [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] y versiones posteriores.<br /><br /> Identificador del grupo de recursos de servidor asociado a la entrada. Acepta valores NULL.<br /><br /> no katmai|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos 

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

## <a name="see-also"></a>Consulte también  
 
  [SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


