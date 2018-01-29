---
title: Configurar SQL Server grupo de disponibilidad AlwaysOn de alta disponibilidad en Linux | Documentos de Microsoft
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 01/24/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: On Demand
ms.openlocfilehash: c510789ccd2c76e2d4e3b7bd8354a46e80e335c2
ms.sourcegitcommit: 0a9c29c7576765f3b5774b2e087852af42ef4c2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Configurar SQL Server grupo de disponibilidad AlwaysOn de alta disponibilidad en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este artículo se describe cómo crear un SQL Server siempre en disponibilidad grupo (AG) de alta disponibilidad en Linux. Hay dos tipos de configuración de grupos de disponibilidad. A *alta disponibilidad* configuración utiliza un administrador de clúster para proporcionar continuidad del negocio. Esta configuración puede incluir también las réplicas de la escala de lectura. Este documento explica cómo crear el AG para lograr alta disponibilidad.

También puede crear un AG sin un clúster de administrador para *lectura escala*. Disponibilidad de escala de lectura solo proporciona réplicas de solo lectura para el rendimiento escalado. No proporciona alta disponibilidad. Para crear un AG de escala de lectura, consulte [configurar un grupo de disponibilidad de SQL Server para la escala de lectura en Linux](sql-server-linux-availability-group-configure-rs.md).

Las configuraciones que garantizan alta disponibilidad y protección de datos que requieren réplicas de confirmación de dos o tres sincrónico. Con tres réplicas sincrónicas, puede recuperar automáticamente la AG incluso si un servidor no está disponible. Para obtener más información, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). 

