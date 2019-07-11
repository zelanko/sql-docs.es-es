---
title: Sys.resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6918c712e5440aa79bef045f2d64b2578eb42a69
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716318"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve datos de almacenamiento y uso de CPU para una base de datos de Azure SQL. Los datos se recopilan y agregan en intervalos de cinco minutos. Para cada base de datos de usuario, hay una fila por cada ventana de informes de cinco minutos en el que hay un cambio en el consumo de recursos. Los datos devueltos incluyen uso de CPU, el cambio de tamaño de almacenamiento y modificación de la SKU de la base de datos. Las bases de datos inactivas sin cambios no pueden tener filas por cada intervalo de cinco minutos. Los datos históricos se conservan durante 14 días aproximadamente.  
  
 El **sys.resource_stats** vista tiene definiciones diferentes dependiendo de la versión del servidor de base de datos de SQL de Azure que está asociada la base de datos. Tenga en cuenta estas diferencias y cualquier modificación que requiera la aplicación al actualizar a una nueva versión de servidor.  
  
 En la tabla siguiente se describen las columnas disponibles en un servidor v12:  
  
|Columnas|Tipo de datos|Descripción|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora de UTC que indica el inicio del intervalo de informes de cinco minutos.|  
|end_time|**datetime**|Hora de UTC que indica el final del intervalo de informes de cinco minutos.|  
|database_name|**varchar**|Nombre de la base de datos del usuario.|  
|sku|**varchar**|Nivel de servicio de la base de datos. Los posibles valores son los siguientes:<br /><br /> Básica<br /><br /> Estándar<br /><br /> Premium<br /><br />Uso general<br /><br />Crítico para la empresa|  
|storage_in_megabytes|**float**|Tamaño de almacenamiento máximo en megabytes para el período de tiempo, incluida la base de datos, índices, procedimientos almacenados y los metadatos.|  
|avg_cpu_percent|**numeric**|Uso de proceso promedio como porcentaje del límite del nivel de servicio.|  
|avg_data_io_percent|**numeric**|Uso de E/S promedio como porcentaje según el límite del nivel de servicio.|  
|avg_log_write_percent|**numeric**|Uso de recursos de escritura promedio como porcentaje del límite del nivel de servicio.|  
|max_worker_percent|**decimal(5,2)**|Máximo de trabajos simultáneos (solicitudes) en porcentaje basado en el límite del nivel de servicio de la base de datos.<br /><br /> Actualmente se calcula el máximo para el intervalo de cinco minutos en función de las muestras de 15 segundos de recuentos de trabajo simultáneas.|  
|max_session_percent|**decimal(5,2)**|Número máximo de sesiones simultáneo en porcentaje basado en el límite del nivel de servicio de la base de datos.<br /><br /> Actualmente se calcula el máximo para el intervalo de cinco minutos en función de las muestras de 15 segundos de recuentos de sesiones simultáneas.|  
|dtu_limit|**int**|Base de datos max DTU configuración actual de esta base de datos durante este intervalo. |  
|allocated_storage_in_megabytes|**float**|El formato de la cantidad de espacio de archivo en MB disponible para almacenar la base de datos. Espacio de archivo con formato también se conoce como espacio de datos asignado.  Para obtener más información, vea: [Administración del espacio de archivo en la base de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  Para obtener más contexto sobre estos límites y los niveles de servicio, vea los temas [niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/).  
    
## <a name="permissions"></a>Permisos  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a virtual **maestro** base de datos.  
  
## <a name="remarks"></a>Comentarios  
 Los datos devueltos por **sys.resource_stats** se expresa como un porcentaje de los límites máximos permitidos para el nivel de rendimiento o servicio que se está ejecutando.  
  
 Cuando una base de datos es un miembro de un grupo elástico, estadísticas de recursos que aparecen como los valores de porcentaje, se expresan como el porcentaje del límite máximo para las bases de datos como se establece en la configuración del grupo elástico.  
  
 Para obtener una vista más detallada de estos datos, use **sys.dm_db_resource_stats** vista de administración dinámica en una base de datos de usuario. Esta vista captura datos cada 15 segundos u mantiene datos históricos durante 1 hora.  Para obtener más información, consulte [sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

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
  
  
