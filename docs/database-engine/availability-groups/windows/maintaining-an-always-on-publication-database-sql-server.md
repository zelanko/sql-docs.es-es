---
title: Mantener una base de datos de publicación AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 55b345fe-2eb9-4b04-a900-63d858eec360
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 98d565fa9b504c6a131dcd348778be9eb61047b4
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34769711"
---
# <a name="maintaining-an-always-on-publication-database-sql-server"></a>Mantener una base de datos de publicación AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se tratan consideraciones especiales para mantener una base de datos de publicación cuando se usan grupos de disponibilidad AlwaysOn.  
  
 **En este tema:**  
  
-   [Mantener una base de datos publicada en un grupo de disponibilidad](#MaintainPublDb)  
  
-   [Quitar una base de datos publicada de un grupo de disponibilidad](#RemovePublDb)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="MaintainPublDb"></a> Mantener una base de datos publicada en un grupo de disponibilidad  
 El mantenimiento de una base de datos de publicación AlwaysOn se realiza básicamente de la misma forma que para una base de datos de publicación estándar, con las siguientes salvedades:  
  
-   La administración debe producirse en el host de réplica principal. En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], las publicaciones aparecen bajo la carpeta de **Publicaciones locales** para el host de réplica principal y también para las réplicas secundarias legibles. Después de la conmutación por error, puede que tenga que actualizar manualmente [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] para que el cambio quede reflejado si el elemento secundario promovido a principal no era legible.  
  
-   El Monitor de replicación muestra siempre la información de publicación en el publicador original. Sin embargo, esta información se puede ver en el Monitor de replicación de cualquier réplica al agregar el publicador original como servidor.  
  
-   Si se utilizan procedimientos almacenados o Replication Management Objects (RMO) para administrar la replicación en la réplica principal actual, en los casos en que se especifica el nombre del publicador, se debe especificar el nombre de la instancia en la que la base de datos se habilitó para la replicación (el publicador original). Para determinar el nombre correcto, use la función **PUBLISHINGSERVERNAME** . Cuando una base de datos de publicación se une a un grupo de disponibilidad, los metadatos de replicación almacenados en las réplicas de la base de datos secundaria son idénticos a los de la principal. En consecuencia, para las bases de datos de publicación habilitadas para replicación en la entidad principal, el nombre de la instancia del publicador que está almacenado en las tablas del sistema en la entidad secundaria es el nombre de la entidad principal en lugar del nombre de la entidad secundaria. Esto afecta a la configuración y al mantenimiento de la replicación si se produce la conmutación por error de la base de datos de publicación a la entidad secundaria. Por ejemplo, si configura la replicación con procedimientos almacenados en una entidad secundaria después de la conmutación por error y quiere una suscripción de extracción a una base de datos de publicación que se habilitó en otra réplica, debe especificar el nombre del publicador original en lugar del publicador actual como parámetro *@publisher* de **sp_addpullsubscription** o **sp_addmergepulllsubscription**. Sin embargo, si habilita una base de datos de publicación después de la conmutación por error, el nombre de la instancia del publicador almacenado en las tablas del sistema es el nombre del host principal actual. En este caso, usaría el nombre de host de réplica principal actual para el parámetro *@publisher* .  
  
    > [!NOTE]  
    >  En algunos procedimientos, como **sp_addpublication**, el parámetro *@publisher* solo se admite para publicadores que no sean instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. En estos casos, no es relevante para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn.  
  
-   Para sincronizar una suscripción en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] tras una conmutación por error, sincronice las suscripciones de extracción del suscriptor y sincronice las suscripciones de inserción del publicador activo.  
  
##  <a name="RemovePublDb"></a> Quitar una base de datos publicada de un grupo de disponibilidad  
 Tenga en cuenta los siguientes problemas si quita una base de datos publicada de un grupo de disponibilidad, o si quita un grupo de disponibilidad que tiene una base de datos de miembros publicada.  
  
