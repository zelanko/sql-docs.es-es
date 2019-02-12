---
title: Sys.elastic_pool_resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d7fff3c65aaf6a5670be2d457440f4384f7c5fdd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011996"
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>Sys.elastic_pool_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve estadísticas de uso de recursos para todos los grupos elásticos en un servidor de base de datos SQL. Para cada grupo elástico, hay una fila para cada 15 segundos (cuatro filas por minuto) de la ventana de informe. Esto incluye el uso de CPU, E/S, registro, consumo de almacenamiento y simultáneas de solicitudes o sesiones todas las bases de datos en el grupo. Estos datos se conservan durante 14 días. 
  
||  
|-|  
|**Se aplica a**:  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|Hora de UTC que indica el inicio del segundo intervalo de informes 15.|  
|**end_time**|**datetime2**|Hora de UTC que indica el final del segundo intervalo de informes 15.|  
|**elastic_pool_name**|**nvarchar(128)**|Nombre del grupo de bases de datos elásticas.|  
|**avg_cpu_percent**|**decimal(5,2)**|Uso de proceso medio en porcentaje del límite del grupo.|  
|**avg_data_io_percent**|**decimal(5,2)**|Uso de E/S medio en porcentaje basado en el límite del grupo.|  
|**avg_log_write_percent**|**decimal(5,2)**|Promedio de escritura utilización de recursos en porcentaje del límite del grupo.|  
|**avg_storage_percent**|**decimal(5,2)**|Promedio de utilización del almacenamiento en porcentaje del límite del grupo de almacenamiento.|  
|**max_worker_percent**|**decimal(5,2)**|Máximo de trabajos simultáneos (solicitudes) en porcentaje basado en el límite del grupo.|  
|**max_session_percent**|**decimal(5,2)**|Número máximo de sesiones simultáneo en porcentaje basado en el límite del grupo.|  
|**elastic_pool_dtu_limit**|**int**|Máximo de grupo elástico DTU configuración actual de este grupo elástico durante este intervalo.|  
|**elastic_pool_storage_limit_mb**|**bigint**|Límite de almacenamiento máximo del grupo elástico actual configuración para este grupo elástico en megabytes durante este intervalo.|
|**avg_allocated_storage_percent**|**decimal(5,2)**|El porcentaje de espacio de datos asignado todas las bases de datos en el grupo elástico.  Esto es la proporción de espacio de datos asignado al tamaño máximo de datos para el grupo elástico.  Para obtener más información, vea: [Administración del espacio de archivo en la base de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>Comentarios

 Esta vista existe en la base de datos maestra del servidor de base de datos SQL. Debe estar conectado a la base de datos maestra para consultar **sys.elastic_pool_resource_stats**.  
  
## <a name="permissions"></a>Permisos

 Debe pertenecer a la **dbmanager** rol.  
  
## <a name="examples"></a>Ejemplos

 El ejemplo siguiente devuelve los datos de utilización de recursos ordenados por la hora más reciente de todos los grupos de bases de datos elásticas en el servidor de base de datos SQL actual.  
  
```sql
SELECT * FROM sys.elastic_pool_resource_stats
ORDER BY end_time DESC;  
```

 El ejemplo siguiente calcula el consumo medio de porcentaje DTU para un grupo determinado.  

```sql
SELECT start_time, end_time,
  (SELECT Max(v)
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]
FROM sys.elastic_pool_resource_stats
WHERE elastic_pool_name = '<your pool name>'
ORDER BY end_time DESC;  
```

## <a name="see-also"></a>Vea también

 [Control del crecimiento explosivo con bases de datos elásticas](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [Crear y administrar un grupo de bases de datos elásticas de SQL Database (versión preliminar)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [Sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
