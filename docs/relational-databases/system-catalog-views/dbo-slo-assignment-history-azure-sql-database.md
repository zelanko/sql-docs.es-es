---
title: dbo.slo_assignment_history (base de datos de SQL Azure) | Documentos de Microsoft
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
- dbo.slo_assignment_history
- slo_assignment_history
- slo_assignment_history_TSQL
- dbo.slo_assignment_history_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
ms.assetid: 048a6fb5-2fc2-4d12-a436-4c53ecd413f3
caps.latest.revision: "9"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fcff1c5141e6556f8cb4184284769e3be537f80a
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="dbosloassignmenthistory-azure-sql-database"></a>dbo.slo_assignment_history (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **Esto se aplica solo a [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.**  
>   
>  Esta característica se encuentra en un estado de vista previa. No dependa de la implementación específica de esta característica, ya que podría modificarse o quitarse en una versión futura.  
  
 Devuelve el historial de asignaciones de SLO (objetivo de nivel de servicio) de la base de datos en el servidor, que incluye lo siguiente:  
  
-   El historial de asignaciones SLO de la base de datos en el servidor.  
  
-   La hora de inicio y de finalización de cada solicitud de cambio de SLO de la base de datos.  
  
-   Los errores de asignaciones de SLO que se registran en las columnas error_code y error_desc.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|Nombre de la base de datos.|  
|database_id|**int**|Identificador de la base de datos.|  
|create_date|**datetimeoffset(7)**|Fecha de creación de la base de datos.|  
|service_objective_name|**sysname**|Nombre del SLO (objetivo de nivel de servicio).|  
|service_objective_id|**uniqueidentifier**|Identificador del SLO.|  
|operation_id|**uniqueidentifier**|Identificador de la operación.|  
|operation_start_time|**datetimeoffset(7)**|Hora de inicio de la solicitud de cambio de SLO de la base de datos.|  
|operation_end_time|**datetimeoffset(7)**|Hora de finalización de la solicitud de cambio de SLO de la base de datos.|  
|error_code|**int**|Código de error de la solicitud de cambio de SLO de la base de datos.|  
|error_desc|**nvarchar**|Descripción del error de la solicitud de cambio de SLO de la base de datos.|  
  
## <a name="permissions"></a>Permissions  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a virtual **maestro** base de datos.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el historial de asignaciones de SLO de la base de datos para la base de datos especificada.  
  
```  
SELECT *  
FROM dbo.slo_assignment_history   
WHERE database_name = '<DB NAME>’   
ORDER BY operation_start_time DESC;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Administración de bases de datos Premium](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
