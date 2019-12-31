---
title: Creación y configuración de grupos de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], creating
ms.assetid: 7f89fab8-6ee2-4273-9de0-e594bfb9407f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9858638287876d31733035d1a6bb6d95705708f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228720"
---
# <a name="creation-and-configuration-of-availability-groups-sql-server"></a>Creación y configuración de grupos de disponibilidad (SQL Server)
  Los temas de esta sección explican la forma de implementar una implementación de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en instancias de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] que residen en nodos diferentes de clústeres de conmutación por error de Windows Server (WSFC) dentro de un único clúster de conmutación por error de WSFC.  
  
 Antes de crear el primer grupo de disponibilidad, se recomienda encarecidamente que se familiarice con la información de los temas siguientes:  
  
 [Requisitos previos, restricciones y recomendaciones para el SQL Server de &#40;de Grupos de disponibilidad AlwaysOn&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
 En este tema se describen los requisitos previos, restricciones y recomendaciones para equipos; los nodos de WSFC; las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; los grupos, réplicas y bases de datos de disponibilidad. Este tema también contiene información sobre consideraciones de seguridad.  
  
 [Introducción con Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
 Incluye información sobre los pasos para configurar una instancia de servidor, crear un grupo de disponibilidad, configurar el grupo de disponibilidad para las conexiones de cliente, administrar los grupos de disponibilidad y supervisar los grupos de disponibilidad.  
  
 
  
##  <a name="RelatedTasks"></a>Tareas relacionadas  
 **Para configurar una instancia de servidor para[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [Habilitar y deshabilitar Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Cree un extremo de creación de reflejo de la base de datos para Grupos de disponibilidad AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Crear un extremo de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Permitir que un extremo de creación de reflejo de la base de datos use certificados para las conexiones salientes &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
 **Para comenzar a configurar los grupos de disponibilidad AlwaysOn**  
  
-   [Introducción con Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **Para crear y configurar un nuevo grupo de disponibilidad**  
  
-   [Use el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Crear un grupo de disponibilidad &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Cree un grupo de disponibilidad &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Use el cuadro de diálogo nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Especifique la dirección URL del extremo al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Cree o configure un agente de escucha del grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar la directiva de conmutación por error flexible para controlar las condiciones de la conmutación automática por error (grupos de disponibilidad AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
-   [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Unir una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Iniciar el movimiento de datos en una base de datos secundaria AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Administración de inicios de sesión y trabajos para las bases de datos de un grupo de disponibilidad &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **Para solucionar problemas**  
  
-   [Solucionar problemas de configuración de Grupos de disponibilidad AlwaysOn (SQL Server) eliminada](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Solucionar problemas de una operación Add-File &#40;Grupos de disponibilidad AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a>Contenido relacionado  
  
-   **Blogs**  
  
     [Series de aprendizaje de AlwaysON - HADRON: uso del grupo de trabajo para las bases de datos compatibles con HADRON](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Blogs del equipo de AlwaysOn de SQL Server: el blog oficial del equipo de AlwaysOn de SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos**  
  
     [Microsoft SQL Server Code-Named "Denali", Serie AlwaysOn, parte 1: Introducción a la solución de alta disponibilidad de siguiente generación](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server “Denali”, Serie AlwaysOn, parte 2: Crear una solución esencial de alta disponibilidad utilizando AlwaysOn](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **White**  
  
     [Guía de soluciones AlwaysOn de Microsoft SQL Server para lograr alta disponibilidad y recuperación ante desastres](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Notas del producto de Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto de SQL Server Customer Advisory](http://sqlcat.com/)  
  
## <a name="see-also"></a>Véase también  
 [Información general de Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Administración de un grupo de disponibilidad &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [Directivas de AlwaysOn para problemas operativos con Grupos de disponibilidad AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Supervisión de grupos de disponibilidad &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Grupos de disponibilidad AlwaysOn: interoperabilidad (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)  
  
