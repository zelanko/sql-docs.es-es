---
title: Configurar grupo de disponibilidad de escalado horizontal de lectura para SQL Server en Linux | Documentos de Microsoft
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf249ff8e6d2e82d1cf413bdec0272e3796b72cb
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---

# <a name="configure-read-scale-out-availability-group-for-sql-server-on-linux"></a>Configurar grupo de disponibilidad de escalado horizontal de lectura para SQL Server en Linux

Puede configurar un grupo de disponibilidad de escalabilidad horizontal de lectura de SQL Server en Linux. Hay dos arquitecturas para grupos de disponibilidad. A *alta disponibilidad* arquitectura utiliza un administrador de clústeres para proporcionar mejor continuidad del negocio. Esta arquitectura también puede incluir lecturas réplicas de escalabilidad horizontal. Para crear la arquitectura de alta disponibilidad, consulte [Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md).

Este documento explica cómo crear un *lectura escalabilidad* grupo de disponibilidad sin un administrador de clústeres. Esta arquitectura proporciona solo solo lectura de escala horizontal. No proporciona alta disponibilidad.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Crear el grupo de disponibilidad

Cree el grupo de disponibilidad. Set `CLUSTER_TYPE = NONE`. Además, establecer cada réplica con `FAILOVER_MODE = NONE`. Aplicaciones de cliente análisis o informes de las cargas de trabajo directamente pueden conectarse a bases de datos secundarias. También puede crear una lista de enrutamiento de solo lectura. Las conexiones a la réplica principal al día leen las solicitudes de conexión a cada una de las réplicas secundarias de la lista de enrutamiento en un modo de operación por turnos.

El script de Transact-SQL siguiente crea un nombre de grupo de disponibilidad `ag1`. La secuencia de comandos configura las réplicas del grupo de disponibilidad con `SEEDING_MODE = AUTOMATIC`. Esta configuración hace que SQL Server crear automáticamente la base de datos en cada servidor secundario después de agregarse al grupo de disponibilidad. Actualice el siguiente script para su entorno. Reemplace el `**<node1>**` y `**<node2>**` valores con los nombres de las instancias de SQL Server que hospedan las réplicas. Reemplace el `**<5022>**` con el puerto definido para el extremo. Ejecute el código Transact-SQL siguiente en la réplica principal de SQL Server:

```Transact-SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'**<node1>**' WITH (
            ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'**<node2>**' WITH ( 
            ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-availability-group"></a>Unir los servidores secundarios de SQL al grupo de disponibilidad

El siguiente script de Transact-SQL une a un servidor a un grupo de disponibilidad denominado `ag1`. Actualizar la secuencia de comandos para su entorno. En cada réplica de SQL Server, ejecute el siguiente Transact-SQL para unirse al grupo de disponibilidad.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

No se trata de una configuración de alta disponibilidad, si necesita alta disponibilidad, siga las instrucciones de [Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md). En concreto, cree el grupo de disponibilidad con `CLUSTER_TYPE=WSFC` (en Windows) o `CLUSTER_TYPE=EXTERNAL` (en Linux) e integrar con un administrador de clúster - a WSFC en Windows o bien marcapasos en Linux.

## <a name="connect-to-read-only-secondary-replicas"></a>Conectarse a réplicas secundarias de solo lectura

Hay dos formas de conectarse a las réplicas secundarias de solo lectura. Las aplicaciones pueden conectarse directamente a la instancia de SQL Server que hospeda la réplica secundaria y consultar las bases de datos, o pueden utilizar el enrutamiento de solo lectura. enrutamiento de solo lectura, requiere un agente de escucha.

[Réplicas secundarias legibles](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[enrutamiento de solo lectura](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-out-availability-group"></a>Conmutar por error la réplica principal en el grupo de disponibilidad de escalabilidad horizontal de lectura

Cada grupo de disponibilidad tiene solo una réplica principal. La réplica principal permite lecturas y escrituras. Para cambiar qué réplica es el principal, puede conmutar por error. En un grupo de disponibilidad para lograr alta disponibilidad, el Administrador de clústeres automatiza el proceso de conmutación por error. En un grupo de disponibilidad de escalabilidad horizontal de lectura, el proceso de conmutación por error es manual. Hay dos maneras para conmutar la réplica principal en un grupo de disponibilidad de la escala de lectura.

- Error manual se fuerza con pérdida de datos

- Conmutar por error manual sin pérdida de datos

### <a name="forced-fail-over-with-data-loss"></a>Forzada conmutación por error con pérdida de datos

Use este método cuando la réplica principal no está disponible y no se puede recuperar. También puede encontrar más información acerca de la conmutación por error forzada con pérdida de datos en [realizar una conmutación por error de Manual de forzada](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).

Para forzar un error sobre con pérdida de datos, conéctese a la instancia SQL que hospeda la réplica secundaria de destino y ejecute:
```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-fail-over-without-data-loss"></a>Conmutar por error manual sin pérdida de datos

Use este método cuando la réplica principal está disponible, pero debe temporal o permanentemente, cambiar la configuración y cambiar la instancia de SQL Server que hospeda la réplica principal. Antes de emitir por error manual sobre, asegúrese de que la réplica secundaria de destino está actualizada, por lo que no hay ninguna pérdida de datos. 

Los pasos siguientes describen cómo conmutación por error manual sin pérdida de datos:

1. Realizar la confirmación sincrónica de réplica secundaria de destino.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] MODIFY REPLICA ON N'**<node2>*' WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```
1. Actualización `required_synchronized_secondaries_to_commit`en 1.

   Este valor garantiza que todas las transacciones activas se compromete a la réplica principal y al menos un elemento secundario sincrónico. El grupo de disponibilidad está listo para conmutar por error cuando se SINCRONIZA el synchronization_state_desc y el sequence_number es el mismo para ambos principal y la réplica secundaria de destino. Ejecute esta consulta para comprobar:

   ```Transact-SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

1. Disminuir el nivel de la réplica principal a réplica secundaria. Después de que la réplica principal se degrada, es de solo lectura. Ejecute este comando en la instancia SQL que hospeda la réplica principal para actualizar el rol secundario:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY); 
   ```

1. Promover la réplica secundaria de destino a principal. 

   ```Transact-SQL
   ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > Para eliminar un grupo de disponibilidad, use [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Para un grupo de disponibilidad creado con CLUSTER_TYPE ninguno o externa, el comando debe ejecutarse en parte de todas las réplicas del grupo de disponibilidad.

## <a name="next-steps"></a>Pasos siguientes

[Configurar grupo de disponibilidad distribuido](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[Más información acerca de los grupos de disponibilidad](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)


