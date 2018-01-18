---
title: Operar el grupo de disponibilidad SQL Server en Linux | Documentos de Microsoft
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 07/20/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 23eedac40aff1fcab50c2e05406d3c87b988e392
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Siempre funcionan en grupos de disponibilidad en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

## <a name="failover"></a>Conmutación por error el grupo de disponibilidad

Utilice las herramientas de administración de clúster para conmutar por error un grupo de disponibilidad administrado por un administrador de clúster externo. Por ejemplo, si una solución usa marcapasos para administrar clústeres de Linux, use `pcs` para realizar conmutaciones por error manuales en RHEL o Ubuntu. En SLES use `crm`. 

> [!IMPORTANT]
> En las operaciones normales, no realizan la conmutación con herramientas de administración de Transact-SQL o SQL Server como SSMS o PowerShell. Cuando `CLUSTER_TYPE = EXTERNAL`, el único valor aceptable para `FAILOVER_MODE` es `EXTERNAL`. Con esta configuración, se ejecutan todas las acciones de conmutación por error manual o automática mediante el Administrador de clústeres externa. 

### <a name="manual-failover-examples"></a>Ejemplos de conmutación por error manual

Conmutación por error manualmente el grupo de disponibilidad con las herramientas de administración del clúster externo. En las operaciones normales, no iniciar la conmutación por error con Transact-SQL. Si las herramientas de administración del clúster externo no responde, puede forzar la conmutación por error del grupo de disponibilidad. Para que obtener instrucciones forzar la conmutación por error manual, consulte [Manual mover cuando las herramientas de clúster no están respondiendo](#forceManual).

Completar la conmutación por error manual en dos pasos. 

1. Mover el recurso de grupo de disponibilidad desde el nodo de clúster que pertenece a los recursos a un nuevo nodo.

   El Administrador de clústeres mueve el recurso de grupo de disponibilidad y agrega una restricción de ubicación. Esta restricción configura el recurso que se va a ejecutar en el nuevo nodo. Debe quitar esta restricción para mover que ya sea manual o automáticamente conmutar por error en el futuro.

2. Quite la restricción de ubicación.

#### <a name="1-manually-fail-over"></a>1. Conmutación por error manual

Para conmutar por error manualmente un recurso de grupo de disponibilidad denominado *ag_cluster* al nodo de clúster denominado *Nombredenodo2*, ejecute el comando adecuado para su distribución:

- **Ejemplo RHEL/Ubuntu**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **Ejemplo SLES**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```



>[!IMPORTANT]
>Después de conmutar manualmente un recurso, debe eliminar una restricción de ubicación que se agrega automáticamente durante el desplazamiento.

#### <a name="2-remove-the-location-constraint"></a>2. Quitar la restricción de ubicación

Durante una operación de traslado manual, la `pcs` comando `move` o `crm` comando `migrate` agrega una restricción de ubicación para el recurso que se va a colocar en el nuevo nodo de destino. Para ver la nueva restricción, ejecute el comando siguiente después de mover manualmente el recurso:

- **Ejemplo RHEL/Ubuntu**

   ```bash
   sudo pcs constraint --full
   ```

- **Ejemplo SLES**

   ```bash
   crm config show
   ```

Debe quitar la restricción de ubicación para que las futuras operaciones de mover (incluida la conmutación automática por error) se realicen correctamente. 

Para quitar la restricción, ejecute el comando siguiente. 

- **Ejemplo RHEL/Ubuntu**

   En este ejemplo `ag_cluster-master` es el nombre del recurso que se ha movido. 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **Ejemplo SLES**

   En este ejemplo `ag_cluster` es el nombre del recurso que se ha movido. 

   ```bash
   crm resource clear ag_cluster
   ```

Como alternativa, puede ejecutar el comando siguiente para quitar la restricción de ubicación.  

- **Ejemplo RHEL/Ubuntu**

   En el comando siguiente, `cli-prefer-ag_cluster-master` es el identificador de la restricción que se debe quitar. `sudo pcs constraint --full` devuelve este identificador. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
- **Ejemplo SLES**

   En el siguiente comando `cli-prefer-ms-ag_cluster` es el identificador de la restricción. `crm config show` devuelve este identificador. 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>La conmutación automática por error no agrega una restricción de ubicación, por lo que no es necesaria ninguna limpieza. 

Para obtener más información:
- [Red Hat: Managing Cluster Resources](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html) (Red Hat: Administración de recursos de clúster)
- [Marcapasos - mover recursos manualmente](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
 [SLES Administration Guide - recursos](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 

### <a name="forceManual"></a>Manual mover cuando las herramientas de clúster no están respondiendo 

En casos extremos, si un usuario no puede utilizar las herramientas de administración de clúster para interactuar con el clúster (es decir, el clúster no responde, herramientas de administración de clúster tienen un comportamiento defectuoso), el usuario podría tener que conmutar por error manualmente: omitiendo el Administrador de clústeres externa. Esto no se recomienda para las operaciones normales y debe usarse en casos de clúster no se puede ejecutar la acción de conmutación por error utilizando las herramientas de administración de clúster.

Si no se producirá un error en el grupo de disponibilidad con las herramientas de administración de clúster, siga estos pasos para la conmutación por error de las herramientas de SQL Server:

1. Compruebe que el recurso de grupo de disponibilidad no está administrado por el clúster nunca más. 

      - Ha intentado establecer el recurso en modo de no administrado. Esto indica que la administración y el agente de recursos para detener la supervisión de recursos. Por ejemplo: 
      
      ```bash
      sudo pcs resource unmanage <**resourceName**>
      ```

      - Si se produce un error en el intento de establecer el modo de recursos en modo de no administrado, elimine el recurso. Por ejemplo:

      ```bash
      sudo pcs resource delete <**resourceName**>
      ```

      >[!NOTE]
      >Cuando se elimina un recurso también elimina todas las restricciones asociadas. 

1. Establecer manualmente la variable de contexto de sesión `external_cluster`.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Conmutar por error el grupo de disponibilidad con Transact-SQL. En el ejemplo siguiente reemplazar `<**MyAg**>` con el nombre del grupo de disponibilidad. Conéctese a la instancia de SQL Server que hospeda la réplica secundaria de destino y ejecute el siguiente comando:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <**MyAg**> FAILOVER;
   ```

1. Reinicie Administración y supervisión de recursos de clúster. Ejecute el siguiente comando:

   ```bash
   sudo pcs resource manage <**resourceName**>
   sudo pcs resource cleanup <**resourceName**>
   ```

## <a name="database-level-monitoring-and-failover-trigger"></a>Desencadenador de supervisión y la conmutación por error de nivel de base de datos

Para `CLUSTER_TYPE=EXTERNAL`, la semántica de desencadenador de conmutación por error es diferentes en comparación con WSFC. Cuando el grupo de disponibilidad está en una instancia de SQL Server en un WSFC, pasando de `ONLINE` de estado para la base de datos hace que el estado del grupo de disponibilidad notificar un error. Esto indicará que el Administrador de clústeres para desencadenar una acción de conmutación por error. En Linux, la instancia de SQL Server no puede comunicarse con el clúster. Supervisión de estado de la base de datos se realiza "outside-in". Si el usuario eligió en para la supervisión de nivel de conmutación por error de base de datos y conmutación por error (estableciendo la opción `DB_FAILOVER=ON` al crear el grupo de disponibilidad), el clúster comprobará si el estado de la base de datos es `ONLINE` cada vez que cuando se ejecuta una acción de supervisión. El clúster de consulta el estado en `sys.databases`. Para cualquier estado distinto `ONLINE`, desencadena una conmutación por error automáticamente (si se cumplen las condiciones de la conmutación automática por error). El tiempo real de la conmutación por error depende de la frecuencia de la acción de supervisión, así como el estado de la base de datos que se actualiza en sys.databases.

## <a name="upgrade-availability-group"></a>Actualizar grupo de disponibilidad

Antes de actualizar un grupo de disponibilidad, revise las prácticas recomendadas en [actualizar instancias de réplica del grupo de disponibilidad](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

Las siguientes secciones explican cómo realizar una actualización gradual con instancias de SQL Server en Linux con grupos de disponibilidad. 

### <a name="upgrade-steps-on-linux"></a>Pasos de actualización en Linux

Una vez réplicas del grupo de disponibilidad en las instancias de SQL Server en Linux, el tipo de clúster del grupo de disponibilidad es `EXTERNAL` o `NONE`. Un grupo de disponibilidad que está administrado por un administrador de clústeres, además de clúster de conmutación por error de Windows Server (WSFC) es `EXTERNAL`. Marcapasos con Corosync es un ejemplo de un administrador de clústeres externa. Un grupo de disponibilidad con el Administrador de clúster no tiene el tipo de clúster `NONE` los pasos de actualización que se describen aquí son específicos para los grupos de disponibilidad del tipo de clúster `EXTERNAL` o `NONE`.

1. Antes de comenzar, cada base de datos de copia de seguridad.
2. Actualizar las instancias de SQL Server que hospeden las réplicas secundarias.

    A. Actualice primero las réplicas secundarias asincrónicas.

    B. Actualizar las réplicas secundarias sincrónicas.

   >[!NOTE]
   >Si un grupo de disponibilidad solo tiene asincrónica réplicas - para evitar la pérdida de datos cambiar una réplica al sincrónica y esperan hasta que se sincronicen. A continuación, actualice esta réplica.
   
   b.1. Detener el recurso en el nodo que hospeda la réplica secundaria de destino para la actualización
   
   Antes de ejecutar el comando de actualización, detenga el recurso para que el clúster no se supervisará y producirá un error innecesariamente. En el ejemplo siguiente se agrega una restricción de ubicación en el nodo que se producirá en el recurso que se va a detener. Actualización `ag_cluster-master` con el nombre del recurso y `nodeName1` con el nodo que hospeda la réplica de destino para la actualización.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```
   b.2. Actualizar SQL Server en la réplica secundaria

   Las siguientes actualizaciones de ejemplo `mssql-server` y `mssql-server-ha` paquetes.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   b.3. Quitar la restricción de ubicación

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

1. Después de la conmutación por error, actualice SQL Server en la réplica principal anterior repitiendo el mismo procedimiento descrito en los pasos anteriores de b.3 b.1.

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

1. Para un grupos de disponibilidad con un clúster externo manager - donde escribir el clúster es externo, Liberador de espacio en la restricción de ubicación que es atribuible a la conmutación por error manual. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Reanude el movimiento de datos para la réplica secundaria recién actualizado: la réplica principal. Esto es necesario cuando una instancia superior de la versión de SQL Server está transfiriendo de bloques de registro a una instancia de versión menor en un grupo de disponibilidad. Ejecute el siguiente comando en la nueva réplica secundaria (la réplica principal anterior).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Después de actualizar todos los servidores, puede que la conmutación por recuperación - conmutar por recuperación a la réplica principal original - si es necesario. 

## <a name="drop-an-availability-group"></a>Quitar un grupo de disponibilidad

Para eliminar un grupo de disponibilidad, ejecute [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Si el tipo de clúster es `EXTERNAL` o `NONE` ejecute el comando en cada instancia de SQL Server que hospeda una réplica. Por ejemplo, para quitar un grupo de disponibilidad denominado `group_name` ejecute el siguiente comando:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Pasos siguientes

[Configurar Red Hat Enterprise Linux clúster de recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar el clúster SUSE Linux Enterprise Server para los recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar recursos de clúster del grupo de disponibilidad de SQL Server del clúster Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)
