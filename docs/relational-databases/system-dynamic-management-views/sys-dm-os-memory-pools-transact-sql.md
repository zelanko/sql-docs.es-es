---
title: Sys. dm_os_memory_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b9737e75142bf29b9a77602eb1bf4c912e60b255
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826729"
---
# <a name="sysdm_os_memory_pools-transact-sql"></a>sys.dm_os_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila para cada almacén de objetos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta vista se puede utilizar para supervisar el uso de la memoria caché e identificar el comportamiento del almacenamiento en caché incorrecto  
  
> [!NOTE]  
>  Para llamar a este método desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use el nombre **Sys. dm_pdw_nodes_os_memory_pools**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary(8**|Dirección de memoria de la entrada que representa el grupo de memoria. No admite valores NULL.|  
|**pool_id**|**int**|Id. de un grupo específico en un conjunto de grupos. No admite valores NULL.|  
|**type**|**nvarchar(60)**|Tipo de grupo de objetos. No admite valores NULL. Para obtener más información, vea [Sys. dm_os_memory_clerks &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**name**|**nvarchar(256)**|Nombre asignado por el sistema de este objeto de memoria. No admite valores NULL.|  
|**max_free_entries_count**|**bigint**|Nombre máximo de entradas libres que puede tener un grupo. No admite valores NULL.|  
|**free_entries_count**|**bigint**|Número de entradas libres en el grupo actualmente. No admite valores NULL.|  
|**removed_in_all_rounds_count**|**bigint**|Número de entradas quitadas del grupo desde que se inició la sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No admite valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiere el `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

## <a name="remarks"></a>Comentarios  
 Los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a veces utilizan un marco de grupos comunes para almacenar en caché tipos de datos homogéneos, sin estado. El marco de grupos es más sencillo que el marco de la caché. Todas las entradas en los grupos se consideran iguales. Internamente, los grupos son distribuidores de memoria y se pueden utilizar en lugares donde se utilizan distribuidores de memoria.  
  
## <a name="see-also"></a>Consulte también  
 
  [SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


