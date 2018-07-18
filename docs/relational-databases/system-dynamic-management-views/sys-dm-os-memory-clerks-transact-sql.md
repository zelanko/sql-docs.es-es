---
title: Sys.dm_os_memory_clerks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_memory_clerks
- sys.dm_os_memory_clerks
- dm_os_memory_clerks_TSQL
- sys.dm_os_memory_clerks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_clerks dynamic management view
ms.assetid: 1d556c67-5c12-46d5-aa8c-7ec1bb858df7
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 00fad2477b9dd6bd25f998d3d741bcb63c364d05
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052363"
---
# <a name="sysdmosmemoryclerks-transact-sql"></a>sys.dm_os_memory_clerks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el conjunto de todos los distribuidores de memoria activos actualmente en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_memory_clerks**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**memory_clerk_address**|**varbinary (8)**|Especifica la dirección de memoria exclusiva del distribuidor de memoria. Es la columna de clave principal. No admite valores NULL.|  
|**Tipo**|**nvarchar(60)**|Especifica el tipo de distribuidor de memoria. Cada distribuidor tiene un tipo específico, como MEMORYCLERK_SQLCLR de distribuidores de CLR. No admite valores NULL.|  
|**Nombre**|**nvarchar(256)**|Especifica el nombre asignado internamente de este distribuidor de memoria. Un componente puede tener varios distribuidores de memoria de un tipo específico. Un componente puede optar por usar nombres específicos para identificar distribuidores de memoria del mismo tipo. No admite valores NULL.|  
|**memory_node_id**|**smallint**|Especifica el identificador del nodo de memoria. No acepta valores NULL.|  
|**single_pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].|  
|**pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica la cantidad de memoria de página asignada en kilobytes (KB) para este distribuidor de memoria. No admite valores NULL.|  
|**multi_pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Cantidad de memoria de páginas múltiples asignada en KB. Es la cantidad de memoria asignada mediante el asignador de páginas múltiples de los nodos de memoria. Esta memoria se asigna fuera del grupo de búferes y aprovecha las ventajas del asignador virtual de los nodos de memoria. No admite valores NULL.|  
|**virtual_memory_reserved_kb**|**bigint**|Especifica la cantidad de memoria virtual reservada por un distribuidor de memoria. No admite valores NULL.|  
|**virtual_memory_committed_kb**|**bigint**|Especifica la cantidad de memoria virtual confirmada por un distribuidor de memoria. La cantidad de memoria confirmada debe ser siempre menor que la cantidad de memoria reservada. No admite valores NULL.|  
|**awe_allocated_kb**|**bigint**|Especifica la cantidad de memoria en kilobytes (KB) bloqueada en la memoria física y no transferida por el sistema operativo. No admite valores NULL.|  
|**shared_memory_reserved_kb**|**bigint**|Especifica la cantidad de memoria compartida reservada por un distribuidor de memoria. Es la cantidad de memoria reservada que van a utilizar la memoria compartida y la asignación de archivos. No admite valores NULL.|  
|**shared_memory_committed_kb**|**bigint**|Especifica la cantidad de memoria compartida confirmada por el distribuidor de memoria. No admite valores NULL.|  
|**page_size_in_bytes**|**bigint**|Especifica la granularidad de la asignación de páginas para este distribuidor de memoria. No admite valores NULL.|  
|**page_allocator_address**|**varbinary (8)**|Especifica la dirección del asignador de páginas. Esta dirección es única para un distribuidor de memoria y se pueden usar en **sys.dm_os_memory_objects** para buscar objetos de memoria que están enlazados a este distribuidor. No admite valores NULL.|  
|**host_address**|**varbinary (8)**|Especifica la dirección de memoria del host para este distribuidor de memoria. Para obtener más información, consulte [sys.dm_os_hosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md). Los componentes, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, acceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los recursos de memoria a través de la interfaz del host.<br /><br /> 0x00000000 = El distribuidor de memoria pertenece a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> No admite valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos 

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="remarks"></a>Notas  
 El administrador de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consta de una jerarquía de tres capas. En la parte inferior de la jerarquía están los nodos de memoria. El nivel intermedio incluye los distribuidores de memoria, los almacenamientos en caché de la memoria y los bloques de memoria. La capa superior incluye los objetos de memoria. Normalmente, estos objetos se utilizan para asignar memoria en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los nodos de memoria proporcionan la interfaz y la implementación de los asignadores de nivel inferior. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], solo los distribuidores de memoria tienen acceso a nodos de memoria. Los distribuidores de memoria tienen acceso a interfaces de nodos de memoria para asignar memoria. Los nodos de memoria también realizan el seguimiento de la memoria asignada utilizando el distribuidor para diagnósticos. Cada componente que asigna una cantidad de memoria importante debe crear su propio distribuidor de memoria y asignar toda su memoria utilizando las interfaces del distribuidor. Con frecuencia, los componentes crean sus distribuidores correspondientes cuando se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  

 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
  
  


