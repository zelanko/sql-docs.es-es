---
title: Configurar un grupo de disponibilidad de la escala de lectura para SQL Server en Linux | Documentos de Microsoft
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 10/20/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 84fe8851a6ff3ad71e9ad9007bddc8715efc8829
ms.sourcegitcommit: c41e1bf5a53e96855b4424de4e0897153070bb28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2017
---
# <a name="configure-a-read-scale-availability-group-for-sql-server-on-linux"></a>Configurar un grupo de disponibilidad de la escala de lectura para SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Puede configurar un grupo de disponibilidad de la escala de lectura de SQL Server en Linux. Hay dos arquitecturas para grupos de disponibilidad. Una arquitectura de alta disponibilidad, utiliza un administrador de clústeres para proporcionar mejor continuidad del negocio. Esta arquitectura también puede incluir las réplicas de la escala de lectura. Para crear la arquitectura de alta disponibilidad, consulte [configurar un grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md).

Este documento explica cómo crear un grupo de disponibilidad de la escala de lectura sin un administrador de clústeres. Esta arquitectura proporciona solo lectura escala. No se ofrecen alta disponibilidad.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Crear el grupo de disponibilidad

Cree el grupo de disponibilidad. Set `CLUSTER_TYPE = NONE`. Además, establecer cada réplica con `FAILOVER_MODE = NONE`. Aplicaciones de cliente análisis o informes de las cargas de trabajo directamente pueden conectarse a bases de datos secundarias. También puede crear una lista de enrutamiento de solo lectura. Las conexiones a la réplica principal al día leen las solicitudes de conexión a cada una de las réplicas secundarias de la lista de enrutamiento en un modo round-robin.

El script de Transact-SQL siguiente crea un grupo de disponibilidad denominado `ag1`. La secuencia de comandos configura las réplicas del grupo de disponibilidad con `SEEDING_MODE = AUTOMATIC`. Esta configuración hace que SQL Server crear automáticamente la base de datos en cada servidor secundario después de agregarse al grupo de disponibilidad. Actualice el siguiente script para su entorno. Reemplace el `**<node1>**` y `**<node2>**` valores con los nombres de las instancias de SQL Server que hospedan las réplicas. Reemplace el `**<5022>**` valor con el puerto definido para el extremo. Ejecute el siguiente script de Transact-SQL en la réplica principal de SQL Server:

```SQL
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

El siguiente script de Transact-SQL une a un servidor a un grupo de disponibilidad denominado `ag1`. Actualizar la secuencia de comandos para su entorno. En cada réplica de SQL Server, ejecute el siguiente script de Transact-SQL para unirse al grupo de disponibilidad:

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

Este grupo de disponibilidad no es una configuración de alta disponibilidad. Si necesita alta disponibilidad, siga las instrucciones de [configurar un grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md). En concreto, cree el grupo de disponibilidad con `CLUSTER_TYPE=WSFC` (en Windows) o `CLUSTER_TYPE=EXTERNAL` (en Linux). A continuación, se integre con un administrador de clústeres con cualquier conmutación por error de Windows Server en Windows o marcapasos en Linux de agrupación en clústeres.

## <a name="connect-to-read-only-secondary-replicas"></a>Conectarse a réplicas secundarias de solo lectura

Hay dos maneras de conectarse a réplicas secundarias de solo lectura. Las aplicaciones pueden conectarse directamente a la instancia de SQL Server que hospeda la réplica secundaria y consultar las bases de datos. También puede usar enrutamiento de solo lectura, lo que requiere un agente de escucha.

* [Réplicas secundarias legibles](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [Enrutamiento de solo lectura](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>Conmutar por error la réplica principal en un grupo de disponibilidad de la escala de lectura

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Pasos siguientes

* [Configurar un grupo de disponibilidad distribuido](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)
* [Más información acerca de los grupos de disponibilidad](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)
* [Realizar una conmutación manual por error forzada](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)

