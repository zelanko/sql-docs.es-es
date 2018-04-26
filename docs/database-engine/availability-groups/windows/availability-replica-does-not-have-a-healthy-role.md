---
title: La réplica de disponibilidad no tiene un rol en buen estado | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.arp1rolehealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: afc3139b04304a44c787e69f25365158fc5b09b1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="availability-replica-does-not-have-a-healthy-role"></a>La réplica de disponibilidad no tiene un rol en buen estado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado del rol de réplica de disponibilidad|  
|**Problema**|La réplica de disponibilidad no tiene un rol en buen estado.|  
|**Categoría**|**Crítico**|  
|**Faceta**|Réplica de disponibilidad|  
  
## <a name="description"></a>Description  
 Esta directiva comprueba el estado del rol de la réplica de disponibilidad. La directiva está en mal estado cuando el rol de la réplica de disponibilidad no es principal ni secundario. De lo contrario, la directiva está en un estado correcto.  
  
> [!NOTE]  
>  En esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [La réplica de disponibilidad no tiene un rol en buen estado](http://go.microsoft.com/fwlink/p/?LinkId=220856) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 El rol de esta réplica de disponibilidad está en mal estado. La réplica no tiene el rol principal o secundario.  
  
## <a name="possible-solution-informationstilltocome"></a>Solución posible: Information_still_to_come  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
