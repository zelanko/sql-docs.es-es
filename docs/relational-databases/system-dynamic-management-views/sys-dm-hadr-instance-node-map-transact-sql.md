---
title: sys.dm_hadr_instance_node_map (Transact-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3e0b022996ab5b0f6de91773871fc7357c29e7f
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511392"
---
# <a name="sysdmhadrinstancenodemap-transact-sql"></a>sys.dm_hadr_instance_node_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda una réplica de disponibilidad que se une a su grupo de disponibilidad AlwaysOn, devuelve el nombre del nodo de clúster de conmutación por error de Windows Server (WSFC) que hospeda la instancia del servidor. Esta vista de administración dinámica tiene las siguientes aplicaciones:  
  
-   Esta vista de administración dinámica es útil para detectar un grupo de disponibilidad con varias réplicas de disponibilidad que se hospedan en el mismo nodo de WSFC, que es una configuración no admitida que puede producirse después de una conmutación por error de FCI si el grupo de disponibilidad está configurado incorrectamente. Para obtener más información, vea [Clúster de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).  
  
-   Cuando varias instancias de SQL Server se hospedan en el mismo nodo de WSFC, el archivo DLL de recursos utiliza esta vista de administración dinámica para determinar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se va a conectar.  
   
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**ag_resource_id**|**nvarchar(256)**|Identificador único del grupo de disponibilidad como un recurso en el WSFC.|  
|**instance_name**|**nvarchar(256)**|Nombre:*server*/*instancia*-de una instancia de servidor que hospeda una réplica del grupo de disponibilidad.|  
|**node_name**|**nvarchar(256)**|Nombre del nodo WSFC.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
