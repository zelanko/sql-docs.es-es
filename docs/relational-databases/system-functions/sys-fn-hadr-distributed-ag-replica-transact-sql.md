---
title: Sys.fn_hadr_distributed_ag_replica (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_replica
- sys.fn_hadr_distributed_ag_replica_TSQL
- fn_hadr_distributed_ag_replica
- fn_hadr_distributed_ag_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_replica
ms.assetid: a1e5f9cb-c350-4bb4-a04f-7394f6f25d62
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 780fb8e20efd3b8d40ed88c2382cbfdc01852b05
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysfnhadrdistributedagreplica-transact-sql"></a>sys.fn_hadr_distributed_ag_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Se utiliza para asignar una réplica en un grupo de disponibilidad distribuido al grupo de disponibilidad local.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_hadr_distributed_ag_replica( lag_Id, replica_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*lag_Id*'  
 Es el identificador del grupo de disponibilidad distribuidos. *lag_Id* es de tipo **uniqueidentifier**.  
  
 '*replica_id*'  
 Es el identificador de una réplica del grupo de disponibilidad distribuidos. *replica_id* es de tipo **uniqueidentifier**.  
  
## <a name="tables-returned"></a>Tablas devueltas  
 Devuelve la siguiente información.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador único (GUID) del grupo de disponibilidad local.|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="using-sysfnhadrdistributedagreplica"></a>Usar sys.fn_hadr_distributed_ag_replica  
 En el ejemplo siguiente se devuelve una tabla con el identificador del grupo de disponibilidad local que está asociado a la réplica y los grupos de disponibilidad distribuido especificado.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @replicaId uniqueidentifier = 'D5517513-04A8-FD82-14C6-E684EC913935'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_replica(@lagId, @replicaId)  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn & #40; SQL Server & #41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Distribuye los grupos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)  
 [Crear grupo de disponibilidad & #40; Transact-SQL & #41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP & #40; Transact-SQL & #41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
