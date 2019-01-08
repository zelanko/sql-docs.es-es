---
title: Configurar SQL Server grupo de disponibilidad AlwaysOn para alta disponibilidad en Linux
titleSuffix: SQL Server
description: Obtenga información sobre cómo crear un SQL Server siempre en grupo de disponibilidad (AG) de alta disponibilidad en Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 9f88178450fb5ca19e52703ad02e29d107ca562a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201964"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Configurar SQL Server grupo de disponibilidad AlwaysOn para alta disponibilidad en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describe cómo crear un SQL Server siempre en grupo de disponibilidad (AG) de alta disponibilidad en Linux. Hay dos tipos de configuración para grupos de disponibilidad. Un *alta disponibilidad* configuración utiliza un administrador de clústeres para proporcionar continuidad del negocio. Esta configuración también puede incluir las réplicas de escalado de lectura. Este documento explica cómo crear el grupo de disponibilidad para alta disponibilidad.

También puede crear un grupo de disponibilidad sin un clúster de administrador para *escalado de lectura*. Solo el grupo de disponibilidad de escalado de lectura proporciona réplicas de solo lectura para el rendimiento escalado horizontal. No proporciona alta disponibilidad. Para crear un grupo de disponibilidad de escalado de lectura, consulte [configurar un grupo de disponibilidad de SQL Server para el escalado de lectura en Linux](sql-server-linux-availability-group-configure-rs.md).

Las configuraciones que garantizan la alta disponibilidad y protección de datos que requieren las réplicas de confirmación de dos o tres sincrónica. Con tres réplicas sincrónicas, puede recuperar automáticamente el grupo de disponibilidad incluso si un servidor no está disponible. Para obtener más información, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). 

