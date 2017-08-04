---
title: Configurar grupo de disponibilidad para SQL Server en Linux | Documentos de Microsoft
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
ms.openlocfilehash: 3a94bf7646143d687a7300c8ab2a66c3caa2d8d9
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---

# <a name="configure-always-on-availability-group-for-sql-server-on-linux"></a>Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux

En este artículo se describe cómo crear un servidor de SQL siempre en el grupo de disponibilidad para la alta disponibilidad en Linux. Hay dos tipos de configuración para los grupos de disponibilidad. A *alta disponibilidad* configuración utiliza un administrador de clúster para proporcionar continuidad del negocio. Esta configuración también puede incluir la lectura de las réplicas de escalabilidad horizontal. Este documento explica cómo crear la configuración de alta disponibilidad del grupo de disponibilidad.

También puede crear un *lectura escalabilidad* grupo de disponibilidad sin un administrador de clústeres. Esta configuración solo proporciona réplicas de solo lectura para el rendimiento escalado. No proporciona alta disponibilidad. Para crear un grupo de disponibilidad de escalado horizontal de lectura, consulte [Configurar grupo de disponibilidad y escalabilidad de lectura para SQL Server en Linux](sql-server-linux-availability-group-configure-rs.md).

Las configuraciones que garantizan alta disponibilidad y protección de datos que requieren réplicas de confirmación de dos o tres sincrónico. Con tres réplicas sincrónicas el grupo de disponibilidad puede terminar automáticamente recuperación incluso si un servidor no está disponible. Para obtener más información, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). 

