---
title: "Creaci&#243;n de reflejo de la base de datos: interoperabilidad y coexistencia (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "alta disponibilidad [SQL Server], interoperabilidad y coexistencia"
  - "Motor de base de datos [SQL Server], alta disponibilidad"
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: 16
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 16
---
# Creaci&#243;n de reflejo de la base de datos: interoperabilidad y coexistencia (SQL Server)
  La creación de reflejo de la base de datos se puede utilizar con las siguientes características o componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Instancias de clúster de conmutación por error de AlwaysOn (clústeres de conmutación por error de SQL Server)](../../database-engine/database-mirroring/database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [Captura de datos modificados (y seguimiento de cambios)](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [Instantáneas de base de datos](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
-   [Catálogos de texto completo](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [Trasvase de registros](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [Replicación](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
 La creación de reflejo de la base de datos no interopera con lo siguiente:  
  
-   Transacciones entre bases de datos y transacciones distribuidas  
  
     Para obtener más información sobre por qué dichas transacciones no se admiten, vea [Transacciones entre bases de datos no compatibles para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions - always on availability and database mirroring.md).  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## Vea también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  