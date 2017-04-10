---
title: "Inicializar autom&#225;ticamente grupos de disponibilidad Always On | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 67c6a601-677a-402b-b3d1-8c65494e9e96
caps.latest.revision: 18
ms.author: "v-saume"
manager: "jhubbard"
---
# Inicializar autom&#225;ticamente grupos de disponibilidad Always On
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


 SQL Server 2016 presenta la propagación automática de grupos de disponibilidad. Cuando se crea un grupo de disponibilidad con propagación automática, SQL Server crea automáticamente las réplicas secundarias para cada base de datos del grupo. Con la propagación automática ya no es necesario realizar copias de seguridad de las réplicas secundarias ni restaurarlas de forma manual. Para habilitar la propagación automática, cree el grupo de disponibilidad con T-SQL.
 
## Requisitos previos

La propagación automática exige que la ruta de acceso del archivo de datos y de registro sea la misma en cada instancia de SQL Server que participe en el grupo de disponibilidad. 

La propagación del grupo de disponibilidad se comunica a través del punto de conexión de creación de reflejo de la base de datos. Abra las reglas de firewall de entrada al puerto del punto de conexión de creación de reflejo en cada servidor.

Las bases de datos de un grupo de disponibilidad deben estar en modelo de recuperación completa. La base de datos debe tener una copia de seguridad completa actual y una copia de seguridad de registro de transacciones. Estos archivos de copia de seguridad no se usan para la propagación automática, pero son necesarios para incluir la base de datos en un grupo de disponibilidad. 
 
## Crear grupos de disponibilidad con propagación automática

Para crear un grupo de disponibilidad con propagación automática, establezca `SEEDING_MODE=AUTOMATIC`. 

En el ejemplo siguiente se crea un grupo de disponibilidad en un clúster de conmutación por error de dos nodos de Windows Server. Antes de ejecutar los scripts, actualice los valores del entorno.

1. Cree los puntos de conexión. Cada servidor necesitará un punto de conexión. El script siguiente crea un punto de conexión que usa el puerto TCP 5022 del agente de escucha. Establezca `<endpoint_name>` y `LISTENER_PORT` de modo que coincidan con el entorno y ejecute el script:

    ```
    --Create the endpoint on both servers
    -- Run this script twice, once on each server. 
    CREATE ENDPOINT [<endpoint_name>] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE, ENCRYPTION = REQUIRED ALGORITHM AES)
    GO
    ```

1. Cree el grupo de disponibilidad. El siguiente script crea el grupo de disponibilidad. Actualice los valores de nombre del grupo, nombres de servidores y nombres de dominios y ejecute en la instancia principal de SQL Server.  

    ```
    ---Run On Primary
    CREATE AVAILABILITY GROUP [<availability_group_name>]
    FOR DATABASE db1
    REPLICA ON'<*primary_server*>'
    WITH (ENDPOINT_URL = N'TCP://<primary_server>.<fully_qualified_domain_name>:5022', 
    FAILOVER_MODE = AUTOMATIC, 
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
    BACKUP_PRIORITY = 50, 
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
    SEEDING_MODE = AUTOMATIC),
    N'<secondary_server>' WITH (ENDPOINT_URL = N'TCP://<secondary_server>.<fully_qualified_domain_name>:5022', 
    FAILOVER_MODE = AUTOMATIC, 
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
    BACKUP_PRIORITY = 50, 
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
    SEEDING_MODE = AUTOMATIC);
    GO
    ``` 

1. Una el servidor secundario al grupo de disponibilidad y conceda permiso al grupo de disponibilidad para crear bases de datos. Ejecute el siguiente script en la instancia secundaria de SQL Server: 
 
    ```
    --Run on Secondary Replica to join to the availability group
    ALTER AVAILABILITY GROUP [<availability_group_name>] JOIN
    GO  
    ALTER AVAILABILITY GROUP [<availability_group_name>] GRANT CREATE ANY DATABASE
    GO
    ```

SQL Server creará automáticamente la réplica de base de datos en el servidor secundario. Si la base de datos es grande, puede llevar algún tiempo completar la sincronización de la base de datos. Si una base de datos está en un grupo de disponibilidad configurado para la propagación automática, puede consultar la vista del sistema `sys.dm_hadr_automatic_seeding` para supervisar el progreso de la propagación. La siguiente consulta devuelve una fila por cada base de datos que esté en un grupo de disponibilidad configurado para la propagación automática.

```
 SELECT start_time,
       ag.name,
       db.database_name,
       current_state,
       performed_seeding,
       failure_state,
       failure_state_desc
 FROM sys.dm_hadr_automatic_seeding autos 
    JOIN sys.availability_databases_cluster db ON autos.ag_db_id = db.group_database_id
    JOIN sys.availability_groups ag ON autos.ag_id = ag.group_id
```