Todos los servidores deben ser físicos o virtuales y servidores virtuales deben estar en la misma plataforma de virtualización. Este requisito es porque los agentes de barrera son específicas de la plataforma. Vea [directivas para clústeres invitados](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Guía básica

Los pasos para crear un grupo de disponibilidad en servidores Linux para lograr alta disponibilidad son diferentes de los pasos en un clúster de conmutación por error de Windows Server. En la lista siguiente se describe los pasos de alto niveles: 

1. [Configurar SQL Server en tres servidores de clúster](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Los tres servidores del grupo de disponibilidad deben estar en la misma plataforma - física o virtual - porque Linux alta disponibilidad usa a agentes de barrera para aislar los recursos en los servidores. Los agentes de barrera son específicos para cada plataforma.

2. Cree el grupo de disponibilidad. Este paso se describe en este artículo actual. 

3. Configurar un administrador de recursos de clúster, como marcapasos.
   
   La manera de configurar un administrador de recursos de clúster depende de la distribución de Linux específica. Vea los siguientes vínculos para obtener instrucciones específicas de distribución: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Los entornos de producción requieren a un agente de barrera, como STONITH para lograr alta disponibilidad. Las demostraciones en esta documentación no utiliza a agentes de barrera. Las demostraciones son para pruebas y la validación solo. 
   
   >Un clúster de Linux usa barrera para devolver el clúster a un estado conocido. La manera de configurar la barrera depende de la distribución y el entorno. Actualmente, la barrera no está disponible en algunos entornos de nube. Para obtener más información, consulte [directivas de soporte técnico para alta disponibilidad RHEL clústeres: plataformas de virtualización](https://access.redhat.com/articles/29440).
   
   >Para SLES, consulte [extensión de alta disponibilidad de SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Agregue el grupo de disponibilidad como un recurso en el clúster.  

   La manera de agregar el grupo de disponibilidad como un recurso del clúster depende de la distribución de Linux. Vea los siguientes vínculos para obtener instrucciones específicas de distribución: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES GRANDE](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Crear el grupo de disponibilidad

Existen dos configuraciones de grupo de disponibilidad admitidos para SQL Server en Linux.

- [Tres réplicas sincrónicas.](sql-server-linux-availability-group-ha.md#threeSynch)

- [Dos réplicas sincrónicas.](sql-server-linux-availability-group-ha.md#twoSynch)

Para obtener información, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md).

Cree el grupo de disponibilidad para lograr alta disponibilidad en Linux. Use la [crear grupo de disponibilidad](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-availability-group-transact-sql) con `CLUSTER_TYPE = EXTERNAL`. 

* Grupo de disponibilidad: `CLUSTER_TYPE = EXTERNAL` especifica que una entidad externa clúster administra el grupo de disponibilidad. Marcapasos es un ejemplo de una entidad externa del clúster. Cuando el tipo de clúster del grupo de disponibilidad es externo, 

* Conjunto de réplicas principales y secundarias `FAILOVER_MODE = EXTERNAL`. 
   Especifica que la réplica se interactúa con un administrador de clúster externo, como marcapasos. 

Las secuencias de comandos de Transact-SQL siguientes crea un grupo de disponibilidad para lograr alta disponibilidad con el nombre `ag1`. La secuencia de comandos configura las réplicas del grupo de disponibilidad con `SEEDING_MODE = AUTOMATIC`. Esta configuración hace que SQL Server crear automáticamente la base de datos en cada servidor secundario. Actualice el siguiente script para su entorno. Reemplace el `**<node1>**`, y `**<node2>**` valores con los nombres de las instancias de SQL Server que hospedan las réplicas. Reemplace el `**<5022>**` con el puerto se configura para el extremo de reflejo de datos. Para crear el grupo de disponibilidad, ejecute el código Transact-SQL siguiente en la instancia de SQL Server que hospeda la réplica principal.

Ejecutar **sola** de las secuencias de comandos siguientes: 

- Crear grupo de disponibilidad con tres réplicas sincrónicas.

   ```Transact-SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'**<node1>**' 
            WITH (
               ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'**<node2>**' 
            WITH ( 
               ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'**<node3>**'
           WITH( 
              ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >Después de ejecutar el script anterior para crear un grupo de disponibilidad con tres réplicas sincrónicas, no ejecute el script siguiente:

<a name="readScale"></a>

- Crear grupo de disponibilidad con dos réplicas sincrónicas.

   Incluya dos réplicas con el modo sincrónico de disponibilidad. Por ejemplo, el script siguiente crea un grupo de disponibilidad denominado `ag1`. `node1`y `node2` hospedan las réplicas en modo sincrónico, con conmutación automática por error y la propagación automática.

   >[!IMPORTANT]
   >Solo se ejecute el siguiente script para crear un grupo de disponibilidad con dos réplicas sincrónicas. No ejecute el siguiente script si se ejecutó el script anterior. 

   ```Transact-SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


También puede configurar un grupo de disponibilidad con `CLUSTER_TYPE=EXTERNAL` con SQL Server Management Studio o PowerShell. 

### <a name="join-secondary-replicas-to-the-availability-group"></a>Une las réplicas secundarias al grupo de disponibilidad

El siguiente script de Transact-SQL une a una instancia de SQL Server a un grupo de disponibilidad denominado `ag1`. Actualizar la secuencia de comandos para su entorno. En cada instancia de SQL Server que hospeda una réplica secundaria, ejecute el siguiente Transact-SQL para unirse al grupo de disponibilidad.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Después de crear el grupo de disponibilidad, debe configurar la integración con una tecnología de clúster como marcapasos para alta disponibilidad. Para una configuración de escalado horizontal lectura usa grupos de disponibilidad, a partir de [!INCLUDE [versión de SQL Server](..\includes\sssqlv14-md.md)], no es necesario configurar un clúster.

Si ha seguido los pasos descritos en este documento, tiene un grupo de disponibilidad que no está en clúster. El siguiente paso es agregar el clúster. Esta configuración es válida para los escenarios de equilibrio de carga de fuera de escala lecturas, no está completo para lograr alta disponibilidad. Para lograr alta disponibilidad, debe agregar el grupo de disponibilidad como un recurso de clúster. Vea [pasos siguientes](#next-steps) para obtener instrucciones. 

## <a name="notes"></a>Notas

>[!IMPORTANT]
>Después de configurar el clúster y agregar el grupo de disponibilidad como un recurso de clúster, no puede usar Transact-SQL para conmutar los recursos del grupo de disponibilidad. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En RHEL o Ubuntu usar `pcs`. En SLES usar `crm`. 

>[!IMPORTANT]
>Si el grupo de disponibilidad es un recurso de clúster, hay un problema conocido en la versión actual, donde la conmutación por error forzada con pérdida de datos a una réplica asincrónica no funciona. Este problema se solucionará en la próxima versión. Se realiza correctamente la conmutación por error de manual o automática a una réplica sincrónica. 


## <a name="next-steps"></a>Pasos siguientes

[Configurar Red Hat Enterprise Linux clúster de recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar el clúster SUSE Linux Enterprise Server para los recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar recursos de clúster del grupo de disponibilidad de SQL Server del clúster Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

