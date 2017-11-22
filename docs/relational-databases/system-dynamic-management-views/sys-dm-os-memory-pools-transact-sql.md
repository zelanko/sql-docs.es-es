---
title: Sys.dm_os_memory_pools (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e0e649688167c772defa308172f3b8a633ab6b7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosmemorypools-transact-sql"></a>sys.dm_os_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila para cada almacén de objetos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta vista se puede utilizar para supervisar el uso de la memoria caché e identificar el comportamiento del almacenamiento en caché incorrecto  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_memory_pools**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary (8)**|Dirección de memoria de la entrada que representa el grupo de memoria. No admite valores NULL.|  
|**pool_id**|**int**|Id. de un grupo específico en un conjunto de grupos. No admite valores NULL.|  
|**tipo**|**nvarchar (60)**|Tipo de grupo de objetos. No admite valores NULL. Para obtener más información, consulte [sys.dm_os_memory_clerks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**Nombre**|**nvarchar(256)**|Nombre asignado por el sistema de este objeto de memoria. No admite valores NULL.|  
|**max_free_entries_count**|**bigint**|Nombre máximo de entradas libres que puede tener un grupo. No admite valores NULL.|  
|**free_entries_count**|**bigint**|Número de entradas libres en el grupo actualmente. No admite valores NULL.|  
|**removed_in_all_rounds_count**|**bigint**|Número de entradas quitadas del grupo desde que se inició la sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No admite valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.  
  
## <a name="remarks"></a>Comentarios  
 Los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a veces utilizan un marco de grupos comunes para almacenar en caché tipos de datos homogéneos, sin estado. El marco de grupos es más sencillo que el marco de la caché. Todas las entradas en los grupos se consideran iguales. Internamente, los grupos son distribuidores de memoria y se pueden utilizar en lugares donde se utilizan distribuidores de memoria.  
  
## <a name="see-also"></a>Vea también  
 
  [Sistema operativo SQL Server relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


