---
title: Sys.server_resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.service: sql-database
ms.reviewer: carlrab, edmaca
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
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 72e363b05e8f14dda535abd70e4218c949c42c91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133069"
---
# <a name="sysserverresourcestats-azure-sql-database"></a>Sys.server_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Devuelve los datos de almacenamiento, la E/S y el uso de CPU para una instancia administrada de SQL de Azure. Los datos se recopilan y agregan en intervalos de cinco minutos. Hay una fila para cada 15 segundos de informes. Los datos devueltos incluyen el uso de CPU, tamaño de almacenamiento, uso de E/S y SKU de instancia administrada. Los datos históricos se conservan durante 14 días aproximadamente.

El **sys.server_resource_stats** vista tiene definiciones diferentes dependiendo de la versión de la instancia administrada de SQL de Azure que está asociada la base de datos. Tenga en cuenta estas diferencias y cualquier modificación que requiera la aplicación al actualizar a una nueva versión de servidor.
 
  
 En la tabla siguiente se describen las columnas disponibles en un servidor v12:  
  
|Columnas|Tipo de datos|Descripción|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|Hora UTC que indica el inicio del intervalo de informes de quince segundos|  
|end_time|**datetime**|Hora UTC que indica el final del intervalo de informes de quince segundos|
|resource_type|nvarchar (128)|Tipo de recurso para el que se proporcionan métricas|
|resource_name|nvarchar (128)|Nombre del recurso.|
|sku|nvarchar (128)|Administrar el nivel de servicio de instancia de la instancia. Los posibles valores son los siguientes: <br><ul><li>Uso general</li></ul><ul><li>Crítico para la empresa</li></ul>|
|hardware_generation|nvarchar (128)|Identificador de generación de hardware: por ejemplo, Gen 4 o Gen 5|
|virtual_core_count|int|Representa el número de núcleos virtuales por instancia (8, 16 o 24 en versión preliminar pública)|
|avg_cpu_percent|decimal (5,2)|Promedio de uso en porcentaje del límite del nivel de servicio de instancia administrada usado por la instancia de proceso. Se calcula como la suma del tiempo de CPU de todos los grupos de recursos para todas las bases de datos en la instancia y dividido por el tiempo de CPU disponible para ese nivel en el intervalo especificado.|
|reserved_storage_mb|bigint|Reservado el almacenamiento por instancia (cantidad de almacenamiento de espacio que el cliente comprado para la instancia administrada)|
|storage_space_used_mb|decimal(18,2)|Almacenamiento utilizado por los archivos de todas las instancia administrada las bases de datos (incluidas las bases de datos de usuario y del sistema)|
|io_request|bigint|Número total de operaciones de e/s física dentro del intervalo|
|io_bytes_read|bigint|Número de bytes físicos dentro del intervalo de lectura|
|io_bytes_written|bigint|Número de bytes físicos escritos dentro del intervalo|

 
> [!TIP]  
>  Para obtener más contexto sobre estos límites y los niveles de servicio, vea los temas [niveles de servicio de instancia administrada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers).  
    
## <a name="permissions"></a>Permisos  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a la **maestro** base de datos.  
  
## <a name="remarks"></a>Comentarios  
 Los datos devueltos por **sys.server_resource_stats** se expresan como el total utilizado en bytes o megabytes (que se indica en los nombres de columna) que no sea avg_cpu, que se expresa como un porcentaje de los límites máximos permitidos para el servicio nivel de rendimiento o que se está ejecutando.  
 
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todas las bases de datos cuyo promedio de uso de proceso fue al menos del 80 % durante la semana pasada.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT resource_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.server_resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY resource_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>Vea también  
 [Administra los niveles de servicio de instancia](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)
