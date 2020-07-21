---
title: Sys. dm_hadr_instance_node_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sys.dm_hadr_instance_node_map_TSQL
- sys.sys.dm_hadr_instance_node_map
- sys.dm_hadr_instance_node_map_TSQL
- sys.dm_hadr_instance_node_map
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC
- sys.sys.dm_hadr_instance_node_map dynamic management view
ms.assetid: ccfaf62c-9f87-43cf-a5e7-8942e91dd041
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 32001d88c17358406b5b855cbb698c9d2686e40f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760252"
---
# <a name="sysdm_hadr_instance_node_map-transact-sql"></a>sys.dm_hadr_instance_node_map (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda una réplica de disponibilidad que está unida a su Always on grupo de disponibilidad, devuelve el nombre del nodo de clúster de conmutación por error de Windows Server (WSFC) que hospeda la instancia de servidor. Esta vista de administración dinámica tiene las siguientes aplicaciones:  
  
-   Esta vista de administración dinámica es útil para detectar un grupo de disponibilidad con varias réplicas de disponibilidad que se hospedan en el mismo nodo de WSFC, que es una configuración no admitida que puede producirse después de una conmutación por error de FCI si el grupo de disponibilidad está configurado incorrectamente. Para obtener más información, vea [Clúster de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).  
  
-   Cuando varias instancias de SQL Server se hospedan en el mismo nodo de WSFC, el archivo DLL de recursos utiliza esta vista de administración dinámica para determinar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se va a conectar.  
   
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**ag_resource_id**|**nvarchar(256)**|IDENTIFICADOR único del grupo de disponibilidad como un recurso en el WSFC.|  
|**instance_name**|**nvarchar(256)**|Nombre:*server* / *instancia*del servidor-de una instancia del servidor que hospeda una réplica para el grupo de disponibilidad.|  
|**node_name**|**nvarchar(256)**|Nombre del nodo de WSFC.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Always On vistas y funciones de administración dinámica de grupos de disponibilidad &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On vistas de catálogo de grupos de disponibilidad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
