---
title: Administración de un grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], managing
ms.assetid: 0b7542fa-235e-413d-81bf-3eff9ee07480
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4896c9219632d816565fdd30c11aa82ccbf7fef1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791899"
---
# <a name="administration-of-an-availability-group-sql-server"></a>Administración de un grupo de disponibilidad (SQL Server)
  La administración de un grupo de disponibilidad AlwaysOn en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] implica una o varias de las siguientes tareas:  
  
-   Modificar las propiedades de una réplica de disponibilidad existente, por ejemplo para cambiar el acceso de la conexión de cliente (para configurar réplicas secundarias legibles), cambiar el modo de conmutación por error, el modo de disponibilidad o el valor de tiempo de espera de la sesión.  
  
-   Agregar o quitar réplicas secundarias.  
  
-   Agregar o quitar una base de datos.  
  
-   Suspender o reanudar una base de datos.  
  
-   Realizar una conmutación por error manual planeada (una *conmutación por error manual*) o una conmutación por error manual forzada (una *conmutación por error forzada*).  
  
-   Crear o configurar un agente de escucha del grupo de disponibilidad.  
  
-   Administrar [réplicas secundarias legibles](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) para un grupo de disponibilidad determinado. Esto implica la configuración de una o varias replica el acceso de solo lectura al ejecutar con rol secundario, y la configuración de enrutamiento de solo lectura.  
  
-   Administrar [copias de seguridad en las réplicas secundarias](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) para un grupo de disponibilidad determinado. Esto implica configurar desde donde prefiera que se ejecuten los trabajos de copia de seguridad y despues incluir en scripts los trabajos de copia de seguridad para implementar sus preferencias de copia de seguridad. necesita los trabajos de copia de seguridad de script para cada base de datos del grupo de la disponibilidad en cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda una réplica de disponibilidad.  
  
-   Eliminar un grupo de disponibilidad.  
  
-   Migración entre clústeres de grupos de disponibilidad AlwaysOn para la actualización del sistema operativo  
  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar un grupo de disponibilidad existente**  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Agregar una base de datos a un grupo de disponibilidad &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [Quitar una base de datos secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Quitar una base de datos principal de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Configurar la directiva de conmutación por error Flexible para controlar las condiciones para la conmutación automática por error &#40;grupos de disponibilidad AlwaysOn&#41;](configure-flexible-automatic-failover-policy.md)  
  
 **Para administrar un grupo de disponibilidad**  
  
-   [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Realizar una conmutación por error manual planeada de un grupo de disponibilidad &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Realizar una conmutación por error manual forzada de un grupo de disponibilidad &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Quitar un grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)  
  
 **Para administrar una réplica de disponibilidad**  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Cambiar el modo de disponibilidad de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Cambiar el modo de conmutación por error de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Cambiar el tiempo de espera de la sesión en una réplica de disponibilidad &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Para administrar una base de datos de disponibilidad**  
  
-   [Agregar una base de datos a un grupo de disponibilidad &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Quitar una base de datos principal de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Quitar una base de datos secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Suspender una base de datos de disponibilidad &#40;SQL Server&#41;](suspend-an-availability-database-sql-server.md)  
  
-   [Reanudar una base de datos de disponibilidad &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
 **Para supervisar un grupo de disponibilidad**  
  
-   [Supervisión de los grupos de disponibilidad &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
 **Para admitir la migración de grupos de disponibilidad a un nuevo clúster de WSFC (migración entre clústeres)**  
  
-   [Cambiar el contexto de clúster de HADR de la instancia de servidor &#40;SQL Server&#41;](change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
-   [Poner sin conexión un grupo de disponibilidad &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)  
  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [Blogs del equipo de AlwaysOn SQL Server: El blog del equipo de AlwaysOn oficial SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server Code-Named "Denali", serie AlwaysOn, parte 1: Introducción a la solución de alta disponibilidad de próxima generación](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named "Denali", serie AlwaysOn, parte 2: Creación de una solución esencial de alta disponibilidad utilizando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Notas del producto:**  
  
     [Notas del producto de Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](http://sqlcat.com/)  
  
  
## <a name="see-also"></a>Vea también  
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Configuración de una instancia del servidor para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)  
 [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Secundarias activas: Las réplicas secundarias legibles &#40;grupos de disponibilidad AlwaysOn&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Secundarias activas: Copia de seguridad en réplicas secundarias &#40;grupos de disponibilidad AlwaysOn&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Directivas de AlwaysOn para problemas operativos con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Supervisión de los grupos de disponibilidad &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Grupos de disponibilidad AlwaysOn: interoperabilidad &#40;SQL Server&#41;](always-on-availability-groups-interoperability-sql-server.md)   
 [Información general sobre instrucciones Transact-SQL para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](transact-sql-statements-for-always-on-availability-groups.md)   
 [Introducción a los PowerShell Cmdlets para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
