---
title: "Administrar la conmutación por error de disponibilidad grupo: SQL Server en Linux | Documentos de Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 086cf16e243810452a3bace411abdc3689e74ff8
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="always-on-availability-group-failover-on-linux"></a>Conmutación por error del grupo de disponibilidad AlwaysOn en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En el contexto de un grupo de disponibilidad (AG), el rol principal y el rol secundario de réplicas de disponibilidad son suelen ser intercambiables en un proceso conocido como conmutación por error. Hay tres formas de conmutación por error: conmutación por error automática (sin pérdida de datos), conmutación por error manual planeada (sin pérdida de datos) y conmutación por error manual forzada (con posible pérdida de datos), normalmente denominada *conmutación por error forzada*. Automática y planeadas conmutaciones por error manuales mantienen todos los datos. Conmutar por error un AG en el nivel de réplica de disponibilidad. Es decir, un AG conmuta por error a uno de sus réplicas secundarias (el destino de conmutación por error actual). 

Para obtener información general acerca de la conmutación por error, consulte [modos de conmutación por error y conmutación por error](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).

## <a name="failover"></a>conmutación por error manual

Utilice las herramientas de administración de clúster para conmutar por error un AG administrado por un administrador de clústeres externa. Por ejemplo, si una solución usa marcapasos para administrar clústeres de Linux, use `pcs` para realizar conmutaciones por error manuales en RHEL o Ubuntu. En SLES use `crm`. 

