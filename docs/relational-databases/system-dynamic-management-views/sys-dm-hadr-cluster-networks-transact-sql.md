---
title: Sys.dm_hadr_cluster_networks (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b02faa8108154ae4efba474a01dac8edf5610ea6
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466152"
---
# <a name="sysdmhadrclusternetworks-transact-sql"></a>sys.dm_hadr_cluster_networks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada miembro del clúster de WSFC que participa en la configuración de subred de un grupo de disponibilidad. Puede utilizar esta vista de administración dinámica para validar la dirección IP virtual de red configurada para cada réplica de disponibilidad.  
  
 Clave principal: **member_name** + **network_subnet_IP** + **network_subnet_prefix_length**  
  
 > [!TIP]
 > A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], esta vista de administración dinámica admite siempre en Failover Cluster Instances además de grupos de disponibilidad AlwaysOn.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**MEMBER_NAME**|**nvarchar(128)**|Un nombre de equipo de un nodo del clúster de WSFC.|  
|**network_subnet_ip**|**nvarchar(48)**|Dirección de IP de red de la subred a la que pertenece el equipo. Puede ser una dirección IPv4 o IPv6.|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|Máscara de subred de red que especifica la subred a la que pertenece la dirección IP. **network_subnet_ipv4_mask** para especificar las opciones de DHCP < network_subnet_option > en una cláusula WITH DHCP de la [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) o [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.<br /><br /> NULL = subred IPv6.|  
||||  
|**network_subnet_prefix_length**|**int**|Longitud de prefijo de IP de red que especifica la subred a la que pertenece el equipo.|  
|**is_public**|**bit**|Si la red es privada o pública en el clúster de WSFC, puede ser:<br /><br /> 0 = Privada<br /><br /> 1 = Pública|  
|**is_ipv4**|**bit**|Tipo de la subred; puede ser:<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Clústeres de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Supervisar grupos de disponibilidad & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [Consultar el catálogo de sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