## Evitar la propagación automática después de un grupo de disponibilidad

Para evitar temporalmente que la base de datos principal propague más bases de datos a la réplica secundaria, puede denegar al grupo de disponibilidad el permiso para crear bases de datos. Ejecute la consulta siguiente en la instancia que hospeda la réplica secundaria para denegar al grupo de disponibilidad el permiso para crear bases de datos de réplica.

```
ALTER AVAILABILITY GROUP [<availability_group_name>] DENY CREATE ANY DATABASE
GO
```


## Habilitar la propagación automática en un grupo de disponibilidad existente

Puede establecer la propagación automática en una base de datos existente. El siguiente comando modificará un grupo de disponibilidad para usar la propagación automática. 

```
ALTER AVAILABILITY GROUP [<availability_group_name>] 
MODIFY REPLICA ON '<primary_node>' WITH (SEEDING_MODE = AUTOMATIC)
GO
```

Esto obligará a una base de datos a reiniciar la propagación en caso necesario. Por ejemplo, si se produce un error de propagación debido a una insuficiencia de espacio en disco en la réplica secundaria, puede ejecutar `ALTER AVAILABILITY GROUP ... WITH (SEEDING_MODE=AUTOMATIC)` para reiniciar la propagación después de agregar espacio libre.

## Detener la propagación automática

Para detener la propagación automática de un grupo de disponibilidad, ejecute el siguiente script en la instancia que hospeda la réplica principal:

```
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    MODIFY REPLICA ON '<primary_node>'   
    WITH (SEEDING_MODE = MANUAL)
GO
```

Con esto se cancelarán las réplicas que se estén propagando en ese momento y se evitará que SQL Server inicialice automáticamente cualquier réplica en este grupo de disponibilidad. Esto no detendrá la sincronización de las réplicas que ya se hayan inicializado. 


## Supervisar grupos de disponibilidad de propagación automática

### Usar vistas de administración dinámica del sistema para supervisar la propagación

Las siguientes vistas del sistema muestran el estado de la propagación automática de SQL Server.

**sys.dm_hadr_automatic_seeding** 

En la réplica principal, consulte `sys.dm_hadr_automatic_seeding` para comprobar el estado del proceso de propagación automática. La vista devuelve una fila por cada proceso de propagación. Por ejemplo:

``` 
SELECT start_time, 
        completion_time
        is_source,
        current_state,
        failure_state,
        failure_state_desc
FROM sys.dm_hadr_automatic_seeding
```
 
**sys.dm_hadr_physical_seeding_stats** 

En la réplica principal, consulte la vista de administración dinámica `sys.dm_hadr_physical_seeding_stats` para ver las estadísticas físicas de cada proceso de propagación que se esté ejecutando en ese momento. La siguiente consulta devuelve filas cuando se está ejecutando la propagación:

```
SELECT * FROM sys.dm_hadr_physical_seeding_stats;
```

### Diagnosticar la inicialización de la base de datos mediante la propagación automática en el registro de errores

Al agregar una base de datos a un grupo de disponibilidad configurado para la propagación automática, SQL Server realiza una copia de seguridad VDI a través del punto de conexión del grupo de disponibilidad. Revise el registro de errores de SQL Server para obtener información sobre cuándo se completó la copia de seguridad y cuándo se sincronizó la secundaria.

### Diagnosticar el estado de nivel de base de datos con eventos extendidos

La propagación automática tiene nuevos eventos extendidos para realizar el seguimiento de las modificaciones de estado, los errores y las estadísticas de rendimiento durante la inicialización. 

Por ejemplo, este script crea una sesión de eventos extendidos que capture eventos relacionados con la propagación automática: 

```
CREATE EVENT SESSION [AlwaysOn_autoseed] ON SERVER 
    ADD EVENT sqlserver.hadr_automatic_seeding_state_transition,
    ADD EVENT sqlserver.hadr_automatic_seeding_timeout,
    ADD EVENT sqlserver.hadr_db_manager_seeding_request_msg,
    ADD EVENT sqlserver.hadr_physical_seeding_backup_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_failure,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_target_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_progress,
    ADD EVENT sqlserver.hadr_physical_seeding_restore_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_submit_callback
    ADD TARGET package0.event_file(SET filename=N’autoseed.xel’,max_file_size=(5),max_rollover_files=(4))
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)
GO 

ALTER EVENT SESSION AlwaysOn_autoseed ON SERVER STATE=START
GO 
```


La tabla siguiente enumera los eventos extendidos relacionados con la propagación automática: 

