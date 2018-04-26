---
title: 'Creación de reflejo de la base de datos: interoperabilidad y coexistencia (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc1edc91226f5b8d20e982c9b1234f32db5cee44
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>Creación de reflejo de la base de datos: interoperabilidad y coexistencia (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La creación de reflejo de la base de datos se puede utilizar con las siguientes características o componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Instancias de clúster de conmutación por error de AlwaysOn (clústeres de conmutación por error de SQL Server)](../../database-engine/database-mirroring/database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [Captura de datos modificados (y seguimiento de cambios)](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [Instantáneas de base de datos](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
-   [Catálogos de texto completo](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [Trasvase de registros](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [Replicación](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
 La creación de reflejo de la base de datos no interopera con lo siguiente:  
  
-   Transacciones entre bases de datos y transacciones distribuidas  
  
     Para obtener más información sobre por qué dichas transacciones no se admiten, vea [Transacciones entre bases de datos no compatibles para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
