---
title: "Inicios de sesión y trabajos de las bases de datos de grupo de disponibilidad | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: d7da14d3-848c-44d4-8e49-d536a1158a61
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f431b401f2bc3e14dfea116d9c5be0c2d3fd18cc
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="logins-and-jobs-for-availability-group-databases"></a>Inicios de sesión y trabajos de las bases de datos de grupo de disponibilidad
  Debe mantener de forma sistemática el mismo conjunto de inicios de sesión de usuario y de trabajos del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en cada base de datos principal de un grupo de disponibilidad AlwaysOn y sus correspondientes bases de datos secundarias. Los inicios de sesión y los trabajos se deben reproducir en cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospede una réplica de disponibilidad para el grupo de disponibilidad.  
  
-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Trabajos de agente**  
  
     Debe copiar manualmente los trabajos pertinentes de la instancia de servidor que hospeda la réplica principal original a las instancias de servidor que hospedan las réplicas secundarias originales. Para todas las bases de datos, debe agregar lógica al principio de cada trabajo importante para que el trabajo solo se ejecute en la base de datos principal; es decir, solo cuando la réplica local sea la réplica principal de la base de datos.  
  
     Las instancias de servidor que hospedan las réplicas de disponibilidad de un grupo de disponibilidad se pueden configurar de forma diferente, con letras de unidad de cinta distintas, etc. Los trabajos para cada réplica de disponibilidad deben permitir tales diferencias.  
  
     Cabe mencionar que los trabajos de copia de seguridad pueden usar la función [sys.fn_hadr_is_preferred_backup_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) para identificar si la réplica local es la preferida para las copias de seguridad, según las preferencias de copia de seguridad del grupo de disponibilidad. Los trabajos de copia de seguridad creados mediante el [Asistente para planes de mantenimiento](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md) usan esta función de forma nativa. Para otros trabajos de copia de seguridad, se recomienda usar esta función como condición de los trabajos de copia de seguridad, de forma que solo se ejecuten en la réplica preferida. Para obtener más información, vea [Secundarias activas: copia de seguridad en las réplicas secundarias &#40;grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
-   **Inicios de sesión**  
  
     Si usa bases de datos independientes, puede configurar usuarios independientes en las bases de datos, y para estos usuarios no es necesario crear inicios de sesión en las instancias de servidor que hospedan una réplica secundaria. En el caso de una base de datos de disponibilidad dependiente, deberá crear usuarios para los inicios de sesión en las instancias de servidor que hospedan las réplicas de disponibilidad. Para obtener más información, vea [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md).  
  
     Si ninguna de las aplicaciones usa la autenticación [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o un inicio de sesión local de Windows, vea [Inicios de sesión de aplicaciones que usan la autenticación de SQL Server o un inicio de sesión local de Windows](../../../database-engine/availability-groups/windows/logins-and-jobs-for-availability-group-databases.md#SSauthentication), más adelante en este tema.  
  
    > [!NOTE]  
    >  Un usuario de base de datos cuyo inicio de sesión de SQL Server está sin definir o se ha definido de forma incorrecta en una instancia de servidor no podrá iniciar una sesión en la instancia. Es lo que se denomina un *usuario huérfano* de la base de datos en esa instancia de servidor. Si un usuario está huérfano en una instancia de servidor determinada, puede configurar los inicios de sesión de usuario en cualquier momento. Para obtener más información, vea [Solucionar problemas de usuarios huérfanos &#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md).  
  
-   **Metadatos adicionales**  
  
     Los inicios de sesión y los trabajos no son la única información que es necesario volver a crear en cada instancia de servidor que hospeda una réplica secundaria para un grupo de disponibilidad determinado. Por ejemplo, quizás necesite volver a crear la configuración del servidor, las credenciales, los datos cifrados, los permisos, la configuración de replicación, las aplicaciones de Service Broker, los desencadenadores (en el nivel de servidor), etc. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="SSauthentication"></a> Inicios de sesión de aplicaciones que usan la autenticación de SQL Server o un inicio de sesión local de Windows  
 Si una aplicación usa la Autenticación de SQL Server o un inicio de sesión local de Windows, los SID que no coinciden pueden impedir que el inicio de sesión de la aplicación se resuelva en una instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los SID que no coincidan harán que el inicio de sesión sea un usuario huérfano en la instancia del servidor remoto. Este problema puede producirse cuando una aplicación se conecta con una base de datos reflejada o de trasvase de registros después de una conmutación por error o con una base de datos Suscriptor de replicación que se inicializó desde una copia de seguridad.  
  
 Para evitar que se produzca este problema, se recomienda tomar medidas preventivas al configurar una aplicación de este tipo para que utilice una base de datos hospedada por una instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La prevención implica la transferencia de los inicios de sesión y las contraseñas de la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información sobre cómo evitar que se produzca este problema, vea el artículo de KB 918992:[Cómo transferir inicios de sesión y contraseñas entre instancias de SQL Server 2005 y 2008](http://support.microsoft.com/kb/918992/).  
  
> [!NOTE]  
>  Este problema afecta a las cuentas locales de Windows en distintos equipos. Sin embargo, este problema no ocurre en las cuentas de dominio debido a que el SID es el mismo en todos los equipos.  
  
 Para obtener más información, vea [Usuarios huérfanos con creación de reflejo de la base de datos y trasvase de registros](http://blogs.msdn.com/b/sqlserverfaq/archive/2009/04/13/orphaned-users-with-database-mirroring-and-log-shipping.aspx) (un blog del motor de base de datos).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear un inicio de sesión](../../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [Create a Database User](../../../relational-databases/security/authentication-access/create-a-database-user.md).  
  
-   [Crear un trabajo](http://msdn.microsoft.com/library/b35af2b6-6594-40d1-9861-4d5dd906048c)  
  
-   [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Bases de datos independientes](../../../relational-databases/databases/contained-databases.md)   
 [Crear trabajos](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b)  
  
  

