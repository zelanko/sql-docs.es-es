---
title: Base de datos secundaria sin combinar | Microsoft Docs
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
- sql13.swb.agdashboard.drp2joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78fd5d8d4139f8863d74bb42d29e2516fba0ba58
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="secondary-database-is-not-joined"></a>Base de datos secundaria sin combinar
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de combinación de la base de datos de disponibilidad|  
|**Problema**|Base de datos secundaria sin combinar.|  
|**Categoría**|**Advertencia**|  
|**Faceta**|Base de datos de disponibilidad|  
  
## <a name="description"></a>Description  
 Esta directiva comprueba el estado de la unión de la base de datos secundaria (también denominada “réplica de base de datos secundaria”). La directiva está en mal estado cuando la réplica de conjunto de datos no está combinada. De lo contrario, la directiva está en un estado correcto.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [La base de datos secundaria no se ha combinado](http://go.microsoft.com/fwlink/p/?LinkId=220862) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 Esta base de datos secundaria no está combinada con el grupo de disponibilidad. La configuración de esta base de datos secundaria está incompleta.  
  
## <a name="possible-solution"></a>Solución posible  
 Use Transact-SQL, PowerShell o SQL Server Management Studio para combinar la réplica secundaria con el grupo de disponibilidad. Para obtener más información sobre cómo combinar las réplicas secundarias con los grupos de disponibilidad, vea [Combinar una réplica secundaria con un grupo de disponibilidad (SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx).  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
