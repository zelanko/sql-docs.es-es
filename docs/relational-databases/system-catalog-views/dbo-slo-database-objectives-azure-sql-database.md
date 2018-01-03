---
title: dbo.slo_database_objectives (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.slo_database_objectives
- dbo.slo_database_objectives_TSQL
- slo_database_objectives_TSQL
- slo_database_objectives
dev_langs: TSQL
helpviewer_keywords:
- slo_database_objectives
- dbo.slo_database_objectives
ms.assetid: a522569d-8cfc-4643-a170-1cd291e61eee
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6210e47a8178cf8f6f0f5a3aa50a6541010eb492
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="dboslodatabaseobjectives-azure-sql-database"></a>dbo.slo_database_objectives (base de datos de SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **Esto se aplica solo a [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.**  
>   
>  Para [! INCLUIR[ssSDSfull](../system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) (en master) para la operación ALTER DATABASE.   
  
 Devuelve el estado de asignación de un Objetivo de nivel de servicio (SLO) de una SQL Database.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|Nombre de la base de datos.|  
|current_slo|**sysname**|SLO actual de la base de datos.|  
|target_slo|**sysname**|SLO de destino de la base de datos según se especifica en la solicitud de cambio de SLO.|  
|state_desc|**nvarchar**|Estado de la solicitud de cambio de SLO: completado o pendiente.|  
  
## <a name="permissions"></a>Permissions  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a virtual **maestro** base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
```  
SELECT   
database_name=database_name.name   
    , current_slo=current_slo.name   
    , target_slo=target_slo.name   
    , state_desc=database_slo.state_desc   
FROM slo_database_objectives AS database_slo  
INNER JOIN slo_service_objectives AS current_slo ON database_slo.current_objective_id = current_slo.objective_id  
INNER JOIN slo_service_objectives AS target_slo ON database_slo.configured_objective_id = target_slo.objective_id  
INNER JOIN sys.databases AS database_name  ON database_slo.database_id = database_name.database_id;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Administración de bases de datos Premium](http://go.microsoft.com/fwlink/?LinkID=311927)  
[sys.dm_operation_status (Azure SQL Database)](../system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 
