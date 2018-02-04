---
title: Sys.elastic_pool_resource_stats (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 09/30/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- Azure SQL Database
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7af69bdd1f98560d3a6ae9699551b4f3062f68c6
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>sys.elastic_pool_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve estadísticas de uso de recursos para todos los grupos de servidor de base de datos elástica en un servidor lógico. Para cada grupo elástico de base de datos, hay una fila para cada 15 segundos reporting ventana (cuatro filas por minuto). Esto incluye el uso de CPU, E/S, registro, consumo de almacenamiento y solicitud/sesiones simultáneas todas las bases de datos en el grupo. Estos datos se conservan durante 14 días. 
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|Hora UTC que indica el inicio del segundo 15 intervalo de informes.|  
|**end_time**|**datetime2**|Hora UTC que indica el final de la segunda 15 intervalo de informes.|  
|**elastic_pool_name**|**nvarchar(128)**|Nombre del grupo elástico de base de datos.|  
|**avg_cpu_percent**|**decimal(5,2)**|Uso de proceso promedio en porcentaje del límite del grupo.|  
|**avg_data_io_percent**|**decimal(5,2)**|Uso promedio de E/S en porcentaje basado en el límite del grupo.|  
|**avg_log_write_percent**|**decimal(5,2)**|Utilización de recursos de escritura promedio en porcentaje del límite del grupo.|  
|**avg_storage_percent**|**decimal(5,2)**|Promedio de utilización del almacenamiento en porcentaje del límite del grupo de almacenamiento.|  
|**max_worker_percent**|**decimal(5,2)**|Máximos simultáneos trabajadores (solicitudes) de porcentaje se basa en el límite del grupo.|  
|**max_session_percent**|**decimal(5,2)**|Número máximo de sesiones simultáneo de porcentaje se basa en el límite del grupo.|  
|**elastic_pool_dtu_limit**|**int**|Máximo de grupo elástico DTU configuración actual para este grupo elástico durante este intervalo.|  
|**elastic_pool_storage_limit_mb**|**bigint**|Límite de almacenamiento máximo del grupo elástico actual configuración para este grupo elástico en megabytes durante este intervalo.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista existe en la base de datos maestra del servidor lógico. Debe estar conectado a la base de datos maestra para consultar **sys.elastic_pool_resource_stats**.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **dbmanager** rol.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los datos de uso de recursos ordenados por la hora más reciente para todos los grupos de servidor de base de datos elástica en el servidor lógico actual.  
  
```  
SELECT * FROM sys.elastic_pool_resource_stats   
ORDER BY end_time DESC;  
```  
  
 En el ejemplo siguiente se calcula el promedio porcentaje de consumo de DTU para un grupo dado.  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.elastic_pool_resource_stats   
WHERE elastic_pool_name = '<your pool name>'   
ORDER BY end_time DESC;  
```  
  
## <a name="see-also"></a>Vea también  
 [Dominar drástico crecimiento con bases de datos elásticas](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [Crear y administrar un grupo de base de datos elástica de base de datos SQL (vista previa)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
