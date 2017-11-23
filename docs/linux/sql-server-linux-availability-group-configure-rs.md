---
title: Configurar grupo de disponibilidad de la escala de lectura para SQL Server en Linux | Documentos de Microsoft
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
ms.openlocfilehash: bd3fa34a4fbfe40dfe184f7d5cf0e1f64372c8f2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="configure-read-scale-availability-group-for-sql-server-on-linux"></a>Configurar grupo de disponibilidad de la escala de lectura para SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Puede configurar un grupo de disponibilidad de la escala de lectura de SQL Server en Linux. Hay dos arquitecturas para grupos de disponibilidad. A *alta disponibilidad* arquitectura utiliza un administrador de clústeres para proporcionar mejor continuidad del negocio. Esta arquitectura también puede incluir las réplicas de la escala de lectura. Para crear la arquitectura de alta disponibilidad, consulte [Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md).

Este documento explica cómo crear un *lectura escala* grupo de disponibilidad sin un administrador de clústeres. Esta arquitectura proporciona solo sólo lectura escala. No proporciona alta disponibilidad.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Crear el grupo de disponibilidad

Cree el grupo de disponibilidad. Set `CLUSTER_TYPE = NONE`. Además, establecer cada réplica con `FAILOVER_MODE = NONE`. Aplicaciones de cliente análisis o informes de las cargas de trabajo directamente pueden conectarse a bases de datos secundarias. También puede crear una lista de enrutamiento de solo lectura. Las conexiones a la réplica principal al día leen las solicitudes de conexión a cada una de las réplicas secundarias de la lista de enrutamiento en un modo de operación por turnos.

El script de Transact-SQL siguiente crea un nombre de grupo de disponibilidad `ag1`. La secuencia de comandos configura las réplicas del grupo de disponibilidad con `SEEDING_MODE = AUTOMATIC`. Esta configuración hace que SQL Server crear automáticamente la base de datos en cada servidor secundario después de agregarse al grupo de disponibilidad. Actualice el siguiente script para su entorno. Reemplace el `**<node1>**` y `**<node2>**` valores con los nombres de las instancias de SQL Server que hospedan las réplicas. Reemplace el `**<5022>**` con el puerto definido para el extremo. Ejecute el código Transact-SQL siguiente en la réplica principal de SQL Server:

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

El siguiente script de Transact-SQL une a un servidor a un grupo de disponibilidad denominado `ag1`. Actualizar la secuencia de comandos para su entorno. En cada réplica de SQL Server, ejecute el siguiente Transact-SQL para unirse al grupo de disponibilidad.

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

No se trata de una configuración de alta disponibilidad, si necesita alta disponibilidad, siga las instrucciones de [Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md). En concreto, cree el grupo de disponibilidad con `CLUSTER_TYPE=WSFC` (en Windows) o `CLUSTER_TYPE=EXTERNAL` (en Linux) e integrar con un administrador de clúster - a WSFC en Windows o bien marcapasos en Linux.

## <a name="connect-to-read-only-secondary-replicas"></a>Conectarse a réplicas secundarias de solo lectura

Hay dos formas de conectarse a las réplicas secundarias de solo lectura. Las aplicaciones pueden conectarse directamente a la instancia de SQL Server que hospeda la réplica secundaria y consultar las bases de datos, o pueden utilizar el enrutamiento de solo lectura. enrutamiento de solo lectura, requiere un agente de escucha.

[Réplicas secundarias legibles](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[enrutamiento de solo lectura](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-availability-group"></a>Conmutar por error la réplica principal en el grupo de disponibilidad de la escala de lectura

[!INCLUDE[Force Failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Pasos siguientes

[Configurar grupos de disponibilidad distribuidos](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[Más información acerca de los grupos de disponibilidad](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)

[Realizar una conmutación por error Manual forzada](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).

