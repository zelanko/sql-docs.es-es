---
title: Supervisar el uso de vistas de administración dinámica (DMV) de SQL Server Machine Learning Services | Microsoft Docs
description: Usar vistas de administración dinámica (DMV) para supervisar SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: aa05c78f8bac4af5187b815126e0ec9e4b6fff4e
ms.sourcegitcommit: c2322c1a1dca33b47601eb06c4b2331b603829f1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/01/2018
ms.locfileid: "50743458"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>Supervisar el uso de vistas de administración dinámica (DMV) de SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Use secuencias de comandos de vistas de administración dinámica (DMV) para supervisar la ejecución de externo (R y Python), de los recursos utilizados, diagnosticar problemas y optimizar el rendimiento en SQL Server Machine Learning Services.

En este artículo, encontrará las DMV que son específicas de SQL Server Machine Learning Services. También encontrará las consultas de ejemplo que muestran:

+ Opciones de configuración para el aprendizaje automático
+ Sesiones activas de ejecución de scripts de R o Python externos
+ Estadísticas de ejecución para el tiempo de ejecución externo para R y Python
+ Contadores de rendimiento de scripts externos
+ Uso de memoria para el sistema operativo, SQL Server y grupos de recursos externos
+ Configuración de memoria para SQL Server y grupos de recursos externos
+ Grupos de recursos del regulador de recursos, incluidos los grupos de recursos externos
+ Paquetes instalados de R y Python

Para obtener información general sobre las DMV, vea [vistas de administración dinámica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).

> [!TIP]
> También puede usar los informes personalizados para supervisar SQL Server Machine Learning Services. Para obtener más información, consulte [supervisar machine learning con informes personalizados en Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="dynamic-management-views"></a>Vistas de administración dinámica

Las siguientes vistas de administración dinámica pueden usarse para supervisar cargas de trabajo de machine learning en SQL Server. Para consultar las DMV, necesita `VIEW SERVER STATE` permiso en la instancia.

| Vista de administración dinámica | Tipo | Descripción |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | Ejecución | Devuelve una fila para cada cuenta de trabajo activa que ejecuta un script externo. |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | Ejecución | Devuelve una fila por cada tipo de solicitud de script externo. |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | Ejecución | Devuelve una fila por contador de rendimiento que se mantiene en el servidor. Si usa la condición de búsqueda `WHERE object_name LIKE '%External Scripts%'`, puede usar esta información para ver cuántos scripts se ejecutaron, que se ejecutaron mediante el modo de autenticación, o cuántas R o llamadas de Python que se emitieron en la instancia global. |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | regulador de recursos | Devuelve información sobre el estado actual del grupo de recursos externos en el regulador de recursos, la configuración actual de los grupos de recursos y las estadísticas del grupo de recursos. |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | regulador de recursos | Devuelve información de afinidad de CPU sobre la configuración actual del grupo de recursos externos en el regulador de recursos. Devuelve una fila por programador en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] donde cada programador está asignado a un determinado procesador. Use esta vista para supervisar la condición de un programador o identificar tareas descontroladas. |

