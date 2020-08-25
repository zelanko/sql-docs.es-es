---
title: Forzar la conmutación por error para grupos de disponibilidad de SQL Server
description: Forzar la conmutación por error para grupos de disponibilidad con el tipo de clúster NONE
services: ''
author: MikeRayMSFT
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: 0933f493ee71fe589842f8636e7364f79a432de0
ms.sourcegitcommit: dec2e2d3582c818cc9489e6a824c732b91ec3aeb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/11/2020
ms.locfileid: "88122282"
---
Cada grupo de disponibilidad tiene solo una réplica principal. La réplica principal permite lecturas y escrituras. Para cambiar la réplica principal, puede efectuar una conmutación por error. En un grupo de disponibilidad de alta disponibilidad, el administrador de clústeres automatiza el proceso de conmutación por error. En un grupo de disponibilidad con el tipo de clúster NONE, el proceso de conmutación por error es manual. 

Hay dos maneras de efectuar una conmutación por error de la réplica principal en un grupo de disponibilidad de tipo de clúster NONE:

- Conmutación por error manual forzada con pérdida de datos
- Conmutación por error manual sin pérdida de datos

### <a name="forced-manual-failover-with-data-loss"></a>Conmutación por error manual forzada con pérdida de datos

Use este método si la réplica principal no está disponible y no se puede recuperar. 

Para forzar una conmutación por error con pérdida de datos, conéctese a la instancia de SQL Server que hospeda la réplica secundaria de destino y ejecute el comando siguiente:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

Cuando la réplica principal anterior se recupere, también asumirá el rol principal. Para asegurarse de que la réplica principal anterior realiza la transición a un rol secundario, ejecute el siguiente comando en la réplica principal anterior.

```SQL
ALTER AVAILABILITY GROUP [ag1]  SET (ROLE = SECONDARY);
```

### <a name="manual-failover-without-data-loss"></a>Conmutación por error manual sin pérdida de datos

Use este método si la réplica principal está disponible, pero necesita modificar temporal o permanentemente la configuración y la instancia de SQL Server que hospeda la réplica principal. Antes de emitir la conmutación por error manual, asegúrese de que la réplica secundaria de destino está actualizada para evitar una posible pérdida de datos. 

Para realizar la conmutación por error manual sin pérdida de datos:

1. Cree la réplica secundaria de destino `SYNCHRONOUS_COMMIT`.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

1. Ejecute la consulta siguiente para identificar que las transacciones activas se confirman en la réplica principal y en al menos una réplica secundaria sincrónica: 

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

1. Actualice `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` a 1.

   El siguiente script establece `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en 1 en un grupo de disponibilidad denominado `ag1`. Antes de ejecutar el siguiente script, reemplace `ag1` por el nombre del grupo de disponibilidad:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1);
   ```

   Este valor garantiza que todas las transacciones activas se confirman en la réplica principal y en, al menos, una réplica secundaria sincrónica. 
   >[!NOTE]
   >Esta opción no es específica de la conmutación por error y se debe establecer en función de los requisitos del entorno.
   
1. Desconecte la réplica principal para preparar los cambios de rol.
   ```SQL
   ALTER AVAILABILITY GROUP [ag1] OFFLINE
   ```

1. Ascienda la réplica secundaria de destino a principal. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ``` 

1. Actualice el rol de la réplica principal antigua a `SECONDARY`, ejecute el comando siguiente en la instancia de SQL Server en la que se hospeda la réplica principal:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

   > [!NOTE] 
   > Para eliminar un grupo de disponibilidad, use [DROP AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/drop-availability-group-transact-sql). Para un grupo de disponibilidad creado con el tipo de clúster NONE o EXTERNAL, ejecute el comando en todas las réplicas que forman parte del grupo de disponibilidad.

1. Reanude el movimiento de datos, ejecute el siguiente comando para cada base de datos del grupo de disponibilidad en la instancia de SQL Server que hospeda la réplica principal: 

   ```sql
   ALTER DATABASE [db1]
        SET HADR RESUME
   ```
