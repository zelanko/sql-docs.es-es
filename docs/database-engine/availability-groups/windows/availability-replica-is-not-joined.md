---
title: La réplica de disponibilidad no está unida | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ab5079c7efcf04dd6f5461504d6bb97f9d2b548d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="availability-replica-is-not-joined"></a>La réplica de disponibilidad no está unida
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de unión de réplica de disponibilidad|  
|**Problema**|La réplica de disponibilidad no está unida.|  
|**Categoría**|**Advertencia**|  
|**Faceta**|Réplica de disponibilidad|  
  
## <a name="description"></a>Description  
 Esta directiva comprueba el estado de unión de la réplica de disponibilidad. La directiva está en mal estado cuando la réplica de disponibilidad se agrega al grupo de disponibilidad, pero no se une correctamente. De lo contrario, la directiva está en un estado correcto.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [La réplica de disponibilidad no está unida](http://go.microsoft.com/fwlink/p/?LinkId=220859) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 La réplica secundaria no se ha unido al grupo de disponibilidad. Para que una réplica de disponibilidad se una correctamente al grupo de disponibilidad, el estado de la unión debe ser Instancia independiente unida (1) o Clúster de conmutación por error unido (2).  
  
## <a name="possible-solution"></a>Solución posible  
 Use Transact-SQL, PowerShell o SQL Server Management Studio para combinar la réplica secundaria con el grupo de disponibilidad. Para obtener más información sobre cómo combinar las réplicas secundarias con los grupos de disponibilidad, vea [Combinar una réplica secundaria con un grupo de disponibilidad (SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx).  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