Para obtener información acerca de la supervisión [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancias, consulte [vistas de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) y [Resource Governor relacionados vistas de administración dinámica](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="settings-and-configuration"></a>Opciones y configuración

Ver las opciones de configuración y la configuración de la instalación de Machine Learning Services.

![Salida de la configuración y la consulta de la configuración](media/dmv-settings-and-configuration.png "de salida de la configuración y la consulta de la configuración")

Ejecute la consulta siguiente para obtener este resultado. Para obtener más información sobre las vistas y funciones que se usan, vea [sys.dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md), y [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md).

```SQL
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
| IsMLServicesInstalled | Devuelve 1 si está instalado SQL Server Machine Learning Services para la instancia. En caso contrario, devuelve 0. |
| ExternalScriptsEnabled | Devuelve 1 si los scripts externos está habilitada para la instancia. En caso contrario, devuelve 0. |
| ImpliedAuthenticationEnabled | Devuelve 1 si la autenticación implícita está habilitado. En caso contrario, devuelve 0. Comprobando si existe un inicio de sesión para SQLRUserGroup, se comprueba la configuración para la autenticación implícita. |
| IsTcpEnabled | Devuelve 1 si el protocolo TCP/IP está habilitado para la instancia. En caso contrario, devuelve 0. Para obtener más información, consulte [predeterminado de configuración de protocolo de SQL Server Network](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md). |

## <a name="active-sessions"></a>Sesiones activas

Ver las sesiones activas de ejecución de scripts externos.

![Salida de la consulta de la configuración activa](media/dmv-active-sessions.png "de salida de la consulta de la configuración activa")

Ejecute la consulta siguiente para obtener este resultado. Para obtener más información sobre las vistas de administración dinámica usa, consulte [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md), [sys.dm_external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md), y [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).

```SQL
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
| database_name | Nombre de la base de datos actual para cada sesión. |
| login_name | Nombre de inicio de sesión de SQL Server en el que se está ejecutando la sesión. |
| wait_time | Si la solicitud está actualmente bloqueada, esta columna devuelve la duración en milisegundos de la espera actual. No admite valores NULL. |
| wait_type | Si la solicitud está actualmente bloqueada, esta columna devuelve el tipo de espera. Para obtener información acerca de los tipos de esperas, vea [sys.dm_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). |
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

Ver las estadísticas de ejecución externos en tiempo de ejecución de R y Python. Solo estadísticas de RevoScaleR, revoscalepy o funciones de microsoftml paquete están disponibles actualmente.

![Salida de la consulta de las estadísticas de ejecución](media/dmv-execution-statistics.png "de salida de la consulta de las estadísticas de ejecución")

Ejecute la consulta siguiente para obtener este resultado. Para obtener más información sobre la vista de administración dinámica utilizada, consulte [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). La consulta devuelve sólo las funciones que se han ejecutado más de una vez.

```SQL
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

Ver los contadores de rendimiento relacionados con la ejecución de scripts externos.

![Consulta de contadores de salida desde el rendimiento](media/dmv-performance-counters.png "salida desde el rendimiento de una consulta de contadores")

Ejecute la consulta siguiente para obtener este resultado. Para obtener más información sobre la vista de administración dinámica utilizada, consulte [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md).

```SQL
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**Sys.dm_os_performance_counters** genera los siguientes contadores de rendimiento para los scripts externos:

| Contador | Descripción |
|---------|-------------|
| Ejecuciones totales | Número de procesos externos iniciados por llamadas locales o remotas. |
| Ejecuciones en paralelo | Número de veces que un script incluyó la _@parallel_ especificación y que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] fue capaz de generar y usar un plan de consulta en paralelo. |
| Ejecuciones de streaming | Número de veces que se ha invocado la característica de transmisión por secuencias. |
| Ejecuciones CC de SQL | Número de scripts externos que ejecutan SQL Server y donde la llamada se crea una instancia de forma remota se ha usado como el contexto de cálculo. |
| Autenticación implícita. Inicios de sesión | Número de veces que se realizó una llamada de bucle invertido ODBC mediante autenticación implícita; es decir, el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ejecuta la llamada en nombre de usuario que envía la solicitud de script. |
| Tiempo total de ejecución (ms) | Tiempo transcurrido entre la llamada y la finalización de llamada. |
| Errores de ejecución | Número de veces que los scripts informaron de errores. Este recuento no incluye errores de R o Python. |

## <a name="memory-usage"></a>Uso de la memoria

Ver información acerca de la memoria utilizada por el sistema operativo, SQL Server y los grupos externos.

![Salida de la consulta de uso de memoria](media/dmv-memory-usage.png "de salida de la consulta de uso de memoria")

Ejecute la consulta siguiente para obtener este resultado. Para obtener más información sobre las vistas de administración dinámica usa, consulte [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) y [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md).

```SQL
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
| committed_kb | La memoria asignada en kilobytes (KB) en el Administrador de memoria. No incluye la memoria reservada del administrador de memoria. |
| external_pool_peak_memory_kb | La suma de la la cantidad máxima de memoria utilizada, en kilobytes, para todos los grupos de recursos externos. |

## <a name="memory-configuration"></a>Configuración de la memoria

Ver información sobre la configuración de memoria máxima en porcentaje de SQL Server y grupos de recursos externos. Si se está ejecutando SQL Server con el valor predeterminado de `max server memory (MB)`, se considera el 100% de la memoria del sistema operativo.

![Salida de la consulta de la configuración de memoria](media/dmv-memory-configuration.png "de salida de la consulta de la configuración de memoria")

Ejecute la consulta siguiente para obtener este resultado. Para obtener más información sobre las vistas que se usan, vea [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) y [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```SQL
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
| NAME | Nombre del grupo de recursos externos o SQL Server. |
| max_memory_percent | La memoria máxima que puede usar SQL Server o el grupo de recursos externos. |

## <a name="resource-pools"></a>Grupos de recursos de servidor

En [regulador de recursos de SQL Server](../../relational-databases/resource-governor/resource-governor.md), un [grupo de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md) representa un subconjunto de los recursos físicos de una instancia. Puede especificar límites sobre la cantidad de CPU, E/S física y memoria que las solicitudes de aplicación entrantes, incluida la ejecución de scripts externos, pueden utilizar en el grupo de recursos. Ver los grupos de recursos que se usa para SQL Server y scripts externos.

![Consulta de grupos de salida desde el recurso](media/dmv-resource-pools.png "salida desde el recurso de grupos de consulta")

Ejecute la consulta siguiente para obtener este resultado. Para obtener más información sobre las vistas de administración dinámica usa, consulte [sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) y [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```SQL
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
| pool_name | Nombre del grupo de recursos de servidor. Los grupos de recursos de SQL Server tienen el prefijo `SQL Server` y grupos de recursos externos tienen el prefijo `External Pool`.
| total_cpu_usage_hours | El uso de CPU acumulado en milisegundos desde que se restablecieron las estadísticas del regulador de recursos. |
| read_io_completed_total | El total de operaciones de E/S de lectura completadas desde que se restablecieron las estadísticas del regulador de recursos. |
| write_io_completed_total | El total de operaciones de E/S de escritura completadas desde que se restablecieron las estadísticas del regulador de recursos. |

## <a name="installed-packages"></a>Paquetes instalados

Puede para ver los paquetes de R y Python que están instalados en SQL Server Machine Learning Services mediante la ejecución de un script de R o Python que da como resultado de estos.

### <a name="installed-packages-for-r"></a>Instala los paquetes de R

Ver los paquetes de R instalados en SQL Server Machine Learning Services.

![Salida de los paquetes instalados para consulta R](media/dmv-installed-packages-r.png "de salida de los paquetes instalados para consulta de R")

Ejecute la consulta siguiente para obtener este resultado. El uso de consultas de un script de R para determinar los paquetes de R se instala con SQL Server.

```SQL
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
| Versión | Versión del paquete. |
| Depende | Enumera los paquetes que depende el paquete instalado. |
| Licencia | Licencia para el paquete instalado. |
| LibPath | Directorio donde puede encontrar el paquete. |

### <a name="installed-packages-for-python"></a>Los paquetes instalados para Python

Ver los paquetes de Python instalados en SQL Server Machine Learning Services.

![Salida de los paquetes instalados para consulta Python](media/dmv-installed-packages-python.png "de salida de los paquetes instalados para consulta de Python")

Ejecute la consulta siguiente para obtener este resultado. La consulta use un script de Python para determinar los paquetes de Python instalados con SQL Server.

```SQL
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
| Versión | Versión del paquete. |
| Ubicación | Directorio donde puede encontrar el paquete. |

## <a name="next-steps"></a>Pasos siguientes

+ [Administración y supervisión de soluciones de aprendizaje automático](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [Eventos extendidos para el aprendizaje automático](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Vistas de administración dinámica relacionadas con el regulador de recursos](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [Vistas de administración dinámica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Supervisar machine learning con informes personalizados en Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)