---
title: Los suscriptores de replicación y grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eac9f39478b66df98de0483f8dc68d3e671ce045
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62789151"
---
# <a name="replication-subscribers-and-alwayson-availability-groups-sql-server"></a>Suscriptores de replicación y grupos de disponibilidad AlwaysOn (SQL Server)
  Cuando el grupo de disponibilidad AlwaysOn que contiene una base de datos que es un suscriptor de replicación realiza una conmutación por error, se puede producir un error en la suscripción de replicación. Para los suscriptores de inserción de replicación transaccional, el agente de distribución se seguirá replicando automáticamente después de una conmutación por error si la suscripción se creó mediante el nombre de la escucha de grupo de disponibilidad. Para los suscriptores de extracción de replicación transaccional, el agente de distribución se seguirá replicando automáticamente después de una conmutación por error si la suscripción se creó mediante el nombre de la escucha de grupo de disponibilidad y el servidor del suscriptor original está activo y en ejecución. El motivo es que los trabajos del agente de distribución solo se crean en el suscriptor original (réplica principal del grupo de disponibilidad). Para los suscriptores de mezcla, un administrador de replicación debe volver a configurar manualmente el suscriptor volviendo a crear la suscripción.  
  
## <a name="what-is-supported"></a>Qué se admite  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite la conmutación por error automática del publicador, la conmutación por error de suscriptores transaccionales y la conmutación por error manual de los suscriptores de mezcla. No se admite la conmutación por error de un distribuidor de una base de datos de disponibilidad. AlwaysOn no puede combinarse con escenarios de Websync ni [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Compact.  
  
 **Conmutación por error de una suscripción de extracción de mezcla**  
  
 Se produce un error en una suscripción de extracción tras la conmutación por error del grupo de disponibilidad porque el agente de extracción no puede encontrar los trabajos almacenados en la base de datos **msdb** de la instancia de servidor que hospeda la réplica principal, que no está disponible porque se ha producido un error en la instancia de servidor.  
  
 **Conmutación por error de una suscripción de inserción de mezcla**  
  
 Se produce un error en una suscripción de inserción tras la conmutación por error del grupo de disponibilidad porque el agente de inserción ya no puede conectarse a la base de datos de suscripciones original en el suscriptor original.  
  
## <a name="how-to-create-transactional-subscription-in-an-alwayson-environment"></a>Cómo crear una suscripción transaccional en un entorno de AlwaysOn  
 Para la replicación transaccional, utilice los pasos siguientes para configurar y conmutar por error un grupo de disponibilidad de suscriptor:  
  
1.  Antes de crear la suscripción, agregue la base de datos del suscriptor al grupo de disponibilidad AlwaysOn adecuado.  
  
2.  Agregue el agente de escucha del grupo de disponibilidad del suscriptor como un servidor vinculado a todos los nodos del grupo de disponibilidad. Este paso garantiza que todos los posibles asociados de conmutación por error sean conscientes del agente de escucha y se puedan conectar al mismo.  
  
3.  Con el script de la sección **Crear una suscripción de inserción para una replicación transaccional** de más abajo, cree la suscripción y use el nombre del agente de escucha del grupo de disponibilidad del suscriptor. Después de una conmutación por error, el nombre del agente de escucha siempre sigue siendo válido, mientras que el nombre de servidor real del suscriptor dependerá del nodo real que se convirtió en el nuevo primario.  
  
    > [!NOTE]  
    >  Es preciso que la suscripción se cree mediante un script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] y no se puede crear con [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
4.  Si se va a crear una suscripción de extracción:  
  
    1.  En [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], en el nodo principal del suscriptor, abra el árbol del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    2.  Identifique el trabajo **Agente de distribución de extracción** y edite el trabajo.  
  
    3.  En el paso de trabajo **Ejecutar agente** , active los parámetros `-Publisher` y `-Distributor` . Asegúrese de que estos parámetros contienen los nombres de servidor y de instancia directos correctos del servidor del publicador y del distribuidor.  
  
    4.  Cambie el parámetro `-Subscriber` al nombre del agente de escucha del grupo de disponibilidad del suscriptor.  
  
 Cuando cree la suscripción siguiendo estos pasos, no tendrá que hacer nada tras una conmutación por error.  
  
## <a name="creating-a-transactional-replication-push-subscription"></a>Crear una suscripción de inserción para una replicación transaccional  
  
```  
-- commands to execute at the publisher, in the publisher database:  
use [<publisher database name>]  
EXEC sp_addsubscription @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @destination_db = N'<subscriber database name>',   
       @subscription_type = N'Push',   
       @sync_type = N'automatic', @article = N'all', @update_mode = N'read only', @subscriber_type = 0;  
GO  
  
EXEC sp_addpushsubscription_agent @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @subscriber_db = N'<subscriber database name>',   
       @job_login = null, @job_password = null, @subscriber_security_mode = 1;  
GO  
```  
  
## <a name="to-resume-the-merge-agents-after-the-availability-group-of-the-subscriber-fails-over"></a>Para reanudar los agentes de mezcla después de la conmutación por error del grupo de disponibilidad del suscriptor  
 Para la replicación de mezcla, un administrador de replicación debe volver a configurar manualmente el suscriptor con los pasos siguientes:  
  
1.  Ejecute `sp_subscription_cleanup` para eliminar la suscripción antigua del suscriptor. Realice esta acción en la nueva réplica principal (que era antes la réplica secundaria).  
  
2.  Vuelva a crear la suscripción, para ello cree una nueva suscripción, comenzando por una nueva instantánea.  
  
> [!NOTE]  
>  El proceso actual no es apto para los suscriptores de replicación de mezcla, aunque el escenario principal para la replicación de mezcla son los usuarios desconectados (escritorio, equipos portátiles, dispositivos de auricular) que no utilizarán los grupos de disponibilidad AlwaysOn en el suscriptor.  
  
  
