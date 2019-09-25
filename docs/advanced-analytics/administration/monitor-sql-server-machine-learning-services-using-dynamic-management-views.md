---
title: Supervisión de la ejecución de scripts de Python y R mediante DMV
description: Use las vistas de administración dinámica (DMV) para supervisar la ejecución de scripts externos de Python y R en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0e541e1d0eb2a8bb1ac512276fa395f8d8c6379f
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2019
ms.locfileid: "70978404"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>Supervisar SQL Server Machine Learning Services mediante vistas de administración dinámica (DMV)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use las vistas de administración dinámica (DMV) para supervisar la ejecución de scripts externos (Python y R), los recursos usados, diagnosticar problemas y ajustar el rendimiento en SQL Server Machine Learning Services.

En este artículo, encontrará las DMV específicas de SQL Server Machine Learning Services. También encontrará consultas de ejemplo que muestran:

+ Opciones de configuración y configuración de machine learning
+ Sesiones activas que ejecutan Python o scripts externos
+ Estadísticas de ejecución del tiempo de ejecución externo para Python y R
+ Contadores de rendimiento para scripts externos
+ Uso de memoria para el sistema operativo, el SQL Server y los grupos de recursos externos
+ Configuración de memoria para SQL Server y grupos de recursos externos
+ Resource Governor de grupos de recursos, incluidos los grupos de recursos externos
+ Paquetes instalados para Python y R

Para obtener más información general sobre las DMV, consulte [vistas de administración dinámica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).

> [!TIP]
> También puede usar los informes personalizados para supervisar SQL Server Machine Learning Services. Para obtener más información, consulte [supervisión del aprendizaje automático mediante informes personalizados en Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="dynamic-management-views"></a>Vistas de administración dinámica

Se pueden usar las siguientes vistas de administración dinámica al supervisar cargas de trabajo de machine learning en SQL Server. Para consultar las DMV, necesita `VIEW SERVER STATE` el permiso en la instancia.

| Vista de administración dinámica | Tipo | Descripción |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | Ejecución | Devuelve una fila para cada cuenta de trabajo activa que ejecuta un script externo. |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | Ejecución | Devuelve una fila por cada tipo de solicitud de script externo. |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | Ejecución | Devuelve una fila por contador de rendimiento que se mantiene en el servidor. Si usa la condición `WHERE object_name LIKE '%External Scripts%'`de búsqueda, puede usar esta información para ver cuántos scripts se ejecutaron, qué scripts se ejecutaban con qué modo de autenticación o cuántas llamadas de R o Python se emitieron en la instancia en general. |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | regulador de recursos | Devuelve información sobre el estado actual del grupo de recursos externos en Resource Governor, la configuración actual de los grupos de recursos y las estadísticas del grupo de recursos. |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | regulador de recursos | Devuelve información de afinidad de CPU acerca de la configuración actual del grupo de recursos externos en Resource Governor. Devuelve una fila por programador en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] donde cada programador está asignado a un determinado procesador. Use esta vista para supervisar la condición de un programador o identificar tareas descontroladas. |

