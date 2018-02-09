---
title: "Forzar la conmutación por error para el grupo de disponibilidad de SQL Server"
description: "Forzar la conmutación por error para el grupo de disponibilidad con el tipo de clúster de NONE"
services: 
author: MikeRayMSFT
ms.service: 
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: 10a2af2cb5bc9e98605a3ee988439e3c3be60c1e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
Cada AG tiene solo una réplica principal. La réplica principal permite lecturas y escrituras. Para cambiar qué réplica principal, puede conmutar por error. En un AG para lograr alta disponibilidad, el Administrador de clústeres automatiza el proceso de conmutación por error. En un AG con el tipo de clúster NONE, el proceso de conmutación por error es manual. 

Hay dos maneras para conmutar la réplica principal en un AG con el tipo de clúster NONE:

- Forzar la conmutación por error manual con pérdida de datos
- Conmutación por error manual sin pérdida de datos

### <a name="forced-manual-failover-with-data-loss"></a>Forzar la conmutación por error manual con pérdida de datos

Use este método cuando la réplica principal no está disponible y no se puede recuperar. 

Para forzar la conmutación por error con pérdida de datos, conéctese a la instancia de SQL Server que hospeda la réplica secundaria de destino y ejecute:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>Conmutación por error manual sin pérdida de datos

Use este método si la réplica principal está disponible, pero necesita modificar temporal o permanentemente la configuración y la instancia de SQL Server que hospeda la réplica principal. Antes de emitir la conmutación por error manual, asegúrese de que la réplica secundaria de destino está actualizada para evitar la posible pérdida de datos. 

Conmutación por error manual sin pérdida de datos:

1. Realizar la réplica secundaria de destino `SYNCHRONOUS_COMMIT`.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. Ejecute la consulta siguiente para identificar los que las transacciones activas se confirman en la réplica principal y al menos una réplica secundaria sincrónica: 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   La réplica secundaria se sincroniza si `synchronization_state_desc` es `SYNCHRONIZED`.

3. Actualización `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en 1.

   El siguiente script establece `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en 1 en un AG denominado `ag1`. Antes de ejecutar el script siguiente, reemplace `ag1` con el nombre de su AG:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   Este valor garantiza que todas las transacciones activas se compromete a la réplica principal y al menos una réplica secundaria sincrónica. 

4. Disminuir el nivel de la réplica principal a una réplica secundaria. Después de que la réplica principal se degrada, es de solo lectura. Ejecute este comando en la instancia de SQL Server que hospeda la réplica principal para el rol de actualizar `SECONDARY`:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. Ascienda la réplica secundaria de destino a principal. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > Para eliminar un AG, use [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Para un AG creado con clúster, escriba ninguno o externo, el comando debe ejecutarse en todas las réplicas que forman parte de disponibilidad.