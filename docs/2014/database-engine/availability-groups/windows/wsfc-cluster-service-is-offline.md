---
title: El servicio de clúster WSFC está sin conexión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp1WSFCquorum.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cfab5de4cd3d171d4d8b7515e65b0a9cd117ac16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62812903"
---
# <a name="wsfc-cluster-service-is-offline"></a>El servicio de clúster de WSFC está sin conexión
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de clúster de WSFC|  
|**Problema**|El servicio de clúster de WSFC está sin conexión.|  
|**Categoría**|**Critical)** (Crítico)|  
|**Faceta**|Instancia de SQL Server|  
  
## <a name="description"></a>Descripción  
 Esta directiva comprueba el estado del clúster de conmutación por error de Windows Server (WSFC). La directiva está en mal estado y se genera una alerta cuando el clúster de WSFC está sin conexión o en el estado de quorum forzado. Todos los grupos de disponibilidad hospedados en este clúster están sin conexión o se requiere una acción de recuperación ante desastres.  
  
 El estado de la directiva es correcto cuando el estado del clúster está en el quorum normal.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [El servicio de clúster de WSFC está desconectado](https://go.microsoft.com/fwlink/p/?LinkId=220849) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Causas posibles  
 Esto puede deberse a un problema del servicio de clúster o a la pérdida del quorum en el clúster.  
  
## <a name="possible-solution"></a>Solución posible  
 Use la herramienta Administrador de clústeres para realizar el flujo de trabajo de quorum forzado o de recuperación ante desastres. Si no puede resolver el problema al realizar el quorum forzado o la recuperación ante desastres, póngase en contacto con el administrador de clústeres para que le ayude a solucionar este problema. Para obtener más información, vea [Forzar el inicio de un clúster WSFC sin un cuórum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md) en los Libros en línea de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Información general de Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
