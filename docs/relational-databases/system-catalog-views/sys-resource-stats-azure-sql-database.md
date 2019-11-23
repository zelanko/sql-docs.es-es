---
title: Sys. resource_stats (Azure SQL Database) | Microsoft Docs
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0c39d57e84e27f7449ebc8464691d2d8ad887848
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "70911107"
---
# <a name="sysresource_stats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve los datos de almacenamiento y uso de CPU para Azure SQL Database. Los datos se recopilan y se agregan en intervalos de cinco minutos. Para cada base de datos de usuario, hay una fila por cada ventana de informes de cinco minutos en la que hay un cambio en el consumo de recursos. Los datos devueltos incluyen el uso de CPU, el cambio de tamaño de almacenamiento y la modificación de la SKU de base de datos. Las bases de datos inactivas sin cambios no pueden tener filas por cada intervalo de cinco minutos. Los datos históricos se conservan durante 14 días aproximadamente.  
  
 La vista **Sys. resource_stats** tiene definiciones diferentes en función de la versión del servidor de Azure SQL Database al que está asociada la base de datos. Tenga en cuenta estas diferencias y cualquier modificación que requiera la aplicación al actualizar a una nueva versión de servidor.  
  
 En la tabla siguiente se describen las columnas disponibles en un servidor v12:  
  
|Columnas|Tipo de datos|Descripción|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora UTC que indica el inicio del intervalo de informes de cinco minutos.|  
|end_time|**datetime**|Hora UTC que indica el final del intervalo de informes de cinco minutos.|  
|database_name|**nvarchar(128)**|Nombre de la base de datos del usuario.|  
|sku|**nvarchar(128)**|Nivel de servicio de la base de datos. Los posibles valores son los siguientes:<br /><br /> Basic<br /><br /> Estándar<br /><br /> Premium<br /><br />Uso general<br /><br />Crucial para la empresa|  
|storage_in_megabytes|**float**|Tamaño de almacenamiento máximo en megabytes para el período de tiempo, incluidos los datos de base de datos, los índices, los procedimientos almacenados y los metadatos.|  
|avg_cpu_percent|**decimal(5,2)**|Uso de proceso promedio como porcentaje del límite del nivel de servicio.|  
|avg_data_io_percent|**decimal(5,2)**|Uso de E/S promedio como porcentaje según el límite del nivel de servicio.|  
|avg_log_write_percent|**decimal(5,2)**|Uso de recursos de escritura promedio como porcentaje del límite del nivel de servicio.|  
|max_worker_percent|**decimal(5,2)**|Número máximo de trabajos simultáneos (solicitudes) en porcentaje según el límite del nivel de servicio de la base de datos.<br /><br /> El máximo se calcula actualmente para el intervalo de cinco minutos basado en las muestras de 15 segundos de los recuentos de trabajo simultáneos.|  
|max_session_percent|**decimal(5,2)**|Número máximo de sesiones simultáneas en porcentaje según el límite del nivel de servicio de la base de datos.<br /><br /> El valor máximo se calcula actualmente para el intervalo de cinco minutos basado en las muestras de 15 segundos de los recuentos de sesiones simultáneas.|  
|dtu_limit|**int**|Valor actual máximo de DTU de base de datos para esta base de datos durante este intervalo. |
|xtp_storage_percent|**decimal (5, 2)**|Uso del almacenamiento para OLTP en memoria en porcentaje del límite del nivel de servicio (al final del intervalo de informes). Esto incluye la memoria usada para el almacenamiento de los siguientes objetos OLTP en memoria: tablas, índices y variables de tabla con optimización para memoria. También incluye la memoria usada para procesar las operaciones de ALTER TABLE.<br /><br /> Devuelve 0 si no se utiliza OLTP en memoria en la base de datos.|
|avg_login_rate_percent|**decimal (5, 2)**|Solamente se identifica con fines informativos. No admitido. La compatibilidad con versiones posteriores no está garantizada.|
|avg_instance_cpu_percent|**decimal (5, 2)**|Uso promedio de la CPU de la base de datos como porcentaje del proceso de base de datos de SQL.|
|avg_instance_memory_percent|**decimal (5, 2)**|Promedio de uso de memoria de base de datos como porcentaje del proceso de base de datos de SQL.|
|cpu_limit|**decimal (5, 2)**|Número de núcleos virtuales para esta base de datos durante este intervalo. En el caso de las bases de datos que usan el modelo basado en DTU, esta columna es NULL.|
|allocated_storage_in_megabytes|**float**|La cantidad de espacio de archivo con formato en MB disponible para almacenar los datos de la base de datos. El espacio de archivo con formato también se conoce como espacio de datos asignado.  Para obtener más información, vea [Administración del espacio de archivo en SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management) .|
  
> [!TIP]  
>  Para más información sobre estos límites y los niveles de servicio, consulte los temas sobre los [niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/).  
    
## <a name="permissions"></a>Permisos  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a la base de datos **maestra** virtual.  
  
## <a name="remarks"></a>Remarks  
 Los datos devueltos por **Sys. resource_stats** se expresan como un porcentaje de los límites máximos permitidos para el nivel de servicio/nivel de rendimiento que se está ejecutando.  
  
 Cuando una base de datos es miembro de un grupo elástico, las estadísticas de recursos que se presentan como valores porcentuales se expresan como el porcentaje del límite máximo de las bases de datos establecidas en la configuración del grupo elástico.  
  
 Para obtener una vista más detallada de estos datos, use la vista de administración dinámica **Sys. dm_db_resource_stats** en una base de datos de usuario. Esta vista captura datos cada 15 segundos u mantiene datos históricos durante 1 hora.  Para obtener más información, vea [Sys. &#40;dm_db_resource_stats&#41;Azure SQL Database](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

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
 [Capacidades y límites del nivel de servicio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