Todos los servidores deben ser físicos o virtuales y servidores virtuales deben estar en la misma plataforma de virtualización. Este requisito es porque los agentes de barrera son específicas de la plataforma. Vea [directivas para clústeres invitados](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Roadmap

Los pasos para crear un AG en servidores Linux para lograr alta disponibilidad son diferentes de los pasos en un clúster de conmutación por error de Windows Server. En la lista siguiente describe los pasos generales: 

1. [Configurar SQL Server en tres servidores de clúster](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Los tres servidores en el AG deben estar en la misma plataforma - física o virtual - porque Linux alta disponibilidad usa a agentes de barrera para aislar los recursos en los servidores. Los agentes de barrera son específicos para cada plataforma.

2. Cree el AG. Este paso se describe en este artículo actual. 

3. Configurar un administrador de recursos de clúster, como marcapasos.
   
   La manera de configurar un administrador de recursos de clúster depende de la distribución de Linux específica. Vea los siguientes vínculos para obtener instrucciones específicas de distribución: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Los entornos de producción requieren a un agente de barrera, como STONITH para lograr alta disponibilidad. Las demostraciones en esta documentación no utiliza a agentes de barrera. Las demostraciones son para pruebas y la validación solo. 
   
   >Un clúster de Linux usa barrera para devolver el clúster a un estado conocido. La manera de configurar la barrera depende de la distribución y el entorno. Actualmente, la barrera no está disponible en algunos entornos de nube. Para obtener más información, consulte [directivas de soporte técnico para alta disponibilidad RHEL clústeres: plataformas de virtualización](https://access.redhat.com/articles/29440).
   
   >Para SLES, consulte [extensión de alta disponibilidad de SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Agregue el AG como un recurso en el clúster.  

   La forma de agregar el AG como un recurso del clúster depende de la distribución de Linux. Vea los siguientes vínculos para obtener instrucciones específicas de distribución: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Crear el grupo de disponibilidad.

Para una configuración de alta disponibilidad que garantiza la conmutación automática por error, el AG requiere al menos tres réplicas. Cualquiera de las siguientes configuraciones puede admitir alta disponibilidad:

- [Tres réplicas sincrónicas.](sql-server-linux-availability-group-ha.md#threeSynch)

- [Una réplica de la configuración más de dos réplicas sincrónicas.](sql-server-linux-availability-group-ha.md#twoSynch)

Para obtener información, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md).

>[!NOTE]
>Los grupos de disponibilidad pueden incluir réplicas sincrónicas o asincrónicas adicionales. 

Cree el AG para lograr alta disponibilidad en Linux. Use la [crear grupo de disponibilidad](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-availability-group-transact-sql) con `CLUSTER_TYPE = EXTERNAL`. 

* Grupo de disponibilidad: `CLUSTER_TYPE = EXTERNAL` especifica que una entidad externa clúster administra la disponibilidad. Marcapasos es un ejemplo de una entidad externa del clúster. Cuando el tipo de clúster de AG es externo, 

* Conjunto de réplicas principales y secundarias `FAILOVER_MODE = EXTERNAL`. 
   Especifica que la réplica se interactúa con un administrador de clúster externo, como marcapasos. 

Los scripts de Transact-SQL siguientes crean un AG para lograr alta disponibilidad con el nombre `ag1`. La secuencia de comandos configura las réplicas AG con `SEEDING_MODE = AUTOMATIC`. Esta configuración hace que SQL Server crear automáticamente la base de datos en cada servidor secundario. Actualice el siguiente script para su entorno. Reemplace el `**<node1>**`, `**<node2>**`, o `**<node3>**` valores con los nombres de las instancias de SQL Server que hospedan las réplicas. Reemplace el `**<5022>**` con el puerto se configura para el extremo de reflejo de datos. Para crear el AG, ejecute el código Transact-SQL siguiente en la instancia de SQL Server que hospeda la réplica principal.

Ejecutar **sola** de las secuencias de comandos siguientes: 

- [Crear grupo de disponibilidad con tres réplicas sincrónicas](#threeSynch).
- [Crear grupo de disponibilidad con dos réplicas sincrónicas y una réplica de configuración](#configOnly)
- [Crear grupo de disponibilidad con dos réplicas sincrónicas](#readScale).

<a name="threeSynch"></a>

- Crear AG con tres réplicas sincrónicas

   ```SQL
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
   >Después de ejecutar el script anterior para crear un AG con tres réplicas sincrónicas, no ejecute el script siguiente:

- Crear AG con dos réplicas sincrónicas y una réplica de configuración:

   >[!IMPORTANT]
   >Esta arquitectura permite que cualquier edición de SQL Server para hospedar la réplica terceros. Por ejemplo, la tercera réplica se puede hospedar en SQL Server Enterprise Edition. En Enterprise Edition, es el tipo de extremo solo es válido `WITNESS`. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'**<node1>**' WITH ( 
          ENDPOINT_URL = N'tcp://**<node1>**:**<5022>**', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'**<node2>**' WITH (  
          ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'**<node3>**' WITH ( 
          ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- Crear AG con dos réplicas sincrónicas.

   Incluya dos réplicas con el modo sincrónico de disponibilidad. Por ejemplo, el script siguiente crea un AG denominado `ag1`. `node1`y `node2` hospedan las réplicas en modo sincrónico, con conmutación automática por error y la propagación automática.

   >[!IMPORTANT]
   >Solo se ejecute el siguiente script para crear un AG con dos réplicas sincrónicas. No se ejecute el siguiente script si ha ejecutado un script anterior. 

   ```SQL
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


También puede configurar un AG con `CLUSTER_TYPE=EXTERNAL` con SQL Server Management Studio o PowerShell. 

### <a name="join-secondary-replicas-to-the-ag"></a>Une las réplicas secundarias para el grupo de disponibilidad.

El siguiente script de Transact-SQL une a una instancia de SQL Server en un AG denominado `ag1`. Actualizar la secuencia de comandos para su entorno. En cada instancia de SQL Server que hospeda una réplica secundaria, ejecute el siguiente Transact-SQL para unirse a la disponibilidad.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Después de crear el AG, debe configurar la integración con una tecnología de clúster como marcapasos para alta disponibilidad. Para una configuración de escalado de lectura mediante grupos de disponibilidad, a partir de [!INCLUDE [SQL Server version](..\includes\sssqlv14-md.md)], no es necesario configurar un clúster.

Si ha seguido los pasos descritos en este documento, tendrá un AG que no está en clúster. El siguiente paso es agregar el clúster. Esta configuración es válida para los escenarios de equilibrio de carga de escala de lectura, no está completo para lograr alta disponibilidad. Para lograr alta disponibilidad, debe agregar el AG como un recurso de clúster. Vea [pasos siguientes](#next-steps) para obtener instrucciones. 

## <a name="notes"></a>Notas

>[!IMPORTANT]
>Después de configurar el clúster y agregar el AG como un recurso de clúster, no puede usar Transact-SQL para conmutar los recursos AG. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En RHEL o Ubuntu usar `pcs`. En SLES usar `crm`. 

>[!IMPORTANT]
>Si el AG es un recurso de clúster, hay un problema conocido en la versión actual, donde la conmutación por error forzada con pérdida de datos a una réplica asincrónica no funciona. Este problema se solucionará en la próxima versión. Se realiza correctamente la conmutación por error de manual o automática a una réplica sincrónica. 


## <a name="next-steps"></a>Pasos siguientes

[Configurar Red Hat Enterprise Linux clúster de recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar el clúster SUSE Linux Enterprise Server para los recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar recursos de clúster del grupo de disponibilidad de SQL Server del clúster Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)
