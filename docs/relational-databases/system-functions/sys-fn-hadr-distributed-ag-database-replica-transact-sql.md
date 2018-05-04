---
title: Sys.fn_hadr_distributed_ag_database_replica (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/14/2016
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
- sys.fn_hadr_distributed_ag_database_replica
- sys.fn_hadr_distributed_ag_database_replica_TSQL
- fn_hadr_distributed_ag_database_replica
- fn_hadr_distributed_ag_database_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_database_replica
ms.assetid: 0e6202a1-e872-4f53-99d7-c16b6f712efc
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3166e1c46db60d2a5d7b97753c6fc5ce0ae5cc2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnhadrdistributedagdatabasereplica-transact-sql"></a>sys.fn_hadr_distributed_ag_database_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Se usa para asignar una base de datos en un grupo de disponibilidad distribuido a la base de datos del grupo de disponibilidad local.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_hadr_distributed_ag_database_replica( lag_Id, database_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*lag_Id*'  
 Es el identificador del grupo de disponibilidad distribuidos. *lag_Id* es de tipo **uniqueidentifier**.  
  
 '*database_id*'  
 Es el identificador de la base de datos en un grupo de disponibilidad distribuido. *database_id* es de tipo **uniqueidentifier**.  
  
## <a name="tables-returned"></a>Tablas devueltas  
 Devuelve la siguiente información.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**group_database_id**|**uniqueidentifier**|Id. de la base de datos del grupo de disponibilidad local.|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="using-sysfnhadrdistributedagdatabasereplica"></a>Usar sys.fn_hadr_distributed_ag_database_replica  
 En el ejemplo siguiente se pasa en el Id. de base de datos en un grupo de disponibilidad distribuido. Devuelve una tabla con el Id. de base de datos asociado con el grupo de disponibilidad local.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @databaseId uniqueidentifier = '3FFA882A-C4C3-5B9E-A203-8F44BD9659F7'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_database_replica(@lagId, @databaseId)  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Distribuye los grupos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)   
 [Crear grupo de disponibilidad & #40; Transact-SQL & #41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP & #40; Transact-SQL & #41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
