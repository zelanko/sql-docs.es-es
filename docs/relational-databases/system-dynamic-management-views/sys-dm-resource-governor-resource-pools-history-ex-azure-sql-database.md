---
title: sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor
- sys.resource_governor_TSQL
- resource_governor
- resource_governor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 1bc5c5d8377b93a3e0101f1160444a207b5881cd
ms.sourcegitcommit: 0c049c539ae86264617672936b31d89456d63bb0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58618122"
---
# <a name="sysdmresourcegovernorresourcepoolshistoryex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Instantánea devuelve intervalos de 15 segundos para los últimos 30 minutos del recurso de los grupos de estadísticas para una base de datos de SQL Azure.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pool_id**|INT|Identificador del grupo de recursos. No admite valores NULL.
|**Nombre**|sysname|El nombre del grupo de recursos. No admite valores NULL.|
|**snapshot_time**|datetime2|Fecha y hora de la instantánea de estadísticas de grupo de recursos realizada|
|**duration_ms**|INT|Duración entre la instantánea actual y anterior|
|**statistics_start_time**|datetime2|La hora en que se restablecieron las estadísticas para este grupo. No admite valores NULL.|
|**active_session_count**|INT|Total sesiones activas en la instantánea actual|
|**active_worker_count**|INT|Número total de trabajos de instantánea actual|
|**delta_cpu_usage_ms**|INT|Uso de CPU en milisegundos desde la última instantánea. No admite valores NULL.|
|**delta_cpu_usage_preemptive_ms**|INT|Las llamadas a win32 preferente no se rigen por grupo de recursos de CPU de SQL, desde la última instantánea|
|**used_data_space_kb**|BIGINT|Espacio total usado en las bases de datos de usuario asociados al grupo de usuario|
|**allocated_disk_space_kb**|BIGINT|Tamaño de bases de datos de usuario del archivo de datos total en asociado con el grupo de usuario|
|**target_memory_kb**|BIGINT|La cantidad de memoria de destino, en kilobytes, que el grupo de recursos de servidor está intentando lograr. Depende de la configuración actual y del estado del servidor. No admite valores NULL.|
|**used_memory_kb**|BIGINT|La cantidad de memoria utilizada, en kilobytes, para el grupo de recursos de servidor. No admite valores NULL.|
|**cache_memory_kb**|BIGINT|El uso de la memoria caché total actual en kilobytes. No admite valores NULL.|
|**compile_memory_kb**|BIGINT|El uso de memoria descartada total actual en kilobytes (kB). La mayoría de este uso sería para la compilación y optimización, pero también puede incluir otros usuarios de la memoria. No admite valores NULL.|
|**active_memgrant_count**|BIGINT|El número actual de concesiones de memoria. No admite valores NULL.|
|**active_memgrant_kb**|BIGINT|La suma, en kilobytes (kB), de las concesiones actuales de memoria. No admite valores NULL.|
|**used_memgrant_kb**|BIGINT|La memoria usada (descartada) total actual de las concesiones de memoria. No admite valores NULL.|
|**delta_memgrant_timeout_count**|INT|recuento de memoria conceder los tiempos de espera en este grupo de recursos de este período. No admite valores NULL.|
|**delta_memgrant_waiter_count**|INT|El número de consultas pendientes actualmente en concesiones de memoria. No admite valores NULL.|
|**delta_out_of_memory_count**|INT|El número de asignaciones de memoria con errores en el grupo desde la última instantánea. No admite valores NULL.|
|**delta_read_io_queued**|INT|El total de lectura IOs puestos en cola desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_read_io_issued**|INT|El total de E/s de lectura emitidas desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_read_io_completed**|INT|El total de E/s completadas desde la última instantánea de lectura. No admite valores NULL.|
|**delta_read_io_throttled**|INT|El total de E/s de lectura limitadas desde la instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_read_bytes**|BIGINT|El número total de bytes leídos desde la última instantánea. No admite valores NULL.|
|**delta_read_io_stall_ms**|INT|Tiempo total (en milisegundos) entre la llegada de E/S de lectura y la finalización desde la última instantánea. No admite valores NULL.|
|**delta_read_io_stall_queued_ms**|INT|Tiempo total (en milisegundos) entre la llegada de E/S de lectura y problema desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S. Delta_read_io_stall_queued_ms distinto de cero significa que la E/S es se vean afectada por grupo de recursos.|
|**delta_write_io_queued**|INT|El total de escritura IOs puestos en cola desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_write_io_issued**|INT|El total de E/s de escritura emitidas desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_write_io_completed**|INT|El total de E/s de escritura completadas desde la última instantánea. No admite valores NULL|
|**delta_write_io_throttled**|INT|El total de escritura limitan de IOs desde la última instantánea. No admite valores NULL|
|**delta_write_bytes**|BIGINT|El número total de bytes escritos desde la última instantánea. No admite valores NULL.|
|**delta_write_io_stall_ms**|INT|Tiempo total (en milisegundos) entre la llegada de E/S de escritura y la finalización desde la última instantánea. No admite valores NULL.|
|**delta_write_io_stall_queued_ms**|INT|Tiempo total (en milisegundos) entre la llegada de E/S de escritura y de problemas desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_io_issue_delay_ms**|INT|Tiempo total (en milisegundos) entre la emisión programada y el número real de E/S desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**max_iops_per_volume**|INT|E/S máxima por segundo (IOPS) por la configuración de volumen de disco para este grupo. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**max_memory_kb**|BIGINT|La cantidad máxima de memoria, en kilobytes, que el grupo de recursos de servidor puede tener. Depende de la configuración actual y del estado del servidor. No admite valores NULL.
|**max_log_rate_kb**|BIGINT|Tasa de registro máximo (kilobytes por segundo) en el nivel del grupo de recursos.|
|**max_data_space_kb**|BIGINT|Límite de almacenamiento máximo del grupo elástico para este grupo elástico en kilobytes.|
|**max_session**|INT|Límite de sesión para el grupo|
|**max_worker**|INT|Límite de trabajo para el grupo|
|**min_cpu_percent**|INT|La configuración actual del ancho banda de la CPU promedio garantizado para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL.|
|**max_cpu_percent**|INT|La configuración actual del ancho banda de la CPU promedio máximo permitido para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL.|
|**cap_cpu_percent**|INT|El límite máximo de ancho de banda de la CPU que recibirán todas las solicitudes en el grupo de recursos. Limita el nivel de ancho de banda máximo de la CPU según el nivel especificado. El intervalo permitido para el valor es de 1 a 100. No admite valores NULL.|
|**min_vcores**|decimal(5,2)|La configuración actual del ancho banda de la CPU promedio garantizado para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU.  En unidades de núcleos virtuales|
|**max_vcores**|decimal(5,2)|La configuración actual del ancho banda de la CPU promedio máximo permitido para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU.  En la unidad de núcleos virtuales|
|**cap_vcores**|decimal(5,2)|El límite máximo de ancho de banda de la CPU que recibirán todas las solicitudes en el grupo de recursos.  En la unidad en núcleos virtuales|
|**instance_cpu_count**|INT|Número de CPU configurado para la instancia|
|**instance_cpu_percent|decimal(5,2)|Porcentaje de CPU configurado para la instancia|
|**instance_vcores**|decimal(5,2)|Número de núcleos virtuales configuradas para la instancia|
|**delta_log_bytes_used**|decimal(5,2)|Generación de registro total (en bytes) en el nivel de grupo desde la última instantánea|
|**avg_login_rate_percent**|decimal(5,2)|Número de inicios de sesión desde la última instantánea, en comparación con el límite de inicio de sesión|
|**delta_vcores_used**|decimal(5,2)|Uso de proceso en el recuento de núcleos virtuales desde la última instantánea.|
|**cap_vcores_used_percent**|decimal(5,2)|Uso de proceso medio en porcentaje del límite del grupo.|
|**instance_vcores_used_percent**|decimal(5,2)|Uso de proceso promedio como porcentaje del límite de la instancia de SQL.|
|**avg_data_io_percent**|decimal(5,2)|Uso de E/S medio en porcentaje basado en el límite del grupo.|
|**avg_log_write_percent**|decimal(5,2)|Promedio de escritura utilización de recursos en porcentaje del límite del grupo.|
|**avg_storage_percent**|decimal(5,2)|Promedio de utilización del almacenamiento en porcentaje del límite del grupo de almacenamiento.|
|**avg_allocated_storage_percent**|decimal(5,2)|El porcentaje de espacio de datos asignado todas las bases de datos en el grupo elástico. Esto es la proporción de espacio de datos asignado al tamaño máximo de datos para el grupo elástico. Para obtener más información, vea: Administración del espacio de archivo en la base de datos SQL|
|**max_worker_percent**|decimal(5,2)|Máximo de trabajos simultáneos (solicitudes) en porcentaje basado en el límite del grupo.|
|**max_session_percent**|decimal(5,2)|Número máximo de sesiones simultáneo en porcentaje basado en el límite del grupo.|
|||