Deben ser todos los servidores físicos o virtuales y servidores virtuales deben estar en la misma plataforma de virtualización. Este requisito es porque los agentes de vallado son específicas de la plataforma. Consulte [directivas para los clústeres invitados](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Mapa de ruta

Los pasos para crear un grupo de disponibilidad en los servidores de Linux para lograr alta disponibilidad son diferentes de los pasos en un clúster de conmutación por error de Windows Server. En la lista siguiente se describe los pasos de alto nivel: 

1. [Configurar SQL Server en tres servidores de clúster](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Los tres servidores en el grupo de disponibilidad deben estar en la misma plataforma - física o virtual - porque la alta disponibilidad de Linux usa a los agentes de barrera para aislar los recursos en los servidores. Los agentes de vallado son específicos para cada plataforma.

2. Cree el grupo de disponibilidad (AG). Este paso se trata en este artículo actual. 

3. Configurar un administrador de recursos de clúster, como Pacemaker.
   
   La manera de configurar un administrador de recursos del clúster depende de la distribución de Linux específica. Vea los siguientes vínculos para obtener instrucciones específicas de distribución: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Entornos de producción requieren a un agente de vallado, como STONITH para lograr alta disponibilidad. Las demostraciones en esta documentación no utiliza a agentes de vallado. Las demostraciones son para pruebas y validación solo. 
   
   >Un clúster de Linux usa vallado para devolver el clúster a un estado conocido. La manera de configurar vallado depende de la distribución y el entorno. Actualmente, la barrera no está disponible en algunos entornos de nube. Para obtener más información, consulte [directivas de soporte técnico para alta disponibilidad RHEL clústeres: plataformas de virtualización](https://access.redhat.com/articles/29440).
   
   >Para SLES, consulte [extensión de alta disponibilidad de SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Agregue el grupo de disponibilidad como un recurso en el clúster.  

   La manera de agregar el grupo de disponibilidad como un recurso del clúster depende de la distribución de Linux. Vea los siguientes vínculos para obtener instrucciones específicas de distribución: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Crear el grupo de disponibilidad

Los ejemplos en esta sección explican cómo crear el grupo de disponibilidad mediante Transact-SQL. También puede usar al Asistente para grupo de disponibilidad de Management Studio de SQL Server. Cuando se crea un grupo de disponibilidad con el asistente, devolverá un error al unir las réplicas para el grupo de disponibilidad. Para solucionar este problema, conceda `ALTER`, `CONTROL`, y `VIEW DEFINITIONS` a la pacemaker en el grupo de disponibilidad en todas las réplicas. Una vez que se conceden permisos en la réplica principal, únase a los nodos al grupo de disponibilidad a través del asistente, pero para alta disponibilidad funcionar correctamente, conceder permisos en todas las réplicas.

Para una configuración de alta disponibilidad que garantiza la conmutación automática por error, el grupo de disponibilidad requiere al menos tres réplicas. Cualquiera de las siguientes configuraciones pueda admitir alta disponibilidad:

- [Tres réplicas sincrónicas.](sql-server-linux-availability-group-ha.md#threeSynch)

- [Una réplica de la configuración más de dos réplicas sincrónicas](sql-server-linux-availability-group-ha.md#twoSynch)

Para obtener información, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md).

>[!NOTE]
>Los grupos de disponibilidad pueden incluir más réplicas sincrónicas o asincrónicas. 

Cree el grupo de disponibilidad para alta disponibilidad en Linux. Use la [crear grupo de disponibilidad](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql) con `CLUSTER_TYPE = EXTERNAL`. 

* Grupo de disponibilidad: `CLUSTER_TYPE = EXTERNAL` especifica que una entidad de clúster externo administra el grupo de disponibilidad. Pacemaker es un ejemplo de una entidad de clúster externo. Cuando es externo, el tipo de clúster del grupo de disponibilidad 

* Conjunto de réplicas principales y secundarias `FAILOVER_MODE = EXTERNAL`. 
   Especifica que la réplica se interactúa con un administrador de clúster externo, como Pacemaker. 

Los scripts de Transact-SQL siguientes crean un grupo de disponibilidad para alta disponibilidad denominado `ag1`. El script configura las réplicas de grupo de disponibilidad con `SEEDING_MODE = AUTOMATIC`. Esta configuración hace que SQL Server crear automáticamente la base de datos en cada servidor secundario. Actualice el script siguiente para su entorno. Reemplace el `<node1>`, `<node2>`, o `<node3>` valores con los nombres de las instancias de SQL Server que hospedan las réplicas. Reemplace el `<5022>` con el puerto se establecen para el extremo de reflejo de datos. Para crear el grupo de disponibilidad, ejecute el siguiente Transact-SQL en la instancia de SQL Server que hospeda la réplica principal.

Ejecute **sola** de los siguientes scripts: 

- [Crear grupo de disponibilidad con tres réplicas sincrónicas](#threeSynch).
- [Crear grupo de disponibilidad con dos réplicas sincrónicas y una réplica de la configuración](#configOnly)
- [Crear grupo de disponibilidad con dos réplicas sincrónicas](#readScale).

<a name="threeSynch"></a>

- Crear grupo de disponibilidad con tres réplicas sincrónicas

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >Después de ejecutar el script anterior para crear un grupo de disponibilidad con tres réplicas sincrónicas, no ejecute el siguiente script:

- Crear grupo de disponibilidad con dos réplicas sincrónicas y una réplica de la configuración:

   >[!IMPORTANT]
   >Esta arquitectura permite que cualquier edición de SQL Server para hospedar la réplica terceros. Por ejemplo, la tercera réplica puede hospedarse en SQL Server Enterprise Edition. En Enterprise Edition, es el tipo de punto de conexión válido sólo `WITNESS`. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- Crear grupo de disponibilidad con dos réplicas sincrónicas

   Incluya las dos réplicas con el modo de disponibilidad sincrónica. Por ejemplo, el script siguiente crea un grupo de disponibilidad denominado `ag1`. `node1` y `node2` hospedan las réplicas en modo sincrónico con conmutación automática por error y la propagación automática.

   >[!IMPORTANT]
   >Solo se ejecute el siguiente script para crear un grupo de disponibilidad con dos réplicas sincrónicas. No se ejecute el siguiente script si se ha ejecutado un script anterior. 

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


También puede configurar un grupo de disponibilidad con `CLUSTER_TYPE=EXTERNAL` mediante SQL Server Management Studio o PowerShell. 

### <a name="join-secondary-replicas-to-the-ag"></a>Une las réplicas secundarias al grupo de disponibilidad

El usuario de pacemaker requiere `ALTER`, `CONTROL`, y `VIEW DEFINITION` permisos en el grupo de disponibilidad en todas las réplicas. Para conceder permisos, ejecute el siguiente script de Transact-SQL una vez creado el grupo de disponibilidad en la réplica principal y en cada réplica secundaria inmediatamente después de agregarlos al grupo de disponibilidad. Antes de ejecutar el script, reemplace `<pacemakerLogin>` con el nombre de la cuenta de usuario de pacemaker.

```Transact-SQL
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

El siguiente script de Transact-SQL une a una instancia de SQL Server a un grupo de disponibilidad denominado `ag1`. Actualice el script para su entorno. En cada instancia de SQL Server que hospeda una réplica secundaria, ejecute el siguiente Transact-SQL para unir el grupo de disponibilidad.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Después de crear el grupo de disponibilidad, debe configurar la integración con una tecnología de clúster como Pacemaker para lograr alta disponibilidad. Para una configuración de escalado de lectura con AG, empezando por [!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)], no es necesario configurar un clúster.

Si ha seguido los pasos descritos en este documento, tiene un grupo de disponibilidad que no está en clúster. El siguiente paso es agregar el clúster. Esta configuración es válida para los escenarios de equilibrio de carga o escalado de lectura, no está completo para la alta disponibilidad. Para lograr alta disponibilidad, deberá agregar el grupo de disponibilidad como un recurso de clúster. Consulte [pasos siguientes](#next-steps) para obtener instrucciones. 

## <a name="notes"></a>Notas

>[!IMPORTANT]
>Después de configurar el clúster y agregar el grupo de disponibilidad como un recurso de clúster, no puede utilizar Transact-SQL para conmutar los recursos del grupo de disponibilidad. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio de SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En RHEL o Ubuntu usar `pcs`. En SLES usar `crm`. 

>[!IMPORTANT]
>Si el grupo de disponibilidad es un recurso de clúster, hay un problema conocido en la versión actual, donde la conmutación por error forzada con pérdida de datos a una réplica asincrónica no funciona. Esto se corregirá en la próxima versión. Se realiza correctamente la conmutación por error de manual o automática a una réplica sincrónica.


## <a name="next-steps"></a>Pasos siguientes

[Configurar el clúster de Red Hat Enterprise Linux para recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configuración de clúster SUSE Linux Enterprise Server para los recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar el clúster de Ubuntu para recursos de clúster del grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
