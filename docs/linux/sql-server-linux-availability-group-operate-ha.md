---
title: Operar el grupo de disponibilidad de SQL Server en Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 8f2978533bb1e4006db9ebf2d2ed97a242a6f603
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086327"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Siempre funcionan en los grupos de disponibilidad en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>Actualizar grupo de disponibilidad

Antes de actualizar un grupo de disponibilidad, revise los patrones y prácticas en [actualizar instancias de réplica del grupo de disponibilidad](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

Las siguientes secciones explican cómo realizar una actualización gradual con instancias de SQL Server en Linux con grupos de disponibilidad. 

### <a name="upgrade-steps-on-linux"></a>Pasos de actualización en Linux

Cuando las réplicas del grupo de disponibilidad se encuentran en las instancias de SQL Server en Linux, el tipo de clúster del grupo de disponibilidad es `EXTERNAL` o `NONE`. Un grupo de disponibilidad que está administrado por un administrador de clústeres, además de clúster de conmutación por error de Windows Server (WSFC) es `EXTERNAL`. Pacemaker con Corosync es un ejemplo de un administrador de clúster externo. Un grupo de disponibilidad con el Administrador de clústeres tiene el tipo de clúster `NONE` los pasos de actualización que se describen aquí son específicos para los grupos de disponibilidad de tipo de clúster `EXTERNAL` o `NONE`.

El orden en el que se actualizan las instancias depende de si su rol es secundaria y el hecho de que hospedan las réplicas sincrónicas o asincrónicas. Actualice las instancias de SQL Server que hospedan réplicas secundarias asincrónicas en primer lugar. A continuación, actualice las instancias que hospedan las réplicas secundarias sincrónicas. 

   >[!NOTE]
   >Si un grupo de disponibilidad solo tiene asincrónica réplicas, para evitar la pérdida de datos cambiar una réplica al sincrónica y espere hasta que se sincronice. A continuación, actualice esta réplica.
   
Antes de comenzar, realizar copias de seguridad de cada base de datos.

1. Detener el recurso en el nodo que hospeda la réplica secundaria de destino para la actualización.
   
   Antes de ejecutar el comando de actualización, detenga el recurso para que el clúster no lo supervisará y producirá un error innecesariamente. El ejemplo siguiente agrega una restricción de ubicación en el nodo que se producirá en el recurso que se va a detener. Actualización `ag_cluster-master` con el nombre del recurso y `nodeName1` con el nodo que hospeda la réplica de destino para la actualización.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. Actualizar SQL Server en la réplica secundaria.

   El siguiente ejemplo se actualiza `mssql-server` y `mssql-server-ha` paquetes.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. Quite la restricción de ubicación.

   Antes de ejecutar el comando de actualización, detenga el recurso para que el clúster no lo supervisará y producirá un error innecesariamente. El ejemplo siguiente agrega una restricción de ubicación en el nodo que se producirá en el recurso que se va a detener. Actualización `ag_cluster-master` con el nombre del recurso y `nodeName1` con el nodo que hospeda la réplica de destino para la actualización.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   Como práctica recomendada, asegúrese de que se inició el recurso (mediante `pcs status` comando) y la réplica secundaria está conectada y sincronizado el estado después de la actualización.

1. Después de actualizan todas las réplicas secundarias, conmutación por error manual a una de las réplicas secundarias sincrónicas.

   Para grupos de disponibilidad con `EXTERNAL` tipo de clúster, use las herramientas de administración de clúster para producir un error over; grupos de disponibilidad con `NONE` tipo de clúster debe utilizar Transact-SQL para la conmutación por error. 
   El ejemplo siguiente se conmuta por error un grupo de disponibilidad con las herramientas de administración de clúster. Reemplace `<targetReplicaName>` con el nombre de la réplica secundaria sincrónica que se convertirá en principal:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >Los pasos siguientes solo se aplican a grupos de disponibilidad que no tienen un administrador de clústeres.

   Si el tipo de clúster del grupo de disponibilidad es `NONE`, manualmente la conmutación por error. Realice los pasos siguientes en el orden indicado:

      A. El siguiente comando establece la réplica principal al secundario. Reemplace `AG1` con el nombre del grupo de disponibilidad. Ejecute el comando de Transact-SQL en la instancia de SQL Server que hospeda la réplica principal.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      B. El siguiente comando establece una réplica secundaria sincrónica a principal. Ejecute el siguiente comando de Transact-SQL en la instancia de destino de SQL Server: la instancia que hospeda la réplica secundaria sincrónica.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. Después de la conmutación por error, actualice SQL Server en la réplica principal anterior, repita el procedimiento anterior.

   El siguiente ejemplo se actualiza `mssql-server` y `mssql-server-ha` paquetes.

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

1. Para un grupos de disponibilidad con un administrador de clúster externo - donde el tipo de clúster es EXTERNAL, limpie la restricción de ubicación se debió a la conmutación por error manual. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Reanudar movimiento de datos de la réplica secundaria recién actualizada: la réplica principal. Este paso es necesario cuando una instancia superior de la versión de SQL Server está transfiriendo los bloques de registro a una instancia de versión menor en un grupo de disponibilidad. Ejecute el siguiente comando en la nueva réplica secundaria (la réplica principal anterior).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Después de actualizar todos los servidores, puede conmutar por recuperación. Conmutar por recuperación al principal original - si es necesario. 

## <a name="drop-an-availability-group"></a>Quitar un grupo de disponibilidad

Para eliminar un grupo de disponibilidad, ejecute [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Si el tipo de clúster es `EXTERNAL` o `NONE` ejecute el comando en cada instancia de SQL Server que hospeda una réplica. Por ejemplo, para quitar un grupo de disponibilidad denominado `group_name` ejecute el siguiente comando:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Pasos siguientes

[Configurar el clúster de Red Hat Enterprise Linux para recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configuración de clúster SUSE Linux Enterprise Server para los recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar el clúster de Ubuntu para recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
