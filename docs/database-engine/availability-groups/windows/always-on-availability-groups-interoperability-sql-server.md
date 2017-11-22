---
title: 'Grupos de disponibilidad AlwaysOn: interoperabilidad (SQL Server) | Microsoft Docs'
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
caps.latest.revision: "21"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5b02338f5f8aaef958db4f7505341a7f13a8ce9f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>Grupos de disponibilidad AlwaysOn: interoperabilidad (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se documenta la interoperabilidad de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] con otras características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
##  <a name="Interop"></a> Características que interoperan con los grupos de disponibilidad AlwaysOn  
 En la tabla siguiente se enumeran las características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que interoperan con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Los vínculos de la columna **Más información** indican que existen consideraciones de interoperabilidad sobre una determinada característica.  
  
|Característica|Más información|  
|-------------|----------------------|  
|Captura de datos modificados|[Replicación, seguimiento de cambios, captura de datos modificados y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|  
|Seguimiento de cambios|[Replicación, seguimiento de cambios, captura de datos modificados y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|  
|Bases de datos independientes|[Bases de datos independientes con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/contained-databases-with-always-on-availability-groups-sql-server.md)|  
|Clave de cifrado de la base de datos|[Bases de datos cifradas con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md)|  
|Instantáneas de base de datos|[Instantáneas de base de datos con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md)|  
|FILESTREAM y FileTable|[FILESTREAM y FileTable con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|  
|Búsqueda de texto completo|Nota: Los índices de texto completo se sincronizan con las bases de datos secundarias AlwaysOn.|  
|Trasvase de registros|[Requisitos previos para migrar desde grupos de trasvase de registros a grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|  
|Almacén remoto de blobs (RBS)|[Almacén remoto de blobs &#40;RBS&#41; y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|  
|Replicación|[Configurar la replicación para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [Mantener una base de datos de publicación AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [Replicación, seguimiento de cambios, captura de datos modificados y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [Suscriptores de replicación y Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)|  
|Analysis Services|[Analysis Services con grupos de disponibilidad AlwaysOn](../../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)|  
|Reporting Services|Use réplicas secundarias de solo lectura como un origen de datos de notificación y reduzca la carga en la réplica de lectura-escritura principal.<br /><br /> [Reporting Services con Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)|  
|Service Broker|[Service Broker con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)|  
|Agente SQL Server||  
  
##  <a name="restrictions"></a> Características que interoperan con los grupos de disponibilidad AlwaysOn con restricciones  
 Las siguientes características interoperan con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] con restricciones específicas. Para obtener detalles, consulte los temas vinculados.  
  
-   Transacciones entre bases de datos o transacciones distribuidas ([!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] y Windows Server 2016). Para obtener más información, vea [Transacciones entre bases de datos no compatibles para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
##  <a name="NoInterop"></a> Características que no interoperan con los grupos de disponibilidad AlwaysOn  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no interopera con las siguientes características:  
  
-   Creación de reflejo de base de datos. Para obtener más información, vea [Transacciones entre bases de datos y transacciones distribuidas para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [Guía de migración: migrar a clústeres de conmutación por error y grupos de disponibilidad de SQL Server 2012 desde implementaciones anteriores de agrupación en clústeres y creación de reflejo](https://blogs.msdn.microsoft.com/sqlalwayson/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments/)  
  
     [Blogs del equipo de AlwaysOn de SQL Server: blog oficial del equipo de AlwaysOn de SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](http://blogs.msdn.com/b/psssql/)  
  
-   **Notas del producto:**  
  
     [Guía de migración: migrar a grupos de disponibilidad AlwaysOn desde implementaciones anteriores que combinan creación de reflejo de la base de datos y trasvase de registros](http://msdn.microsoft.com/library/jj635217)  
  
     [Guía de soluciones AlwaysOn de Microsoft SQL Server para lograr alta disponibilidad y recuperación ante desastres](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Notas del producto de Microsoft para SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