Para obtener información acerca [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de la supervisión de instancias, vea [vistas de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) y [Resource Governor vistas de administración dinámica relacionadas](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="settings-and-configuration"></a>Configuración y configuración

Vea la configuración de la instalación de Machine Learning Services y las opciones de configuración.

![Salida de la consulta de configuración y configuración](media/dmv-settings-and-configuration.png "Salida de la consulta de configuración y configuración")

Ejecute la consulta siguiente para obtener esta salida. Para obtener más información sobre las vistas y funciones usadas, vea [Sys. DM _ _server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [Sys.](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)Configurations y [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md).

```sql
SELECT CAST(SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS INT) AS IsMLServicesInstalled
    , CAST(value_in_use AS INT) AS ExternalScriptsEnabled
    , COALESCE(SIGN(SUSER_ID(CONCAT (
                    CAST(SERVERPROPERTY('MachineName') AS NVARCHAR(128))
                    , '\SQLRUserGroup'
                    , CAST(serverproperty('InstanceName') AS NVARCHAR(128))
                    ))), 0) AS ImpliedAuthenticationEnabled
    , COALESCE((
            SELECT CAST(r.value_data AS INT)
            FROM sys.dm_server_registry AS r
            WHERE r.registry_key LIKE 'HKLM\Software\Microsoft\Microsoft SQL Server\%\SuperSocketNetLib\Tcp'
            AND r.value_name = 'Enabled'
            ), - 1) AS IsTcpEnabled
FROM sys.configurations
WHERE name = 'external scripts enabled';
```

La consulta devuelve las columnas siguientes:

| columna | Descripción |
|--------|-------------|
| IsMLServicesInstalled | Devuelve 1 si se ha instalado SQL Server Machine Learning Services para la instancia de. De lo contrario, devuelve 0. |
| ExternalScriptsEnabled | Devuelve 1 si los scripts externos están habilitados para la instancia de. De lo contrario, devuelve 0. |
| ImpliedAuthenticationEnabled | Devuelve 1 si está habilitada la autenticación implícita. De lo contrario, devuelve 0. La configuración de la autenticación implícita se comprueba comprobando si existe un inicio de sesión para SQLRUserGroup. |
| IsTcpEnabled | Devuelve 1 si el protocolo TCP/IP está habilitado para la instancia de. De lo contrario, devuelve 0. Para obtener más información, vea [configuración predeterminada del Protocolo de red SQL Server](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md). |

## <a name="active-sessions"></a>Sesiones activas

Vea las sesiones activas que ejecutan scripts externos.

![Salida de la consulta de configuración activa](media/dmv-active-sessions.png "Salida de la consulta de configuración activa")

Ejecute la consulta siguiente para obtener esta salida. Para obtener más información sobre las vistas de administración dinámica usadas, vea [Sys. DM _ _exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md), [Sys. DM _ _external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)y [Sys. DM _ exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).

```sql
SELECT r.session_id, r.blocking_session_id, r.status, DB_NAME(s.database_id) AS database_name
    , s.login_name, r.wait_time, r.wait_type, r.last_wait_type, r.total_elapsed_time, r.cpu_time
    , r.reads, r.logical_reads, r.writes, er.language, er.degree_of_parallelism, er.external_user_name
FROM sys.dm_exec_requests AS r
INNER JOIN sys.dm_external_script_requests AS er
ON r.external_script_request_id = er.external_script_request_id
INNER JOIN sys.dm_exec_sessions AS s
ON s.session_id = r.session_id;
```

La consulta devuelve las columnas siguientes:

| columna | Descripción |
|--------|-------------|
| session_id | Identifica la sesión asociada a cada conexión principal activa. |
| blocking_session_id | Id. de la sesión que bloquea la solicitud. Si esta columna es NULL, la solicitud no está bloqueada o la información de la sesión de bloqueo no está disponible (o no puede ser identificada). |
| status | Estado de la solicitud. |
| database_name | Nombre de la base de datos actual de cada sesión. |
| login_name | SQL Server nombre de inicio de sesión en el que se está ejecutando la sesión actualmente. |
| wait_time | Si la solicitud está actualmente bloqueada, esta columna devuelve la duración en milisegundos de la espera actual. No admite valores NULL. |
| wait_type | Si la solicitud está actualmente bloqueada, esta columna devuelve el tipo de espera. Para obtener información sobre los tipos de esperas, vea [Sys. DM _ _os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). |
| last_wait_type | Si esta solicitud se ha bloqueado anteriormente, esta columna devuelve el tipo de la última espera. |
| total_elapsed_time | Tiempo total transcurrido en milisegundos desde que llegó la solicitud. |
| cpu_time | Tiempo de CPU en milisegundos utilizado por la solicitud. |
| reads | Número de lecturas realizadas por esta solicitud. |
| logical_reads | Número de lecturas lógicas realizadas por la solicitud. |
| writes | Número de escrituras realizadas por esta solicitud. |
| language | Palabra clave que representa un lenguaje de script compatible. |
| degree_of_parallelism | Número que indica el número de procesos paralelos que se crearon. Este valor podría ser diferente del número de procesos paralelos que se solicitaron. |
| external_user_name | La cuenta de trabajo de Windows bajo la que se ejecutó el script. |

## <a name="execution-statistics"></a>Estadísticas de ejecución

Vea las estadísticas de ejecución para el tiempo de ejecución externo de R y Python. En la actualidad, solo están disponibles las estadísticas de las funciones del paquete RevoScaleR, revoscalepy o microsoftml.

![Salida de la consulta de estadísticas de ejecución](media/dmv-execution-statistics.png "Salida de la consulta de estadísticas de ejecución")

Ejecute la consulta siguiente para obtener esta salida. Para obtener más información sobre la vista de administración dinámica utilizada, vea [Sys. DM _ _external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). La consulta solo devuelve funciones que se han ejecutado más de una vez.

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

La consulta devuelve las columnas siguientes:

| columna | Descripción |
|--------|-------------|
| language | Nombre del lenguaje de script externo registrado. |
| counter_name | Nombre de una función de script externo seleccionada. |
| counter_value | Número total de instancias que en que se ha llamado la función registrada de script externo en el servidor. Este valor es acumulativo, comienza en el momento en que se instaló la característica en la instancia y no se puede restablecer. |

## <a name="performance-counters"></a>Contadores de rendimiento

Vea los contadores de rendimiento relacionados con la ejecución de scripts externos.

![Salida de la consulta de contadores de rendimiento](media/dmv-performance-counters.png "Salida de la consulta de contadores de rendimiento")

Ejecute la consulta siguiente para obtener esta salida. Para obtener más información sobre la vista de administración dinámica utilizada, vea [Sys. DM _ _os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md).

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**Sys. DM _ _os_performance_counters** genera los siguientes contadores de rendimiento para los scripts externos:

| Contador | Descripción |
|---------|-------------|
| Ejecuciones totales | Número de procesos externos iniciados por llamadas locales o remotas. |
| Ejecuciones en paralelo | Número de veces que un script incluyó la  _\@especificación paralela_ y que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pudo generar y usar un plan de consulta paralelo. |
| Ejecuciones de streaming | Número de veces que se ha invocado la característica de streaming. |
| Ejecuciones CC de SQL | Número de scripts externos ejecutados en los que se creó una instancia de la llamada de forma remota y se usó SQL Server como el contexto de cálculo. |
| Autenticación implícita. Inicios de sesión | Número de veces que se realizó una llamada de bucle invertido ODBC mediante autenticación implícita; es decir, el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ejecutó la llamada en nombre del usuario que envía la solicitud de script. |
| Tiempo total de ejecución (ms) | Tiempo transcurrido entre la llamada y la finalización de la llamada. |
| Errores de ejecución | Número de veces que los scripts han generado errores. Este recuento no incluye errores de R o Python. |

## <a name="memory-usage"></a>Uso de la memoria

Ver información acerca de la memoria usada por el sistema operativo, SQL Server y los grupos externos.

![Salida de la consulta de uso de memoria](media/dmv-memory-usage.png "Salida de la consulta de uso de memoria")

Ejecute la consulta siguiente para obtener esta salida. Para obtener más información sobre las vistas de administración dinámica utilizadas, vea [Sys. DM _ _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) y [Sys. DM _ _os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md).

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

La consulta devuelve las columnas siguientes:

| columna | Descripción |
|--------|-------------|
| physical_memory_kb | La cantidad total de memoria física en el equipo. |
| committed_kb | Memoria asignada en kilobytes (KB) en el administrador de memoria. No incluye la memoria reservada del administrador de memoria. |
| external_pool_peak_memory_kb | La suma de la cantidad máxima de memoria utilizada, en kilobytes, para todos los grupos de recursos externos. |

## <a name="memory-configuration"></a>Configuración de la memoria

Ver información sobre la configuración de memoria máxima en porcentaje de SQL Server y grupos de recursos externos. Si SQL Server se está ejecutando con el valor predeterminado `max server memory (MB)`de, se considera como 100% de la memoria del sistema operativo.

![Salida de la consulta de configuración de memoria](media/dmv-memory-configuration.png "Salida de la consulta de configuración de memoria")

Ejecute la consulta siguiente para obtener esta salida. Para obtener más información sobre las vistas usadas, vea [Sys.](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) Configurations y [Sys. DM _ _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```sql
SELECT 'SQL Server' AS name
    , CASE CAST(c.value AS BIGINT)
        WHEN 2147483647 THEN 100
        ELSE (SELECT CAST(c.value AS BIGINT) / (physical_memory_kb / 1024.0) * 100 FROM sys.dm_os_sys_info)
        END AS max_memory_percent
FROM sys.configurations AS c
WHERE c.name LIKE 'max server memory (MB)'
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name, ep.max_memory_percent
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

La consulta devuelve las columnas siguientes:

| columna | Descripción |
|--------|-------------|
| name | Nombre del grupo de recursos externos o SQL Server. |
| max_memory_percent | Memoria máxima que SQL Server o el grupo de recursos externos puede usar. |

## <a name="resource-pools"></a>Grupos de recursos de servidor

En [SQL Server Resource Governor](../../relational-databases/resource-governor/resource-governor.md), un [grupo de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md) de dispositivo representa un subconjunto de los recursos físicos de una instancia. Puede especificar los límites en la cantidad de CPU, e/s física y memoria que las solicitudes de aplicación entrantes, incluida la ejecución de scripts externos, pueden usar dentro del grupo de recursos. Vea los grupos de recursos usados para SQL Server y scripts externos.

![Salida de la consulta de grupos de recursos](media/dmv-resource-pools.png "Salida de la consulta de grupos de recursos")

Ejecute la consulta siguiente para obtener esta salida. Para obtener más información sobre las vistas de administración dinámica utilizadas, vea [Sys. DM _ _resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) y [Sys. DM _ _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

La consulta devuelve las columnas siguientes:

| columna | Descripción |
|--------|-------------|
| pool_name | Nombre del grupo de recursos de servidor. SQL Server los grupos de recursos tienen el `SQL Server` prefijo y los grupos de recursos externos `External Pool`tienen el prefijo.
| total_cpu_usage_hours | El uso acumulado de la CPU en milisegundos desde que se restablecieron las estadísticas del regulador de recursos. |
| read_io_completed_total | El total de operaciones de E/S de lectura completadas desde que se restablecieron las estadísticas del regulador de recursos. |
| write_io_completed_total | El total de operaciones de E/S de escritura completadas desde que se restablecieron las estadísticas del regulador de recursos. |

## <a name="installed-packages"></a>Paquetes instalados

Puede ver los paquetes de R y Python instalados en SQL Server Machine Learning Services ejecutando un script de R o Python que los genera.

### <a name="installed-packages-for-r"></a>Paquetes instalados para R

Vea los paquetes de R instalados en SQL Server Machine Learning Services.

![Salida de los paquetes instalados para la consulta de R](media/dmv-installed-packages-r.png "Salida de los paquetes instalados para la consulta de R")

Ejecute la consulta siguiente para obtener esta salida. La consulta usa un script de R para determinar los paquetes de R instalados con SQL Server.

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

Las columnas devueltas son:

| columna | Descripción |
|--------|-------------|
| Paquete | Nombre del paquete instalado. |
| `Version` | Versión del paquete. |
| Depende | Enumera los paquetes de los que depende el paquete instalado. |
| Licencia | Licencia para el paquete instalado. |
| LibPath | Directorio en el que puede encontrar el paquete. |

### <a name="installed-packages-for-python"></a>Paquetes instalados para Python

Vea los paquetes de Python instalados en SQL Server Machine Learning Services.

![Salida de los paquetes instalados para la consulta de Python](media/dmv-installed-packages-python.png "Salida de los paquetes instalados para la consulta de Python")

Ejecute la consulta siguiente para obtener esta salida. La consulta usa un script de Python para determinar los paquetes de Python instalados con SQL Server.

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

Las columnas devueltas son:

| columna | Descripción |
|--------|-------------|
| Paquete | Nombre del paquete instalado. |
| `Version` | Versión del paquete. |
| Location | Directorio en el que puede encontrar el paquete. |

## <a name="next-steps"></a>Pasos siguientes

+ [Administración y supervisión de soluciones de aprendizaje automático](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [Eventos extendidos para machine learning](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Resource Governor vistas de administración dinámica relacionadas](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [Vistas de administración dinámica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Supervisión del aprendizaje automático mediante informes personalizados en Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
