---
title: Sys.dm_hadr_database_replica_cluster_states (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_replica_cluster_states
- dm_hadr_database_replica_cluster_states_TSQL
- sys.dm_hadr_database_replica_cluster_states_TSQL
- dm_hadr_database_replica_cluster_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_database_replica_cluster_states dynamic management view
ms.assetid: 6f719071-ebce-470d-aebd-1f55ee8cd70a
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de2182087dce5d924fba15b2000a860c25a1c47f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmhadrdatabasereplicaclusterstates-transact-sql"></a>sys.dm_hadr_database_replica_cluster_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila que contiene información diseñada para proporcionarle una visión general del estado de las bases de datos de disponibilidad en los grupos de disponibilidad AlwaysOn en cada grupo de disponibilidad AlwaysOn en el clúster de clústeres de conmutación por error de servidor de Windows (WSFC). Consulta **sys.dm_hadr_database_replica_states** responder a las preguntas siguientes:  
  
-   ¿Están todas las bases de datos de un grupo de disponibilidad listas para una conmutación por error?  
  
-   Después de una conmutación por error forzada, ¿se ha suspendido localmente una base de datos secundaria y se ha confirmado su estado suspendido en la nueva réplica principal?  
  
-   Si la réplica principal no está disponible actualmente, ¿qué réplica secundaria permitiría una pérdida de datos mínima si se convierte en la réplica principal?  
  
-   Cuando el valor de la [sys.databases](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)**log_reuse_wait_desc** columna es "availability_replica", ¿qué réplica secundaria en un grupo de disponibilidad soporta el truncamiento del registro en una base de datos principal ?  
   
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Identificador de la réplica de disponibilidad dentro del grupo de disponibilidad.|  
|**group_database_id**|**uniqueidentifier**|Identificador de la base de datos dentro del grupo de disponibilidad. Este identificador es idéntico en cada réplica al que está unido esta base de datos.|  
|**database_name**|**sysname**|Nombre de la base de datos que pertenece al grupo de disponibilidad.|  
|**is_failover_ready**|**bit**|Indica si la base de datos secundaria está sincronizada con la base de datos principal correspondiente. uno de:<br /><br /> 0 = La base de datos no está marcada como sincronizada en el clúster. La base de datos no está lista para una conmutación por error.<br /><br /> 1 = La base de datos está marcada como sincronizada en el clúster. La base de datos está lista para una conmutación por error.|  
|**is_pending_secondary_suspend**|**bit**|Indica si, después de una conmutación por error forzada, la base de datos está pendiente de suspensión pendiente; puede ser uno de los siguientes:<br /><br /> 0 = Cualquier estado a excepción de HADR_SYNCHRONIZED_ SUSPENDED.<br /><br /> 1 = HADR_SYNCHRONIZED_ SUSPENDED. Cuando una conmutación por error forzada se completa, cada una de las bases de datos secundarias se establece en HADR_SYNCHONIZED_SUSPENDED y permanece en este estado hasta que la nueva réplica principal recibe confirmación de esa base de datos secundaria en el mensaje SUSPEND.<br /><br /> NULL = Desconocido (sin quórum)|  
|**is_database_joined**|**bit**|Indica si la base de datos de esta réplica de disponibilidad se ha unido al grupo de disponibilidad; puede ser uno de los siguientes:<br /><br /> 0 = La base de datos no se ha unido al grupo de disponibilidad en esta réplica de disponibilidad.<br /><br /> 1 = La base de datos se ha unido al grupo de disponibilidad en esta réplica de disponibilidad.<br /><br /> NULL = Desconocido (la réplica de disponibilidad no tiene quórum).|  
|**recovery_lsn**|**numeric(25,0)**|En la réplica principal, el final del registro de transacciones antes de que la réplica escriba nuevas entradas de registro después de la recuperación o la conmutación por error. En la réplica principal, la fila de una base de datos secundaria dada tendrá el valor que la réplica principal necesita para la sincronización con la réplica secundaria (es decir, para la reversión y la reinicialización).<br /><br /> En las réplicas secundarias este valor es NULL. Tenga en cuenta que cada réplica secundaria tendrá el valor MAX o un valor inferior al que la réplica principal ha notificado a la réplica secundaria que se va a volver.|  
|**truncation_lsn**|**numeric(25,0)**|El valor de truncamiento de registro de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], que puede ser más alto que el LSN de truncamiento local si el truncamiento de registro local está bloqueado (como mediante una operación de copia de seguridad).|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Supervisar grupos de disponibilidad & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Sys.dm_hadr_database_replica_states & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
  
