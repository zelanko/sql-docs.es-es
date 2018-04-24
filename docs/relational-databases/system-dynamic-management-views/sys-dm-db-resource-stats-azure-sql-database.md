---
title: Sys.dm_db_resource_stats (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: bc673459f43662036b4918585a946ef515d7cc95
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.dm_db_resource_stats (base de datos SQL de Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve el consumo de CPU, E/S y memoria para un [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] base de datos. Hay una fila para cada 15 segundos, incluso si no hay ninguna actividad en la base de datos. Los datos históricos se conservan durante una hora.  
  
|Columnas|Tipo de datos|Description|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|Hora UTC que indica el fin del intervalo de informes actual.|  
|avg_cpu_percent|**decimal (5,2)**|Uso de proceso promedio como porcentaje del límite del nivel de servicio.|  
|avg_data_io_percent|**decimal (5,2)**|Promedio de datos de utilización de E/S en porcentaje del límite del nivel de servicio.|  
|avg_log_write_percent|**decimal (5,2)**|Uso de recursos de escritura promedio como porcentaje del límite del nivel de servicio.|  
|avg_memory_usage_percent|**decimal (5,2)**|Uso de memoria promedio como porcentaje del límite del nivel de servicio.<br /><br /> Esto incluye la memoria utilizada para el almacenamiento de objetos de OLTP en memoria.|  
|xtp_storage_percent|**decimal (5,2)**|Uso de almacenamiento para OLTP en memoria como un porcentaje del límite del nivel de servicio (al final del intervalo de informes). Esto incluye la memoria utilizada para el almacenamiento de los siguientes objetos de OLTP en memoria: tablas optimizadas en memoria, índices y las variables de tabla. También incluye la memoria utilizada para procesar las operaciones de ALTER TABLE.<br /><br /> Devuelve 0 si no se utiliza OLTP en memoria en la base de datos.|  
|max_worker_percent|**decimal (5,2)**|Máximos simultáneos trabajadores (solicitudes) como un porcentaje del límite de nivel de servicio de la base de datos.|  
|max_session_percent|**decimal (5,2)**|Número máximo de sesiones simultáneo en porcentaje del límite de nivel de servicio de la base de datos.|  
|dtu_limit|**int**|Base de datos max DTU configuración actual de esta base de datos durante este intervalo. |
|||
  
> [!TIP]  
>  Para obtener más contexto sobre estos límites y los niveles de servicio, vea los temas [niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) y [límites y capacidades de nivel de servicio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/).  
  
## <a name="permissions"></a>Permissions  
 Esta vista necesita el permiso VIEW DATABASE STATE.  
  
## <a name="remarks"></a>Comentarios  
 Los datos devueltos por **sys.dm_db_resource_stats** se expresa como un porcentaje del máximo permitido de límites para el nivel / rendimiento de nivel de servicio que se está ejecutando.
 
 Si la base de datos se conmutó por error a otro servidor en los últimos 60 minutos, la vista solo devolverá datos correspondientes al tiempo que ha sido la base de datos principal desde la conmutación por error.  
  
 Para obtener una vista menos detallada de estos datos, use **sys.resource_stats** vista de catálogo el **maestro** base de datos. Esta vista captura datos cada 5 minutos y mantiene datos históricos durante 14 días.  Para obtener más información, consulte [sys.resource_stats &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md).  
  
 Cuando una base de datos es un miembro de un grupo elástico, las estadísticas de recursos que se presentan como valores de porcentaje se expresan como el porcentaje del límite máximo de las bases de datos como se establece en la configuración del grupo elástico.  
  
## <a name="example"></a>Ejemplo  
  
El ejemplo siguiente devuelve los datos del uso de recursos ordenados por la hora más reciente de la base de datos conectada actualmente.  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 En el ejemplo siguiente se identifica el promedio de consumo de DTU en términos de porcentaje del límite máximo permitido de DTU en el nivel de rendimiento de la base de datos de usuario durante la última hora. Considere aumentar el nivel de rendimiento de estos porcentajes a casi el 100 % de forma coherente.  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 El ejemplo siguiente devuelve los valores máximo y promedio de porcentaje de CPU, la E/S de datos y registro, así como el consumo de memoria durante la última hora.  
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.resource_stats &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Límites y capacidades de nivel de servicio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
