---
title: Operar el grupo de disponibilidad SQL Server en Linux | Documentos de Microsoft
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.openlocfilehash: fd23b5c0de42fa0d91b893000c409083a2637fbb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Siempre funcionan en grupos de disponibilidad en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>Actualizar grupo de disponibilidad

Antes de actualizar un grupo de disponibilidad, revise los patrones y prácticas en [actualizar instancias de réplica del grupo de disponibilidad](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

Las siguientes secciones explican cómo realizar una actualización gradual con instancias de SQL Server en Linux con grupos de disponibilidad. 

### <a name="upgrade-steps-on-linux"></a>Pasos de actualización en Linux

Una vez réplicas del grupo de disponibilidad en las instancias de SQL Server en Linux, el tipo de clúster del grupo de disponibilidad es `EXTERNAL` o `NONE`. Un grupo de disponibilidad que está administrado por un administrador de clústeres, además de clúster de conmutación por error de Windows Server (WSFC) es `EXTERNAL`. Marcapasos con Corosync es un ejemplo de un administrador de clústeres externa. Un grupo de disponibilidad con el Administrador de clúster no tiene el tipo de clúster `NONE` los pasos de actualización que se describen aquí son específicos para los grupos de disponibilidad del tipo de clúster `EXTERNAL` o `NONE`.

El orden en que se actualicen las instancias depende de si su rol es secundaria y si no que hospedan las réplicas sincrónicas o asincrónicas. Actualizar las instancias de SQL Server que hospedan réplicas secundarias asincrónicas en primer lugar. A continuación, actualizar instancias que hospedan las réplicas secundarias sincrónicas. 

   >[!NOTE]
   >Si un grupo de disponibilidad solo tiene asincrónica réplicas, para evitar la pérdida de datos cambiar una réplica al sincrónica y esperan hasta que se sincronicen. A continuación, actualice esta réplica.
   
Antes de comenzar, realizar una copia de cada base de datos.

1. Detener el recurso en el nodo que hospeda la réplica secundaria de destino para la actualización.
   
   Antes de ejecutar el comando de actualización, detenga el recurso para que el clúster no se supervisará y producirá un error innecesariamente. En el ejemplo siguiente se agrega una restricción de ubicación en el nodo que se producirá en el recurso que se va a detener. Actualización `ag_cluster-master` con el nombre del recurso y `nodeName1` con el nodo que hospeda la réplica de destino para la actualización.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. Actualizar SQL Server en la réplica secundaria.

   Las siguientes actualizaciones de ejemplo `mssql-server` y `mssql-server-ha` paquetes.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. Quite la restricción de ubicación.

   Antes de ejecutar el comando de actualización, detenga el recurso para que el clúster no se supervisará y producirá un error innecesariamente. En el ejemplo siguiente se agrega una restricción de ubicación en el nodo que se producirá en el recurso que se va a detener. Actualización `ag_cluster-master` con el nombre del recurso y `nodeName1` con el nodo que hospeda la réplica de destino para la actualización.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   Como práctica recomendada, asegúrese de que se inició el recurso (mediante `pcs status` comando) y la réplica secundaria está conectada y sincronizada estado después de la actualización.

1. Después de que se actualicen todas las réplicas secundarias, conmutación por error manual a una de las réplicas secundarias sincrónicas.

   Para los grupos de disponibilidad con `EXTERNAL` tipo de clúster, use las herramientas de administración de clúster no over; grupos de disponibilidad con `NONE` tipo de clúster debe usar Transact-SQL para una conmutación por error. 
   En el ejemplo siguiente, se produce un error en un grupo de disponibilidad con las herramientas de administración de clúster. Reemplace `<targetReplicaName>` con el nombre de la réplica secundaria sincrónica que se convertirá en principal:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >Los pasos siguientes solo se aplican a grupos de disponibilidad que no tienen un administrador de clústeres.

   Si el tipo de clúster del grupo de disponibilidad es `NONE`, manualmente una conmutación por error. Realice los pasos siguientes en el orden indicado:

      A. El siguiente comando establece la réplica principal al secundario. Reemplace `AG1` con el nombre del grupo de disponibilidad. Ejecute el comando de Transact-SQL en la instancia de SQL Server que hospeda la réplica principal.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      B. El comando siguiente establece una réplica secundaria sincrónica a principal. Ejecute el siguiente comando de Transact-SQL en la instancia de destino de SQL Server: la instancia que hospeda la réplica secundaria sincrónica.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. Después de la conmutación por error, actualice SQL Server en la réplica principal anterior repitiendo el procedimiento anterior.

   Las siguientes actualizaciones de ejemplo `mssql-server` y `mssql-server-ha` paquetes.

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. Para un grupos de disponibilidad con un administrador de clústeres externa - donde el tipo de clúster es externo, limpie la restricción de ubicación que es atribuible a la conmutación por error manual. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Reanude el movimiento de datos para la réplica secundaria recién actualizado: la réplica principal. Este paso es necesario cuando una instancia superior de la versión de SQL Server está transfiriendo de bloques de registro a una instancia de versión menor en un grupo de disponibilidad. Ejecute el siguiente comando en la nueva réplica secundaria (la réplica principal anterior).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Después de actualizar todos los servidores, puede realizar conmutación por recuperación. Conmutación por error nuevo en la réplica principal original - si es necesario. 

## <a name="drop-an-availability-group"></a>Quitar un grupo de disponibilidad

Para eliminar un grupo de disponibilidad, ejecute [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Si el tipo de clúster es `EXTERNAL` o `NONE` ejecute el comando en cada instancia de SQL Server que hospeda una réplica. Por ejemplo, para quitar un grupo de disponibilidad denominado `group_name` ejecute el siguiente comando:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Pasos siguientes

[Configurar Red Hat Enterprise Linux clúster de recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar el clúster SUSE Linux Enterprise Server para los recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar recursos de clúster del grupo de disponibilidad de SQL Server del clúster Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)