| Nombre | Descripción|
|------------ |---------------| 
|hadr_db_manager_seeding_request_msg |  Mensaje de solicitud propagación.
|hadr_physical_seeding_backup_state_change |    Cambio de estado del lado de copia de seguridad de propagación física.
|hadr_physical_seeding_restore_state_change |Cambio de estado del lado de restauración de propagación física.
|hadr_physical_seeding_forwarder_state_change | Cambio de estado del lado de reenviador de propagación física.
|hadr_physical_seeding_forwarder_target_state_change |  Cambio de estado del lado de destino de reenviador de propagación física.
|hadr_physical_seeding_submit_callback  |Evento de devolución de llamada del envío de propagación física.
|hadr_physical_seeding_failure  |Evento de error de propagación física.
|hadr_physical_seeding_progress |   Evento de progreso de propagación física.
|hadr_physical_seeding_schedule_long_task_failure   |Evento de error de tarea larga de programación de propagación física.
|hadr_automatic_seeding_start   |Se produce cuando se envía una operación de propagación automática.
|hadr_automatic_seeding_state_transition    |Se produce cuando cambia el estado de una operación de propagación automática.
|hadr_automatic_seeding_success |Se produce cuando se realiza correctamente una operación de propagación automática.
|hadr_automatic_seeding_failure |Se produce cuando se realiza una operación de propagación automática incorrectamente.
|hadr_automatic_seeding_timeout |Se produce cuando se agota el tiempo de espera de una operación de propagación automática.

### Otras consideraciones de solución de problemas

**Supervisar la finalización de la propagación automática**

Consulte `sys.dm_hadr_physical_seeding_stats` para ver los procesos de propagación automática en ejecución. La vista devuelve una fila por cada base de datos. Por ejemplo:

```
SELECT local_database_name, 
       role_desc, 
       internal_state_desc, 
       transfer_rate_bytes_per_second, 
       transferred_size_bytes, 
       database_size_bytes, 
       start_time_utc, 
       end_time_utc, estimate_time_complete_utc, 
       total_disk_io_wait_time_ms, 
       total_network_wait_time_ms, 
       is_compression_enabled 
FROM sys.dm_hadr_physical_seeding_stats
```

**Solucionar el problema de que una base de datos no aparezca en un grupo de disponibilidad configurado para la propagación automática**


Cuando una base de datos no aparece como parte de un grupo de disponibilidad con la propagación automática habilitada, es probable que hubiera un error en la propagación automática. Esto evita la adición de la base de datos al grupo de disponibilidad en la réplica principal y secundaria. Consulte `sys.dm_hadr_automatic_seeding` en las réplicas principal y secundaria. Por ejemplo, ejecute la consulta siguiente para identificar el estado de error de propagación automática.

```
SELECT start_time, 
       completion_time, 
       is_source, 
       current_state, 
       failure_state, 
       failure_state_desc, 
       error_code 
FROM sys.dm_hadr_automatic_seeding
```

## Propagación automática y consideraciones de rendimiento

SQL Server usa un número fijo de subprocesos para la propagación automática. En la instancia principal, SQL Server usa un subproceso por LUN para leer los cambios. En la instancia secundaria, SQL Server usa un subproceso por LUN para inicializar la base de datos.

Establezca la marca de seguimiento 9567 en la réplica principal para habilitar la compresión del flujo de datos durante la propagación automática. Esto puede reducir considerablemente el tiempo de transferencia de propagación automática, aunque también aumentará el uso de CPU. Para obtener más información, consulte [Tune compression for availability group (Optimizar la compresión para el grupo de disponibilidad)](../../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md). 


## Cuándo no usar la propagación automática

En algunos casos, la propagación automática puede no ser óptima para inicializar una réplica secundaria. Durante la propagación automática, SQL Server realiza una copia de seguridad a través de la red para la inicialización. Este proceso puede ser lento si las bases de datos son muy grandes o si la réplica secundaria es remota. No se puede truncar el registro de transacciones de estas bases de datos durante el proceso de copia de seguridad, por lo que un proceso de inicialización prolongado en una base de datos ocupada puede dar lugar a un crecimiento considerable del registro de transacciones.
Antes de agregar una base de datos a un grupo de disponibilidad con propagación automática, evalúe el tamaño de la base de datos, la carga y la distancia al sitio entre réplicas.

## Recursos

[CREATE AVAILABILITY GROUP (Transact-SQL)
-](https://msdn.microsoft.com/library/ff878399.aspx)

[AlwaysOn Availability Groups Troubleshooting and Monitoring Guide (Guía de solución de problemas y supervisión de grupos de disponibilidad AlwaysOn)](http://technet.microsoft.com/library/dn135328.aspx)
