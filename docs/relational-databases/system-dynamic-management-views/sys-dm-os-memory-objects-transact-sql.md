---
title: Sys.dm_os_memory_objects (Transact-SQL) | Documentos de Microsoft
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
- dm_os_memory_objects
- sys.dm_os_memory_objects
- sys.dm_os_memory_objects_TSQL
- dm_os_memory_objects_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_memory_objects dynamic management view
ms.assetid: 5688bcf8-5da9-4ff9-960b-742b671d7096
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 92d9fc9b94f74a08f84c6f39307a4f88e48b847b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosmemoryobjects-transact-sql"></a>sys.dm_os_memory_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve los objetos de memoria asignados actualmente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede usar **sys.dm_os_memory_objects** para analizar el uso de memoria e identificar memoria posibles pérdidas.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary (8)**|Dirección del objeto de memoria. No admite valores NULL.|  
|**parent_address**|**varbinary (8)**|Dirección del objeto de memoria primario. Acepta valores NULL.|  
|**pages_allocated_count**|**int**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Número de páginas asignadas por este objeto. No admite valores NULL.|  
|**pages_in_bytes**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Cantidad de memoria en bytes que esta instancia del objeto de memoria asigna. No admite valores NULL.|  
|**creation_options**|**int**|Exclusivamente para uso interno. Acepta valores NULL.|  
|**bytes_used**|**bigint**|Exclusivamente para uso interno. Acepta valores NULL.|  
|**tipo**|**nvarchar (60)**|Tipo de objeto de memoria.<br /><br /> Indica algún componente al que pertenece este objeto de memoria, o la función del objeto de memoria. Acepta valores NULL.|  
|**Nombre**|**varchar (128)**|Exclusivamente para uso interno. Acepta valores NULL.|  
|**memory_node_id**|**smallint**|Identificador de un nodo de memoria que utiliza este objeto de memoria. No admite valores NULL.|  
|**creation_time**|**datetime**|Exclusivamente para uso interno. Acepta valores NULL.|  
|**max_pages_allocated_count**|**int**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Número máximo de páginas asignadas por este objeto de memoria. No admite valores NULL.|  
|**page_size_in_bytes**|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Tamaño de las páginas asignadas por este objeto, en bytes. No admite valores NULL.|  
|**max_pages_in_bytes**|**bigint**|Cantidad máxima de memoria que este objeto de memoria nunca usó. No admite valores NULL.|  
|**page_allocator_address**|**varbinary (8)**|Dirección de memoria del asignador de la página. No admite valores NULL. Para obtener más información, consulte [sys.dm_os_memory_clerks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**creation_stack_address**|**varbinary (8)**|Exclusivamente para uso interno. Acepta valores NULL.|  
|**sequence_num**|**int**|Exclusivamente para uso interno. Acepta valores NULL.|  
|**partition_type**|**int**|El tipo de partición:<br /><br /> 0 - no cargas objeto de memoria<br /><br /> 1 - objeto de memoria cargas, actualmente no tienen particionada<br /><br /> 2 - objeto de memoria cargas, particionado por nodo NUMA. En un entorno con un solo nodo NUMA Esto equivale a 1.<br /><br /> 3 - objeto de memoria cargas, dividida por CPU.|  
|**contention_factor**|**real**|Valor que especifica la contención en este objeto de memoria, con lo que significa que no hay contención de 0. El valor se actualiza cada vez que un número especificado de las asignaciones de memoria realizado reflejan contención durante ese período. Se aplica sólo a los objetos de memoria seguros para subprocesos.|  
|**waiting_tasks_count**|**bigint**|Número de esperas de este objeto de memoria. Este contador se incrementa cada vez que se asigna memoria de este objeto de memoria. El incremento es el número de tareas que esperan actualmente para el acceso a este objeto de memoria. Se aplica sólo a los objetos de memoria seguros para subprocesos. Esto es un valor de esfuerzo mejor sin una garantía de corrección.|  
|**exclusive_access_count**|**bigint**|Especifica la frecuencia en que este objeto de memoria accedió exclusivamente. Se aplica sólo a los objetos de memoria seguros para subprocesos.  Esto es un valor de esfuerzo mejor sin una garantía de corrección.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
 **partition_type**, **contention_factor**, **waiting_tasks_count**, y **exclusive_access_count** aún no están implementadas en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.  
  
## <a name="remarks"></a>Comentarios  
 Los objetos de memoria son montones. Proporcionan asignaciones con una granularidad más fina que las que proporcionan los distribuidores de memoria. Los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizan objetos de memoria en lugar de distribuidores de memoria. Los objetos de memoria utilizan la interfaz del asignador de la página del distribuidor de memoria para asignar páginas. Los objetos de memoria no utilizan interfaces de memoria virtual o compartida. Según los patrones de asignación, los componentes pueden crear diferentes tipos de objetos de memoria para asignar regiones de tamaño arbitrario.  
  
 El tamaño de página típico para un objeto de memoria es de 8 KB. No obstante, los objetos de memoria incrementales pueden tener tamaños de página que van desde 512 bytes hasta 8 KB.  
  
> [!NOTE]  
>  El tamaño de página no tiene una asignación máxima. En su lugar, el tamaño de página es la granularidad de la asignación que admite una asignador de la página y que se implementa mediante un distribuidor de memoria. Puede solicitar asignaciones mayores de 8 KB de los objetos de memoria.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve la cantidad de memoria asignada por cada tipo de objeto de memoria.  
  
```  
SELECT SUM (pages_in_bytes) as 'Bytes Used', type   
FROM sys.dm_os_memory_objects  
GROUP BY type   
ORDER BY 'Bytes Used' DESC;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
  [Sistema operativo SQL Server relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Sys.dm_os_memory_clerks &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


