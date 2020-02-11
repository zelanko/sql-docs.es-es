---
title: Sys. dm_os_memory_cache_counters (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 755e0cdbf5bff5bcd9c048a2f77918dc9a6eb2a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73982526"
---
# <a name="sysdm_os_memory_cache_counters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una instantánea del estado de una memoria caché en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Sys. dm_os_memory_cache_counters** proporciona información en tiempo de ejecución acerca de las entradas de caché asignadas, su uso y el origen de la memoria de las entradas de la memoria caché.  
  
> **Nota:** Para llamar a este [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] método [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]desde o, use el nombre **Sys. dm_pdw_nodes_os_memory_cache_counters**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8**|Indica la dirección (clave principal) de los recuentos asociados con una memoria caché específica. No admite valores NULL.|  
|**Name**|**nvarchar(256)**|Especifica el nombre de la memoria caché. No admite valores NULL.|  
|**automáticamente**|**nvarchar (60)**|Indica el tipo de memoria caché asociado con esta entrada. No admite valores NULL.|  
|**single_pages_kb**|**BIGINT**|**Se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] : [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]hasta.<br /><br /> Cantidad, en kilobytes, de memoria de página única asignada. Se trata de la cantidad de memoria asignada mediante el asignador de página única. Se refiere a las páginas de 8 KB tomadas directamente del grupo de búferes para esta caché. No admite valores NULL.|  
|**pages_kb**|**BIGINT**|**Válido para** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> Especifica la cantidad, en kilobytes, de la memoria asignada a la memoria caché. No admite valores NULL.|  
|**multi_pages_kb**|**BIGINT**|**Se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] : [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]hasta.<br /><br /> Cantidad, en kilobytes, de memoria de varias páginas asignada. Es la cantidad de memoria asignada mediante el asignador de varias páginas del nodo de memoria. Esta memoria se asigna fuera del grupo de búferes y aprovecha las ventajas del asignador virtual de los nodos de memoria. No admite valores NULL.|  
|**pages_in_use_kb**|**BIGINT**|**Válido para** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> Especifica la cantidad, en kilobytes, de la memoria asignada que está en uso en la memoria caché. Acepta valores NULL.  No se realiza el seguimiento de los valores de objetos de tipo `USERSTORE_<*>`.  Para esos valores se notifica NULL.|  
|**single_pages_in_use_kb**|**BIGINT**|**Se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] : [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]hasta.<br /><br /> Cantidad, en kilobytes, de memoria de página única utilizada. Acepta valores NULL. No se realiza un seguimiento de esta información para objetos de\<tipo USERSTORE_ * > y estos valores serán null.|  
|**multi_pages_in_use_kb**|**BIGINT**|**Se aplica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] : [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]hasta.<br /><br /> Cantidad, en kilobytes, de la memoria de varias páginas utilizada. Acepta valores NULL. No se realiza un seguimiento de esta información para objetos de\<tipo USERSTORE_ * > y estos valores serán null.|  
|**entries_count**|**BIGINT**|Indica el número de entradas que hay en la memoria caché. No admite valores NULL.|  
|**entries_in_use_count**|**BIGINT**|Indica el número de entradas que hay en la memoria caché que se está usando. No admite valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos 

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

## <a name="see-also"></a>Consulte también  
  [SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


