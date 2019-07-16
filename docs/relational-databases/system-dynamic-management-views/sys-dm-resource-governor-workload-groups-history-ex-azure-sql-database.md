---
title: Sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups_history_ex_TSQL
- sys.dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_resource_governor_workload_groups_history_ex dynamic management view
author: joesackmsft
ms.author: josack
ms.openlocfilehash: ac776813cb817d1357948091bfc48c981fa8e730
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053262"
---
# <a name="sysdmresourcegovernorworkloadgroupshistoryex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Instantánea devuelve intervalos de 15 segundos para los últimos 30 minutos del recurso de los grupos de estadísticas para una base de datos de SQL Azure.
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pool_id**| int |Id. del grupo de recursos de servidor. No admite valores NULL.|
|**group_id**| int |Id. del grupo de cargas de trabajo No admite valores NULL.|
|**name**| nvarchar(256) |Nombre del grupo de cargas de trabajo No admite valores NULL.|
|**snapshot_time**| datetime |Fecha y hora de la instantánea de estadísticas de grupo de recursos realizada.|
|**duration_ms**| int |Duración entre la instantánea actual y anterior.|
|**active_worker_count**| int |Número total de trabajos de instantánea actual.|
|**active_request_count**| int |Recuento actual de solicitudes. No admite valores NULL.|
|**active_session_count**| int |Total sesiones activas en la instantánea actual.|
|**total_request_count**| bigint |El recuento acumulado de solicitudes completadas en el grupo de cargas de trabajo. No admite valores NULL.|
|**delta_request_count**| int |Recuento de solicitudes completadas en el grupo de cargas de trabajo desde la última instantánea. No admite valores NULL.|
|**total_cpu_usage_ms**| bigint |Uso acumulado de la CPU en milisegundos de este grupo de cargas de trabajo. No admite valores NULL.|
|**delta_cpu_usage_ms**| int |Uso de CPU en milisegundos desde la última instantánea. No admite valores NULL.|
|**delta_cpu_usage_preemptive_ms**| int |Las llamadas a win32 preferente se rigen por grupo de recursos de CPU de SQL, no desde la última instantánea.|
|**delta_reads_reduced_memgrant_count**| int |El recuento de concesiones de memoria que se alcanza el límite de tamaño máximo de consulta desde la última instantánea. No admite valores NULL.|
|**reads_throttled**| int |Número total de lecturas limitadas.|
|**delta_reads_queued**| int |El total de lectura IOs puestos en cola desde la última instantánea. Acepta valores NULL. Es null si el grupo de recursos no está regulado para E/S.|
|**delta_reads_issued**| int |El total de E/s de lectura emitidas desde la última instantánea. Acepta valores NULL. Es null si el grupo de recursos no está regulado para E/S.|
|**delta_reads_completed**| int |El total de E/s completadas desde la última instantánea de lectura. No admite valores NULL.|
|**delta_read_bytes**| bigint |El número total de bytes leídos desde la última instantánea. No admite valores NULL.|
|**delta_read_stall_ms**| int |Tiempo total (en milisegundos) entre la llegada de E/S de lectura y la finalización desde la última instantánea. No admite valores NULL.|
|**delta_read_stall_queued_ms**| int |Tiempo total (en milisegundos) entre la llegada de E/S de lectura y problema desde la última instantánea. Acepta valores NULL. Es null si el grupo de recursos no está regulado para E/S. Delta_read_stall_queued_ms distinto de cero significa que la E/S es se vean afectada por grupo de recursos.|
|**delta_writes_queued**| int |El total de escritura IOs puestos en cola desde la última instantánea. Acepta valores NULL. Es null si el grupo de recursos no está regulado para E/S.|
|**delta_writes_issued**| int |El total de E/s de escritura emitidas desde la última instantánea. Acepta valores NULL. Es null si el grupo de recursos no está regulado para E/S.|
|**delta_writes_completed**| int |El total de E/s de escritura completadas desde la última instantánea. No admite valores NULL.|
|**delta_writes_bytes**| bigint |El número total de bytes escritos desde la última instantánea. No admite valores NULL.|
|**delta_write_stall_ms**| int |Tiempo total (en milisegundos) entre la llegada de E/S de escritura y la finalización desde la última instantánea. No admite valores NULL.|
|**delta_background_writes**| int |Nº total de escrituras realizada por tareas en segundo plano desde la última instantánea.|
|**delta_background_write_bytes**| bigint |El tamaño total de escritura realizado por tareas en segundo plano desde la última instantánea, en bytes.|
|**delta_log_bytes_used**| bigint |Registro utilizado desde la última instantánea en bytes.|
|**delta_log_temp_db_bytes_used**| bigint |Registro de tempdb usado desde la última instantánea en bytes.|
|**delta_query_optimizations**| bigint |El recuento de las optimizaciones de consultas de este grupo de cargas de trabajo desde la última instantánea. No admite valores NULL.|
|**delta_suboptimal_plan_generations**| bigint |El número de generaciones de plan poco óptimo que se produjeron en este grupo de cargas de trabajo debido a presión de memoria desde la última instantánea. No admite valores NULL.
|**max_memory_grant_kb**| bigint |Concesión de memoria máximo para el grupo en KB.|
|**max_request_cpu_msec**| bigint |Uso máximo de CPU, en milisegundos, para una única solicitud. No admite valores NULL.|
|**max_concurrent_request**| int |Valor actual del número máximo de solicitudes simultáneas. No admite valores NULL.|
|**max_io**| int |Límite máximo de E/S para el grupo.|
|**max_global_io**| int |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.
|**max_queued_io**| int |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.|
|**max_log_rate_kb**| bigint |Tasa de registro máximo (kilobytes por segundo) en el nivel del grupo de recursos.|
|**max_session**| int |Límite de sesión para el grupo.|
|**max_worker**| int |Límite de trabajo para el grupo.|
|||

## <a name="permissions"></a>Permisos

Esta vista requiere el permiso VIEW SERVER STATE.

## <a name="remarks"></a>Comentarios

Los usuarios pueden tener acceso a esta vista de administración dinámica para supervisar casi en tiempo real de consumo de recursos para el grupo de cargas de trabajo de usuario, así como los grupos internos del sistema de la instancia de Azure SQL Database.

> [!IMPORTANT]
> La mayoría de los datos que se exponen a través de esta DMV está pensado para su uso interno y está sujeta a cambios.

## <a name="examples"></a>Ejemplos

El ejemplo siguiente devuelve los datos de tasa de registro máximo y el consumo en cada instantánea por grupo de usuario:

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>Vea también

- [Gobierno de tasa de registro de traducción](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Límites de recursos DTU de grupo elástico](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Límites de recursos de memoria con núcleo virtual grupo elástico](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
