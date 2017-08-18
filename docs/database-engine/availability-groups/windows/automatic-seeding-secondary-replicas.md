---
title: "Propagación automática de las réplicas secundarias (SQL Server) | Microsoft Docs"
description: "Use la propagación automática para inicializar réplicas secundarias."
services: data-lake-analytics
ms.custom: 
ms.date: 06/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Automatic seeding [SQL Server], secondary replica
ms.assetid: 
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1b72f9f5bf58f72bb4284b1a6cc8d0af7a722aed
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="automatic-seeding-for-secondary-replicas"></a>Propagación automática de réplicas secundarias

[!INCLUDE [tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

En SQL Server 2012 y 2014, la única manera de inicializar una réplica secundaria en un grupo de disponibilidad es recurriendo a los trabajos de copia de seguridad, copia y restauración. SQL Server 2016 incorpora una nueva característica para inicializar una réplica secundaria: la *propagación automática*. La propagación automática emplea el transporte de secuencia de registro para transmitir la copia de seguridad con VDI a la réplica secundaria de cada base de datos del grupo de disponibilidad que use los puntos de conexión configurados. Esta nueva característica se puede usar durante la creación inicial de un grupo de disponibilidad o cuando una base de datos se agrega a uno de estos grupos. La propagación automática se incluye en todas las ediciones de SQL Server que admiten grupos de disponibilidad AlwaysOn, y se puede usar tanto con los grupos de disponibilidad tradicionales como con los [grupos de disponibilidad distribuidos](distributed-availability-groups.md).

## <a name="considerations"></a>Consideraciones

Hay que considerar los siguientes aspectos al usar la propagación automática:

* [Impacto en el rendimiento y el registro de transacciones de la réplica principal](#performance-and-transaction-log-impact-on-the-primary-replica)
* [Diseño de disco](#disk-layout)
* [Seguridad](#security)


### <a name="performance-and-transaction-log-impact-on-the-primary-replica"></a>Impacto en el rendimiento y el registro de transacciones de la réplica principal

La propagación automática puede ser o no práctica a la hora de inicializar una réplica secundaria, según cuál sea el tamaño de la base de datos, la velocidad de red y la distancia entre las réplicas principales y las secundarias. Por ejemplo, en estas circunstancias:

* El tamaño de la base de datos es de 5 TB.
* La velocidad de red es de 1 Gb/s.
* La distancia entre los dos sitios es de 1000 millas.

Una red de 1 Gb/s puede proporcionar un rendimiento sostenido de 125 MB/s si está disponible el ancho de banda completo. En este ejemplo, la propagación automática podría tardar tan solo alrededor de 11 horas. En la práctica, el proceso de propagación automática es un poco más lento, dado que las señales de red se deterioran cuando las distancias son largas y el vínculo se suele compartir con otros recursos de la red. Durante la propagación, el registro de transacciones en la base de datos de la réplica principal continuará creciendo y no se puede truncar hasta que la propagación automática de esa base de datos se complete.  Cuando esto suceda, el registro de transacciones se puede truncar usando una copia de seguridad del registro de transacciones.

La propagación automática es un proceso de un único subproceso que puede asumir hasta cinco bases de datos. Esto puede afectar al rendimiento, especialmente si el grupo de disponibilidad tiene más de una base de datos.

La compresión se puede usar en la propagación automática, pero está deshabilitada de forma predeterminada. Si la compresión se activa, se reducirá el ancho de banda de red y, posiblemente, el proceso se acelere, pero a cambio habrá una mayor sobrecarga del procesador. Para usar la compresión durante la propagación automática, habilite la marca de seguimiento 9567; vea [Tune compression for availability group](tune-compression-for-availability-group.md) (Optimizar la compresión para los grupos de disponibilidad).

### <a name="disk-layout"></a>Diseño de disco

La carpeta donde se va a crear la base de datos a través de la propagación automática ya debe existir y ser la misma que la ruta de acceso de la réplica principal.

### <a name="security"></a>Seguridad

Los permisos de seguridad varían según el tipo de réplica que se esté inicializando:

* Si es un grupo de disponibilidad tradicional, el grupo de disponibilidad en la réplica secundaria debe tener concedidos permisos, ya que está unido al grupo de disponibilidad. En Transact-SQL, use el comando ALTER AVAILABILITY GROUP [nombre del grupo de disponibilidad] GRANT CREATE ANY DATABASE.
* En el caso de un grupo de disponibilidad distribuido, en el que las bases de datos de la réplica que se van a crear se encuentran en la réplica principal del segundo grupo de disponibilidad, no se requiere ningún permiso adicional, puesto que ya es un elemento principal.
* En el caso de una réplica secundaria en el segundo grupo de disponibilidad de un grupo de disponibilidad distribuido, se debe usar el comando ALTER AVAILABILITY GROUP [nombre del segundo grupo de disponibilidad] GRANT CREATE ANY DATABASE. Esta réplica secundaria se propagará desde el elemento principal del segundo grupo de disponibilidad.

## <a name="create-an-availability-group-with-automatic-seeding"></a>Crear un grupo de disponibilidad con propagación automática

Puede crear un grupo de disponibilidad a través de la propagación automática con Transact-SQL o SQL Server Management Studio (SSMS, versión 17 o posterior). Para usar el Asistente para nuevo grupo de disponibilidad en SSMS, siga [estas instrucciones](use-the-availability-group-wizard-sql-server-management-studio.md); cuando llegue al paso 9, verá la propagación automática como primera opción (que es, además, la predeterminada).

![Seleccionar sincronización de datos iniciales][1]

En el siguiente ejemplo se crea un grupo de disponibilidad con Transact-SQL. Vea también el tema [Crear un grupo de disponibilidad (Transact-SQL)](create-an-availability-group-transact-sql.md). La propagación se habilita en una réplica secundaria estableciendo la opción SEEDING_MODE en AUTOMATIC. El comportamiento predeterminado es MANUAL, que es anterior al comportamiento que existía antes de SQL Server 2016 y que precisa que se haga una copia de seguridad de la base de datos en la réplica principal, una copia del archivo de copia de seguridad en la réplica secundaria y una restauración de la copia de seguridad con la opción WITH NORECOVERY.

```
CREATE AVAILABILITY GROUP [AGName]
  FOR DATABASE db1
  REPLICA ON N'Primary_Replica'
WITH (
  ENDPOINT_URL = N'TCP://Primary_Replica.Contoso.com:5022', 
  FAILOVER_MODE = AUTOMATIC, 
  AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
),
  N'Secondary_Replica' WITH (
    ENDPOINT_URL = N'TCP://Secondary_Replica.Contoso.com :5022', 
    FAILOVER_MODE = AUTOMATIC, 
    SEEDING_MODE = AUTOMATIC);
 GO
```

Establecer SEEDING_MODE en una réplica principal durante la instrucción CREATE AVAILABILITY GROUP no tiene ningún efecto, porque la réplica principal ya contiene la copia principal de lectura/escritura de la base de datos. SEEDING_MODE solo procede cuando otra réplica se ha convertido en principal y se le ha agregado una base de datos. El modo de propagación se puede cambiar posteriormente; vea [Cambiar el modo de propagación de una réplica](#change-the-seeding-mode-of-a-replica).

En el caso de una instancia que pasa a ser una réplica secundaria, una vez que dicha instancia se une, se agrega el siguiente mensaje en el registro de SQL Server:

La réplica de disponibilidad local para el grupo de disponibilidad 'nombre del grupo de disponibilidad' no tiene permiso para crear bases de datos, pero su modo SEEDING_MODE se definió como AUTOMATIC. Use el comando ALTER AVAILABILITY GROUP … GRANT CREATE ANY DATABASE para permitir la creación de bases de datos propagadas por la réplica de disponibilidad principal.

Tras la unión, emita la siguiente instrucción:

```
ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE
 GO
````

> [!NOTE] 
> Desde SQL Server 2016 SP1 CU2 existe un problema conocido por el cual una réplica secundaria debe esperar tres minutos para que el grupo de disponibilidad pueda propagar la base de datos antes de ejecutar una instrucción ALTER AVAILABILITY GROUP... Antes de que transcurra ese tiempo, la instrucción no devolverá un error, sino que indicará que todo es correcto. Esto es también un problema conocido. Estos problemas se corregirán en una futura actualización de SQL Server. Como solución temporal, inserte una instrucción WAITFOR:

```
WAITFOR DELAY '00:03:15';
ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE;
GO
```

Si se realiza correctamente, las bases de datos se crean automáticamente en la réplica secundaria con uno de los dos siguientes estados:

* SYNCHRONIZED, si la réplica secundaria está configurada para ser sincrónica y los datos se han sincronizado completamente.
* SYNCHRONIZING, si la réplica secundaria está configurada con un movimiento de datos asincrónico, o bien si está configurada como sincrónica, pero aún no se ha sincronizado con la réplica principal.

<a name="sql-server-log"></a> Aparte de las [vistas de administración dinámica](#dynamic-management-views) descritas aquí, el inicio y la finalización de la propagación automática se pueden ver en el registro de SQL Server:

![Registro de SQL Server][2]

## <a name="combine-backup-and-restore-with-automatic-seeding"></a>Combinar trabajos de copia de seguridad y restauración con la propagación automática

La propagación automática se puede usar de forma combinada con los trabajos tradicionales de copia de seguridad, copia y restauración. En tal caso, restaure primero la base de datos en una réplica secundaria, incluidos todos los registros de transacciones disponibles. Tras ello, habilite la propagación automática cuando cree el grupo de disponibilidad para "detectar" la base de datos de la réplica secundaria, como si se restaurara una copia del final del registro (vea [Copias del final del registro (SQL Server)](../../../relational-databases/backup-restore/tail-log-backups-sql-server.md)).

## <a name="add-a-database-to-an-availability-group-with-automatic-seeding"></a>Agregar una base de datos a un grupo de disponibilidad con propagación automática

Puede agregar una base de datos a un grupo de disponibilidad a través de la propagación automática con Transact-SQL o SQL Server Management Studio (SSMS, versión 17 o posterior).
Si la réplica secundaria usaba la propagación automática cuando se agregó al grupo de disponibilidad, no será necesario hacer nada más. Si se usó un trabajo de copia de seguridad, copia y restauración, cambie primero el modo de propagación (vea la sección siguiente) y, luego, al agregar la base de datos, use la instrucción GRANT; vea [Grupo de disponibilidad: agregar una base de datos](availability-group-add-a-database.md).

## <a name="change-the-seeding-mode-of-a-replica"></a>Cambiar el modo de propagación de una réplica

El modo de propagación de una réplica se puede modificar después de haber creado el grupo de disponibilidad, de forma que la propagación automática se pueda habilitar o deshabilitar. Habilitar la propagación automática después de haber creado el grupo de disponibilidad permite agregar una base de datos al grupo de disponibilidad por medio de la propagación automática, si se creó con copia de seguridad, copia y restauración. Por ejemplo:

```
ALTER AVAILABILITY GROUP [AGName]
  MODIFY REPLICA ON 'Replica_Name'
  WITH (SEEDING_MODE = AUTOMATIC)
```

Para deshabilitar la propagación automática, use el valor MANUAL.

## <a name="prevent-automatic-seeding-after-an-availability-group-is-created"></a>Evitar la propagación automática después de crear un grupo de disponibilidad

Si no quiere deshabilitar la propagación automática por completo en una réplica secundaria, pero sí impedir temporalmente que dicha réplica secundaria pueda crear bases de datos automáticamente, deniegue el permiso de creación de grupos de disponibilidad. Esto sucede cuando una base de datos nueva se agrega al grupo de disponibilidad, pero el grupo de disponibilidad no debe tener permisos para crear la base de datos en una réplica secundaria.

```
ALTER AVAILABILITY GROUP [AGName] DENY CREATE ANY DATABASE
GO
```

## <a name="monitor-automatic-seeding"></a>Supervisar la propagación automática

Existen cuatro elementos con los que se puede supervisar la propagación automática y solucionar problemas al respecto:

* [Registro de SQL Server](#sql-server-log), como ya hemos explicado
* [Vistas de administración dinámica](#dynamic-management-views)
* [Tablas del historial de copias de seguridad](#backup-history-tables)
* [Eventos extendidos](#extended-events)

### <a name="dynamic-management-views"></a>Vistas de administración dinámica

Hay dos vistas de administración dinámica (DMV) para supervisar la propagación: sys.dm_hadr_automatic_seeding y sys.dm_hadr_physical_seeding_stats.

* sys.dm_hadr_automatic_seeding contiene el estado general de la propagación automática y conserva un historial de cada vez que se ejecuta (si lo hace correctamente o no). La columna current_state reflejará los valores COMPLETED o FAILED. Si el valor es FAILED, use el valor en failure_state_desc para tratar de diagnosticar el problema. Puede que sea necesario combinar esta información con lo que aparece en el [registro de SQL Server](#sql-server-log) para saber qué ha ido mal. Esta DMV se rellena en la réplica principal y en todas las réplicas secundarias.

* sys.dm_hadr_physical_seeding_stats muestra el estado de la operación de propagación automática cuando se ejecuta. Al igual que sucede con sys.dm_hadr_automatic_seeding, mostrará los valores en las réplicas principal y secundarias, pero en este caso el historial no se almacena. Los valores se corresponden únicamente con la ejecución actual y no se conservarán. Las columnas de interés son start_time_utc, end_time_utc, estimate_time_complete_utc, total_disk_io_wait_time_ms, total_network_wait_time_ms y, si se produce un error en la operación de propagación, failure_message.

### <a name="backup-history-tables"></a>Tablas del historial de copias de seguridad

La propagación automática también agrega entradas en las tablas `msdb` que almacenan el historial de las copias de seguridad y las restauraciones. En la réplica secundaria que recibe la propagación automática, la columna physical_device_name de la tabla `backupmediafamily` contiene un GUID relativo a su valor, y la entrada correspondiente en `backupset` refleja el nombre de la réplica principal para nombre_servidor y nombre_equipo.

### <a name="extended-events"></a>Eventos extendidos

La propagación automática agrega nuevos eventos extendidos para realizar el seguimiento de las modificaciones de estado, los errores y las estadísticas de rendimiento durante la inicialización.
Por ejemplo, con el siguiente script se crea una sesión de eventos extendidos que capture eventos relacionados con la propagación automática.

```
CREATE EVENT SESSION [AG_autoseed] ON SERVER 
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

En la siguiente tabla se enumeran los eventos extendidos relacionados con la propagación automática.

|Nombre|Descripción|
|----|-----------|
|hadr_db_manager_seeding_request_msg|Mensaje de solicitud propagación.|
|hadr_physical_seeding_backup_state_change|Cambio de estado del lado de copia de seguridad de propagación física.|
|hadr_physical_seeding_restore_state_change|Cambio de estado del lado de restauración de propagación física.|
|hadr_physical_seeding_forwarder_state_change|Cambio de estado del lado de reenviador de propagación física.|
|hadr_physical_seeding_forwarder_target_state_change|Cambio de estado del lado de destino de reenviador de propagación física.|
|hadr_physical_seeding_submit_callback|Evento de devolución de llamada del envío de propagación física.|
|hadr_physical_seeding_failure|Evento de error de propagación física.|
|hadr_physical_seeding_progress|Evento de progreso de propagación física.|
|hadr_physical_seeding_schedule_long_task_failure|Evento de error de tarea larga de programación de propagación física.|
|hadr_automatic_seeding_start|Se produce cuando se envía una operación de propagación automática.|
|hadr_automatic_seeding_state_transition|Se produce cuando cambia el estado de una operación de propagación automática.|
|hadr_automatic_seeding_success|Se produce cuando se realiza correctamente una operación de propagación automática.|
|hadr_automatic_seeding_failure|Se produce cuando se realiza una operación de propagación automática incorrectamente.|
|hadr_automatic_seeding_timeout|Se produce cuando se agota el tiempo de espera de una operación de propagación automática.|

## <a name="see-also"></a>Vea también

[ALTER AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql)

[CREATE AVAILABILITY GROUP (Transact-SQL)](https://msdn.microsoft.com/library/ff878399.aspx)

[Guía de solución de problemas y supervisión de grupos de disponibilidad AlwaysOn](http://technet.microsoft.com/library/dn135328.aspx)

> Contenido escrito por [Allan Hirt](http://mvp.microsoft.com/en-us/PublicProfile/4025254?fullName=Allan%20Hirt), profesional más valioso (MVP) de Microsoft.

<!--Image references-->
[1]: ./media/auto-seed-new-availability-group.png
[2]: ./media/auto-seed-sql-server-log.png