-   Si la base de datos de publicación del publicador original se quita de la réplica principal de un grupo de disponibilidad, debe ejecutar **sp_redirect_publisher** sin especificar un valor para el parámetro *@redirected_publisher* a fin de quitar el redireccionamiento del par publicador y base de datos.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB';  
    ```  
  
     La base de datos se quedará en el estado de recuperación en el servidor principal y debe restaurarse. Una vez que haya realizado esto, la replicación debe funcionar sin cambios en el publicador original.  
  
-   Si la base de datos de publicación conmuta por error desde el publicador original a una réplica y la base de datos se quita de la réplica principal del grupo de disponibilidad, use el procedimiento almacenado **sp_redirect_publisher** para redirigir explícitamente el publicador original al nuevo publicador. La base de datos se quedará en el estado de recuperación y debe restaurarse. Una vez que haya realizado esto, la replicación debe continuar funcionando como lo hizo con el grupo de disponibilidad.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB',  
        @redirected_publisher = 'MyNewPublisher';  
    ```  
  
     No quite el servidor remoto para el publicador original del distribuidor, incluso si ya no se puede tener acceso al servidor. Los metadatos de servidor del publicador original son necesarios en el distribuidor para satisfacer las consultas de los metadatos de la publicación.  
  
-   Si se quita un grupo de disponibilidad completo, el comportamiento con respecto a una base de datos replicada de miembros es el mismo que cuando se quita una base de datos publicada de un grupo de disponibilidad. La replicación se puede reanudar desde el último servidor principal tan pronto como se haya restaurado la base de datos y se haya modificado la redirección. Si la base de datos se restaura en su publicador original, debe quitase la redirección. Si la base de datos se restaura en un host diferente, la redirección debe ejecutarse explícitamente el nuevo host.  
  
    > [!NOTE]  
    >  Cuando se quita un grupo de disponibilidad que ha publicado bases de datos de miembros o una base de datos publicada de un grupo de disponibilidad, todas las copias de las bases de datos publicadas se dejarán en estado de recuperación. Si se restaura, cada una aparecerá como base de datos publicada. Solo se debe conservar una copia con los metadatos de la publicación. Para deshabilitar la replicación para una copia de la base de datos publicada, primero debe quitar todas las suscripciones y publicaciones de la base de datos.  
  
     Ejecute **sp_dropsubscription** para quitar las suscripciones de publicaciones. Asegúrese de establecer el parámetro *@ignore_distributributor* en 1 para mantener los metadatos de la base de datos de publicación activa en el distribuidor.  
  
    ```  
    USE MyDBName;  
    GO  
  
    EXEC sys.sp_dropsubscription   
        @subscriber = 'MySubscriber',  
        @publication = 'MyPublication',  
        @article = 'all',  
        @ignore_distributor = 1;  
    ```  
  
     Ejecute **sp_droppublication** para quitar todas las publicaciones. De nuevo, establezca el parámetro *@ignore_distributor* en 1 para mantener los metadatos de la base de datos de publicación activa en el distribuidor.  
  
    ```  
    EXEC sys.sp_droppublication   
        @publication = 'MyPublication',  
        @ignore_distributor = 1;  
    ```  
  
     Ejecute **sp_replicationdboption** para deshabilitar la replicación de la base de datos.  
  
    ```  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'false';  
    ```  
  
     En este momento, la copia de la base de datos publicada se puede conservar o quitar.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Configurar la replicación para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)  
  
-   [Replicación, seguimiento de cambios, captura de datos modificados y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)  
  
-   [Administración &#40;replicación&#41;](../../../relational-databases/replication/administration/administration-replication.md)  
  
-   [Suscriptores de replicación y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)  
  
## <a name="see-also"></a>Ver también  
 [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Grupos de disponibilidad AlwaysOn: interoperabilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [Replicación de SQL Server](../../../relational-databases/replication/sql-server-replication.md)  
  
  
