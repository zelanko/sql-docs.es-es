---
title: Sys.dm_os_dispatcher_pools (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs: TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 479e97ce3202d33fdf125f0c5978e2c1899ee0cd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosdispatcherpools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre los grupos de distribuidores de la sesión. Los grupos de distribuidores son grupos de subprocesos utilizados por componentes del sistema para realizar el procesamiento en segundo plano.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_dispatcher_pools**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary (8)**|Dirección del grupo de distribuidores. dispatcher_pool_address es único. No admite valores NULL.|  
|Tipo|**nvarchar(256)**|El tipo del grupo de distribuidores. No admite valores NULL. Hay dos tipos de grupos de distribuidores:<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> Consultar la DMV para obtener la lista completa|  
|name|**nvarchar(256)**|El nombre del grupo de distribuidores. No admite valores NULL.|  
|dispatcher_count|**int**|El número de subprocesos de distribución activos. No admite valores NULL.|  
|dispatcher_ideal_count|**int**|El número de subprocesos de distribución que el grupo de distribuidores puede incrementar. No admite valores NULL.|  
|dispatcher_timeout_ms|**int**|El tiempo, en milisegundos, que un distribuidor esperará el nuevo trabajo antes de salir. No admite valores NULL.|  
|dispatcher_waiting_count|**int**|El número de subprocesos de distribución inactivos. No admite valores NULL.|  
|queue_length|**int**|El número de elementos de trabajo que esperan a ser controlados por un grupo de distribuidores. No admite valores NULL.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   
  
## <a name="see-also"></a>Vea también  
  
  


