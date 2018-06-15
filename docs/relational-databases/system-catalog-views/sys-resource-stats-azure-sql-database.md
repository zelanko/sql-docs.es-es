---
title: Sys.resource_stats (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c2f8a0e0cebcf64bedac33861184e806f322d7d1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221206"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve los datos de almacenamiento y uso de CPU para Azure SQL Database. Los datos se recopilan y se agregan en intervalos de cinco minutos. Para cada base de datos de usuario, existe una fila para cada ventana de informes de cinco minutos en que haya cambios en el consumo de recursos. Los datos devueltos incluyen el uso de CPU, cambio de tamaño de almacenamiento o modificación de la SKU de la base de datos. Las bases de datos inactivas sin cambios no pueden tener filas por cada intervalo de cinco minutos. Los datos históricos se conservan durante 14 días aproximadamente.  
  
 El **sys.resource_stats** vista tiene definiciones diferentes dependiendo de la versión del servidor de base de datos de SQL Azure que está asociada la base de datos. Tenga en cuenta estas diferencias y cualquier modificación que requiera la aplicación al actualizar a una nueva versión de servidor.  
  
 En la tabla siguiente se describen las columnas disponibles en un servidor v12:  
  
|Columnas|Tipo de datos|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora UTC que indica el inicio del intervalo de notificación de cinco minutos.|  
|end_time|**datetime**|Hora UTC que indica el final del intervalo informes de cinco minutos.|  
|database_name|**varchar**|Nombre de la base de datos del usuario.|  
|sku|**varchar**|Nivel de servicio de la base de datos. Los posibles valores son los siguientes:<br /><br /> Básico<br /><br /> Standard<br /><br /> Premium<br /><br />Uso general<br /><br />Crucial para la empresa|  
|storage_in_megabytes|**float**|Tamaño de almacenamiento máximo en megabytes para el período de tiempo, incluidos los datos de la base de datos, índices, procedimientos almacenados y metadatos.|  
|avg_cpu_percent|**numeric**|Uso de proceso promedio como porcentaje del límite del nivel de servicio.|  
|avg_data_io_percent|**numeric**|Uso de E/S promedio como porcentaje según el límite del nivel de servicio.|  
|avg_log_write_percent|**numeric**|Uso de recursos de escritura promedio como porcentaje del límite del nivel de servicio.|  
|max_worker_percent|**decimal(5,2)**|Máximos simultáneos trabajadores (solicitudes) de porcentaje se basa en el límite de nivel de servicio de la base de datos.<br /><br /> Actualmente se calcula el máximo para el intervalo de cinco minutos en función de los ejemplos de 15 segundos de recuentos de trabajo simultáneas.|  
|max_session_percent|**decimal(5,2)**|Número máximo de sesiones simultáneo de porcentaje se basa en el límite de nivel de servicio de la base de datos.<br /><br /> Actualmente se calcula el máximo para el intervalo de cinco minutos en función de los ejemplos de 15 segundos de recuentos de sesiones simultáneas.|  
|dtu_limit|**int**|Base de datos max DTU configuración actual de esta base de datos durante este intervalo. |  
  
> [!TIP]  
>  Para obtener más contexto sobre estos límites y los niveles de servicio, vea los temas [niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/).  
    
## <a name="permissions"></a>Permissions  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a virtual **maestro** base de datos.  
  
## <a name="remarks"></a>Comentarios  
 Los datos devueltos por **sys.resource_stats** se expresa como un porcentaje del máximo permitido de límites para el nivel / rendimiento de nivel de servicio que se está ejecutando.  
  
 Cuando una base de datos es un miembro de un grupo elástico, las estadísticas de recursos que se presentan como valores de porcentaje se expresan como el porcentaje del límite máximo de las bases de datos como se establece en la configuración del grupo elástico.  
  
 Para obtener una vista más detallada de estos datos, use **sys.dm_db_resource_stats** vista de administración dinámica en una base de datos de usuario. Esta vista captura datos cada 15 segundos y mantiene datos históricos durante 1 hora.  Para obtener más información, consulte [sys.dm_db_resource_stats &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todas las bases de datos cuyo promedio de uso de proceso fue al menos del 80 % durante la semana pasada.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>Vea también  
 [Niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Límites y capacidades de nivel de servicio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
