---
title: Suscriptores de replicación y grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9bba7c1a4274f3a239cc25e31f8f88687d8175af
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="replication-subscribers-and-always-on-availability-groups-sql-server"></a>Suscriptores de replicación y grupos de disponibilidad AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Cuando el grupo de disponibilidad AlwaysOn que contiene una base de datos que es un suscriptor de replicación realiza una conmutación por error, se puede producir un error en la suscripción de replicación. Para los suscriptores transaccionales, el agente de escucha seguirá replicando automáticamente si la suscripción usa el nombre del agente de escucha del grupo de disponibilidad del suscriptor. Para los suscriptores de mezcla, un administrador de replicación debe volver a configurar manualmente el suscriptor volviendo a crear la suscripción.  
  
## <a name="what-is-supported"></a>Qué se admite  
 La replicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite la conmutación por error automática del publicador y la conmutación por error automática de los suscriptores transaccionales. No se admite la conmutación por error de un distribuidor de una base de datos de disponibilidad. Los suscriptores de mezcla pueden ser parte de un grupo de disponibilidad, pero se requieren acciones manuales para configurar el suscriptor nuevo después de una conmutación por error. Los grupos de disponibilidad no pueden combinarse con los escenarios Websync y ssNoVersion Compact.  
  
## <a name="how-to-create-transactional-subscription-in-an-always-on-environment"></a>Cómo crear una suscripción transaccional en un entorno de AlwaysOn  
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
  
1.  Ejecute **sp_subscription_cleanup** para quitar la antigua suscripción para el suscriptor. Realice esta acción en la nueva réplica principal (que era antes la réplica secundaria).  
  
2.  Vuelva a crear la suscripción, para ello cree una nueva suscripción, comenzando por una nueva instantánea.  
  
> [!NOTE]  
>  El proceso actual no es apto para los suscriptores de replicación de mezcla, aunque el escenario principal para la replicación de mezcla son los usuarios desconectados (escritorio, equipos portátiles, dispositivos de auricular) que no usarán los grupos de disponibilidad AlwaysOn en el suscriptor.  
  
  
