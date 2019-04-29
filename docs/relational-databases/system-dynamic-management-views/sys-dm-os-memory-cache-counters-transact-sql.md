---
title: sys.dm_os_memory_cache_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 19beaafe3e73265eb12f825190ee8aafcdf59897
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047403"
---
# <a name="sysdmosmemorycachecounters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una instantánea del estado de una memoria caché en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Sys.dm_os_memory_cache_counters** proporciona información de tiempo de ejecución acerca de las entradas de caché asignadas, su uso y el origen de la memoria para las entradas de caché.  
  
> **NOTA:** Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_memory_cache_counters**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Indica la dirección (clave principal) de los recuentos asociados con una memoria caché específica. No admite valores NULL.|  
|**Nombre**|**nvarchar(256)**|Especifica el nombre de la memoria caché. No admite valores NULL.|  
|**Tipo**|**nvarchar(60)**|Indica el tipo de memoria caché asociado con esta entrada. No admite valores NULL.|  
|**single_pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Cantidad, en kilobytes, de memoria de página única asignada. Se trata de la cantidad de memoria asignada mediante el asignador de página única. Se refiere a las páginas de 8 KB tomadas directamente del grupo de búferes para esta caché. No admite valores NULL.|  
|**pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica la cantidad, en kilobytes, de la memoria asignada a la memoria caché. No admite valores NULL.|  
|**multi_pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Cantidad, en kilobytes, de memoria de varias páginas asignada. Es la cantidad de memoria asignada mediante el asignador de varias páginas del nodo de memoria. Esta memoria se asigna fuera del grupo de búferes y aprovecha las ventajas del asignador virtual de los nodos de memoria. No admite valores NULL.|  
|**pages_in_use_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica la cantidad, en kilobytes, de la memoria asignada que está en uso en la memoria caché. Acepta valores NULL.  No se realiza el seguimiento de los valores de objetos de tipo `USERSTORE_<*>`.  Para esos valores se notifica NULL.|  
|**single_pages_in_use_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Cantidad, en kilobytes, de memoria de página única utilizada. Acepta valores NULL. No se realiza el seguimiento de esta información para objetos de tipo USERSTORE_\<* > y estos valores serán NULL.|  
|**multi_pages_in_use_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Cantidad, en kilobytes, de la memoria de varias páginas utilizada. QUE ACEPTA VALORES NULL. No se realiza el seguimiento de esta información para objetos de tipo USERSTORE_\<* >, y estos valores serán NULL.|  
|**entries_count**|**bigint**|Indica el número de entradas que hay en la memoria caché. No admite valores NULL.|  
|**entries_in_use_count**|**bigint**|Indica el número de entradas que hay en la memoria caché que se está usando. No admite valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos 

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="see-also"></a>Vea también  
  [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


