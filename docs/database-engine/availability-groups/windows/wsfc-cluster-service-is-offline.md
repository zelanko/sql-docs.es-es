---
title: "El servicio de cl&#250;ster de WSFC est&#225; sin conexi&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.agdashboard.agp1WSFCquorum.issues.f1"
helpviewer_keywords: 
  - "Grupos de disponibilidad [SQL Server], directivas"
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
caps.latest.revision: 16
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 16
---
# El servicio de cl&#250;ster de WSFC est&#225; sin conexi&#243;n
    
## Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de clúster de WSFC|  
|**Problema**|El servicio de clúster de WSFC está sin conexión.|  
|**Categoría**|**Crítico**|  
|**Faceta**|Instancia de SQL Server|  
  
## Descripción  
 Esta directiva comprueba el estado del clúster de conmutación por error de Windows Server (WSFC). La directiva está en mal estado y se genera una alerta cuando el clúster de WSFC está sin conexión o en el estado de quorum forzado. Todos los grupos de disponibilidad hospedados en este clúster están sin conexión o se requiere una acción de recuperación ante desastres.  
  
 El estado de la directiva es correcto cuando el estado del clúster está en el quorum normal.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [El servicio de clúster de WSFC está desconectado](http://go.microsoft.com/fwlink/p/?LinkId=220849) en TechNet Wiki.  
  
## Posibles causas  
 Esto puede deberse a un problema del servicio de clúster o a la pérdida del quorum en el clúster.  
  
## Solución posible  
 Use la herramienta Administrador de clústeres para realizar el flujo de trabajo de quorum forzado o de recuperación ante desastres. Si no puede resolver el problema al realizar el quorum forzado o la recuperación ante desastres, póngase en contacto con el administrador de clústeres para que le ayude a solucionar este problema. Para obtener más información, vea [Forzar el inicio de un clúster WSFC sin un cuórum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md) en los Libros en línea de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  