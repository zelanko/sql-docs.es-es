---
title: Sys.dm_db_resource_stats (base de datos de SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.service: sql-database
ms.reviewer: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 3ca0aa09718d8310ccb6ba304d8cc5595d8c5299
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993889"
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.dm_db_resource_stats (base de datos SQL de Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve el consumo de CPU, E/S y memoria para una base de datos [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Hay una fila para cada 15 segundos, incluso si no hay ninguna actividad en la base de datos. Los datos históricos se conservan durante una hora.  
  
|Columnas|Tipo de datos|Descripción|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|Hora UTC que indica el fin del intervalo de informes actual.|  
|avg_cpu_percent|**decimal (5,2)**|Uso de proceso promedio como porcentaje del límite del nivel de servicio.|  
|avg_data_io_percent|**decimal (5,2)**|Promedio de datos de uso de E/S en porcentaje del límite del nivel de servicio.|  
|avg_log_write_percent|**decimal (5,2)**|Uso de rendimiento de E/S como porcentaje del límite del nivel de servicio de escritura promedio.|  
|avg_memory_usage_percent|**decimal (5,2)**|Uso de memoria promedio como porcentaje del límite del nivel de servicio.<br /><br /> Esto incluye la memoria usada para las páginas del grupo de búferes y el almacenamiento de objetos de OLTP en memoria.|  
|xtp_storage_percent|**decimal (5,2)**|Utilización del almacenamiento de OLTP en memoria en porcentaje del límite del nivel de servicio (al final del intervalo de informes). Esto incluye la memoria utilizada para el almacenamiento de los siguientes objetos de OLTP en memoria: las tablas optimizadas para memoria, índices y las variables de tabla. También incluye la memoria usada para procesar las operaciones ALTER TABLE.<br /><br /> Devuelve 0 si no se utiliza OLTP en memoria en la base de datos.|  
|max_worker_percent|**decimal (5,2)**|Máximo de trabajos simultáneos (solicitudes) en porcentaje del límite del nivel de servicio de la base de datos.|  
|max_session_percent|**decimal (5,2)**|Número máximo de sesiones simultáneo en porcentaje del límite del nivel de servicio de la base de datos.|  
|dtu_limit|**int**|Base de datos max DTU configuración actual de esta base de datos durante este intervalo. Para las bases de datos mediante el modelo basado en núcleos virtuales, esta columna es NULL.|
|cpu_limit|**decimal (5,2)**|Número de núcleos virtuales para esta base de datos durante este intervalo. Para las bases de datos mediante el modelo basado en DTU, esta columna es NULL.|
|avg_instance_cpu_percent|**decimal (5,2)**|Base de datos promedio de uso de CPU en porcentaje.|
|avg_instance_memory_percent|**decimal (5,2)**|Promedio de uso de memoria de base de datos en porcentaje.|
|avg_login_rate_percent|**decimal (5,2)**|Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.|
|replica_role|**int**|Representa la función de la réplica actual con 0 como principal, 1 como base de datos secundaria y 2 como reenviador (principal de geo-secondary). Verá "1" cuando se conecta con la intención de solo lectura a todas las réplicas secundarias legibles. Si se conecta a geo-secondary sin especificar la intención de solo lectura, debería ver "2" (conexión con el reenviador).|
|||
  
> [!TIP]  
>  Para obtener más contexto sobre estos límites y los niveles de servicio, vea los temas [niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) y [límites y capacidades de nivel de servicio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/).  
  
## <a name="permissions"></a>Permisos  
 Esta vista necesita el permiso VIEW DATABASE STATE.  
  
## <a name="remarks"></a>Comentarios  
 Los datos devueltos por **sys.dm_db_resource_stats** se expresa como un porcentaje de los límites máximos permitidos para el nivel de rendimiento o servicio que se está ejecutando.
 
 Si la base de datos se conmutó por error a otro servidor en los últimos 60 minutos, la vista solo devolverá datos correspondientes al tiempo que ha sido la base de datos principal desde la conmutación por error.  
  
 Para obtener una vista menos detallada de estos datos, use **sys.resource_stats** vista de catálogo el **maestro** base de datos. Esta vista captura datos cada 5 minutos y mantiene datos históricos durante 14 días.  Para obtener más información, consulte [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md).  
  
 Cuando una base de datos es un miembro de un grupo elástico, estadísticas de recursos que aparecen como los valores de porcentaje, se expresan como el porcentaje del límite máximo para las bases de datos como se establece en la configuración del grupo elástico.  
  
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
    AVG(avg_log_write_percent) AS 'Average Log Write I/O Throughput Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write I/O Throughput Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Límites y capacidades de nivel de servicio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
