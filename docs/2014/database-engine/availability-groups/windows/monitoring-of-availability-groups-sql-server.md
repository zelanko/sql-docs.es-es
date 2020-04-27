---
title: Supervisión de los grupos de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 1d5e3291-0d0a-45a1-88e5-1fc242d17210
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1793032a72ae1dd150caa5ddd1739f7f5620bce1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62790201"
---
# <a name="monitoring-of-availability-groups-sql-server"></a>Supervisión de los grupos de disponibilidad (SQL Server)
  Para supervisar las propiedades y el estado de un grupo de disponibilidad AlwaysOn, puede utilizar las siguientes herramientas.  
  
|Herramienta|Breve descripción|Vínculos|  
|----------|-----------------------|-----------|  
|Paquete de supervisión de System Center para SQL Server|El paquete de supervisión de SQL Server (SQLMP) es la solución recomendada para supervisar los grupos de disponibilidad y las bases de datos de disponibilidad y de replicación de disponibilidad para los administradores TIC. Entre las características de supervisión que son de particular importancia para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se incluyen las siguientes:<br /><br /> La detectabilidad automática de los grupos de disponibilidad, las réplicas de disponibilidad y la base de datos de disponibilidad entre cientos de equipos. Esto le permite realizar fácilmente el seguimiento del inventario de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .<br /><br /> Alertas y vales de System Center Operations Manager (SCOM). Estas características proporcionan un conocimiento detallado que permite una resolución más rápida de un problema.<br /><br /> Una extensión personalizada de la supervisión del estado de AlwaysOn mediante la administración basada en directivas (PBM).<br /><br /> El estado abarca desde las bases de datos de disponibilidad a las réplicas de disponibilidad.<br /><br /> Tareas personalizadas que administran [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] desde la consola de System Center Operations Manager.|Para descargar el módulo de supervisión (SQLServerMP.msi) y la *Guía del módulo de administración de SQL Server para System Center Operations Manager* (SQLServerMPGuide.doc), vea:<br /><br /> [Paquete de supervisión de System Center para SQL Server](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] proporcionan una gran cantidad de información sobre los grupos de disponibilidad y las réplicas, bases de datos, escuchas y el entorno de clúster de WSFC.|[Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|El panel **Detalles del Explorador de objetos** muestra información básica acerca de los grupos de disponibilidad hospedados en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la que está conectado.<br /><br /> Sugerencia: Utilice este panel para seleccionar varios grupos, réplicas o bases de datos de disponibilidad y para realizar tareas administrativas rutinarias en los objetos seleccionados; por ejemplo, quitar de un grupo de disponibilidad varias réplicas o bases de datos de disponibilidad.|[Usar los detalles del Explorador de objetos para supervisar los grupos de disponibilidad &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|Los cuadros de diálogo**Propiedades** permiten ver las propiedades de los grupos de disponibilidad, las réplicas o los agentes de escucha y, en algunos casos, para cambiar la configuración.|[Ver las propiedades del grupo de disponibilidad &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)<br /><br /> [Ver las propiedades de una réplica de disponibilidad &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)<br /><br /> [Ver las propiedades del agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)|  
|Monitor de sistema|El objeto de rendimiento **SQLServer:Availability Replica** contiene contadores de rendimiento que proporcionan información sobre las réplicas de disponibilidad.|[SQL Server, réplica de disponibilidad](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|Monitor de sistema|El objeto de rendimiento **SQLServer:Database Replica** contiene contadores de rendimiento que proporcionan información sobre las bases de datos secundarias en una réplica secundaria dada.<br /><br /> El objeto **SQLServer:Databases** de SQL Server contiene contadores de rendimiento que supervisan las actividades del registro de transacciones, entre otras cosas. Los siguientes contadores son especialmente importantes para supervisar la actividad del registro de transacciones en bases de datos de disponibilidad: **Tiempo de escritura de vaciados de registro (ms)**, **Vaciados de registro/s**, **Errores de memoria caché de grupo de registros/s**, **Lecturas de disco de grupo de registros/s**y **Solicitudes de grupo de registros/s**.|[SQL Server, réplica de base de datos](../../../relational-databases/performance-monitor/sql-server-database-replica.md) y [SQL Server, objeto Databases](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [Modelo de estado AlwaysOn Parte 1: arquitectura del modelo de estado](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/09/overview-of-the-alwayson-manageability-health-model.aspx)  
  
     [Modelo de estado AlwaysOn Parte 2: el modelo de estado](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
     [Supervisar el estado de AlwaysOn con PowerShell Parte 1: información general básica de los cmdlets](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx)  
  
     [Supervisar el estado de AlwaysOn con PowerShell Parte 2: uso avanzado de los cmdlets](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx)  
  
     [Supervisar el estado de AlwaysOn con PowerShell Parte 3: una aplicación sencilla de supervisión](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx)  
  
     [Supervisar el estado de AlwaysOn con PowerShell Parte 4: integración con el Agente SQL Server](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx)  
  
     [Blogs del equipo de AlwaysOn de SQL Server: el blog oficial del equipo de AlwaysOn de SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Notas del producto:**  
  
     [Notas del producto de Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte también  
 [Grupos de disponibilidad AlwaysOn vistas de catálogo &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql)   
 [Grupos de disponibilidad AlwaysOn vistas y funciones de administración dinámica &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions)   
 [Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad &#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)   
 [Información general de Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [&#40;de reparación de página automática para grupos de disponibilidad y creación de reflejo de la base de datos&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
