---
description: sys.dm_hadr_availability_replica_cluster_states (Transact-SQL)
title: Sys. dm_hadr_availability_replica_cluster_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_replica_cluster_states_TSQL
- dm_hadr_availability_replica_cluster_states
- sys.dm_hadr_availability_replica_cluster_states
- dm_hadr_availability_replica_cluster_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_availability_replica_cluster_states dynamic management view
ms.assetid: 2e0dd780-6a71-4f4b-b7f7-6e063bec71d6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ea7242f1658f5a52ab5a403e186c1be319834825
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89533561"
---
# <a name="sysdm_hadr_availability_replica_cluster_states-transact-sql"></a>sys.dm_hadr_availability_replica_cluster_states (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve una fila para cada réplica de disponibilidad AlwaysOn (independientemente de su estado de unión) de todos los Grupos de disponibilidad AlwaysOn (con independencia de la ubicación de la réplica) del clúster del servicio de clústeres de conmutación por error de Windows Server (WSFC).  
  
##  <a name="connected_state"></a>  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Identificador único de la réplica de disponibilidad.|  
|**replica_server_name**|**nvarchar(256)**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la réplica.|  
|**group_id**|**uniqueidentifier**|Identificador único del grupo de disponibilidad.|  
|**join_state**|**tinyint**|0 = Sin unir<br /><br /> 1 = Unido, independiente<br /><br /> 2 = Instancia de clúster de conmutación por error unida|  
|**join_state_desc**|**nvarchar(60)**|NOT_JOINED<br /><br /> JOINED_STANDALONE<br /><br /> JOINED_FAILOVER_CLUSTER_INSTANCE|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