> [!IMPORTANT]
> En las operaciones normales, no realizan la conmutación con herramientas de administración de Transact-SQL o SQL Server como SSMS o PowerShell. Cuando `CLUSTER_TYPE = EXTERNAL`, el único valor aceptable para `FAILOVER_MODE` es `EXTERNAL`. Con esta configuración, se ejecutan todas las acciones de conmutación por error manual o automática mediante el Administrador de clústeres externa. Para que obtener instrucciones forzar la conmutación por error con posible pérdida de datos, vea [forzar la conmutación por error](#forceFailover).

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">Pasos de conmutación por error manual

Para conmutar por error, la réplica secundaria que se convertirá en la réplica principal debe ser sincrónica. Si una réplica secundaria es asincrónica, [cambiar el modo de disponibilidad](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md).

Conmutación por error manual en dos pasos.

   En primer lugar,[ manual por error el mover recursos AG](#manualMove) desde el nodo de clúster que pertenece a los recursos a un nuevo nodo.

   El clúster conmuta por error el recurso AG y agrega una restricción de ubicación. Esta restricción configura el recurso que se va a ejecutar en el nuevo nodo. Quitar esta restricción para correctamente una conmutación por error en el futuro.

   Segundo, [quitar la restricción de ubicación](#removeLocConstraint).

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">Paso 1. Conmutación por error manual el movimiento de recurso de grupo de disponibilidad

Para conmutar por error manualmente un recurso de AG denominado *ag_cluster* al nodo de clúster denominado *Nombredenodo2*, ejecute el comando adecuado para su distribución:

- **Ejemplo RHEL/Ubuntu**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **Ejemplo SLES**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>Después de conmutar manualmente un recurso, debe eliminar una restricción de ubicación que se agrega automáticamente.

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> Paso 2. Quitar la restricción de ubicación

Durante una conmutación por error manual, la `pcs` comando `move` o `crm` comando `migrate` agrega una restricción de ubicación para el recurso que se va a colocar en el nuevo nodo de destino. Para ver la nueva restricción, ejecute el comando siguiente después de mover manualmente el recurso:

- **Ejemplo RHEL/Ubuntu**

   ```bash
   sudo pcs constraint --full
   ```

- **Ejemplo SLES**

   ```bash
   crm config show
   ```

Quite la restricción de ubicación, por lo que las conmutaciones por error futuras (incluidos la conmutación automática por error) correcta. 

Para quitar la restricción, ejecute el siguiente comando: 

- **Ejemplo RHEL/Ubuntu**

   En este ejemplo `ag_cluster-master` es el nombre del recurso que conmutar por error. 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **Ejemplo SLES**

   En este ejemplo `ag_cluster` es el nombre del recurso que conmutar por error. 

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
 
## <a name="forceFailover"></a> Forzar la conmutación por error 

Una conmutación por error forzada pensada estrictamente para la recuperación ante desastres. En este caso, no puede conmutar con herramientas de administración de clúster porque el centro de datos principal está inactivo. Si se fuerza la conmutación por error a una réplica secundaria no sincronizada, es posible que se pierdan datos. Forzar la conmutación por error sólo si debe restaurar el servicio en el AG inmediatamente y asume el riesgo de perder algunos datos.

Si no puede usar las herramientas de administración de clúster para interactuar con el clúster - por ejemplo, si el clúster deja de responder debido a un evento de desastre en el centro de datos principal, tendrá que forzar la conmutación por error para omitir el Administrador de clústeres externa. Este procedimiento no se recomienda para las operaciones normales, porque corre el riesgo de pérdida de datos. Utilícelo cuando las herramientas de administración de clúster no se pueden ejecutar la acción de conmutación por error. Funcionalmente, este procedimiento es similar a [realizar una conmutación por error manual forzada](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) en un AG en Windows.
 
Este proceso para forzar la conmutación por error es específico de SQL Server en Linux.

1. Compruebe que el recurso de AG más no está administrado por el clúster. 

      - Establecer el recurso al modo de no administrado en el nodo de clúster de destino. Este comando señala al agente de recursos con la administración y supervisión de recursos de detención. Por ejemplo: 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - Si se produce un error en el intento de establecer el modo de recursos en modo de no administrado, elimine el recurso. Por ejemplo:

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >Cuando se elimina un recurso, también elimina todas las restricciones asociadas. 

1. En la instancia de SQL Server que hospeda la réplica secundaria, establezca la variable de contexto de sesión `external_cluster`.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Conmutar por error el AG con Transact-SQL. En el ejemplo siguiente, reemplace `<MyAg>` con el nombre de su AG. Conéctese a la instancia de SQL Server que hospeda la réplica secundaria de destino y ejecute el siguiente comando:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  Después de una conmutación por error forzada, ponga el AG a un estado correcto antes de reiniciar la supervisión de recursos de clúster y la administración o volver a crear el recurso de AG. Revise el [tareas esenciales después de una conmutación por error forzada](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp).

1.  Reiniciar administración y supervisión de recursos de clúster:

   Para reiniciar la supervisión de recursos de clúster y la administración, ejecute el siguiente comando:

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   Si elimina el recurso de clúster, volver a crearla. Para volver a crear el recurso de clúster, siga las instrucciones de [crear recurso de grupo de disponibilidad](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).

>[!Important]
>No utilice los pasos anteriores para recuperación ante desastres, ya que el riesgo de pérdida de datos. En su lugar, cambie la réplica asincrónica a sincrónico y las instrucciones para [normal conmutación manual por error](#manualFailover).

## <a name="database-level-monitoring-and-failover-trigger"></a>Desencadenador de supervisión y la conmutación por error de nivel de base de datos

Para `CLUSTER_TYPE=EXTERNAL`, la semántica de desencadenador de conmutación por error es diferentes en comparación con WSFC. Una vez el AG en una instancia de SQL Server en un WSFC, pasando de `ONLINE` de estado para la base de datos hace que el estado de AG notificar un error. En respuesta, el Administrador de clústeres desencadena una acción de conmutación por error. En Linux, la instancia de SQL Server no puede comunicarse con el clúster. La supervisión de estado de la base de datos se lleva a cabo *fuera de*. Si el usuario eligió en para la supervisión de nivel de conmutación por error de base de datos y conmutación por error (estableciendo la opción `DB_FAILOVER=ON` al crear el AG), el clúster comprobará si el estado de la base de datos es `ONLINE` cada vez que ejecuta una acción de supervisión. El clúster de consulta el estado en `sys.databases`. Para cualquier estado distinto `ONLINE`, desencadena una conmutación por error automáticamente (si se cumplen las condiciones de la conmutación automática por error). El tiempo real de la conmutación por error depende de la frecuencia de la acción de supervisión, así como el estado de la base de datos que se actualiza en sys.databases.

Conmutación automática por error requiere al menos una réplica sincrónica.

## <a name="next-steps"></a>Pasos siguientes

[Configurar Red Hat Enterprise Linux clúster de recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar el clúster SUSE Linux Enterprise Server para los recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar recursos de clúster del grupo de disponibilidad de SQL Server del clúster Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)