## <a name="permissions"></a>Permisos

Esta vista necesita el permiso VIEW DATABASE STATE.

## <a name="remarks"></a>Comentarios

Los usuarios pueden tener acceso a esta vista de administración dinámica para supervisar casi en tiempo real de consumo de recursos para el grupo de cargas de trabajo de usuario, así como los grupos internos del sistema de la instancia de Azure SQL Database.

> [!IMPORTANT]
> La mayoría de los datos que se exponen a través de esta DMV está pensado para su uso interno y está sujeta a cambios.

## <a name="examples"></a>Ejemplos

El ejemplo siguiente devuelve los datos de tasa de registro máximo y el consumo en cada instantánea por grupo de usuario  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

El ejemplo siguiente devuelve información similar como sys.elastic_pool_resource_stats sin tener que conectarse a la maestra lógica

```sql
select snapshot_time, name, cap_vcores_used_percent,
  avg_data_io_percent,  
  avg_log_write_percent,
  avg_storage_percent,
  avg_allocated_storage_percent,
  max_data_space_kb,
  max_worker_percent,
  max_session_percent
    from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

## <a name="see-also"></a>Vea también

- [Gobierno de tasa de registro de traducción](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Límites de recursos DTU de grupo elástico](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Límites de recursos de memoria con núcleo virtual grupo elástico](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)