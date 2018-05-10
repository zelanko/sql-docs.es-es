---
title: Base de datos de disponibilidad suspendida | Microsoft Docs
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
- sql13.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 91529250606470a39c70ee5274a72001658345b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="availability-database-is-suspended"></a>Base de datos de disponibilidad suspendida
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de suspensión de la base de datos de disponibilidad|  
|**Problema**|Base de datos de disponibilidad suspendida.|  
|**Categoría**|**Advertencia**|  
|**Faceta**|Base de datos de disponibilidad|  
  
## <a name="description"></a>Description  
 Esta directiva comprueba el estado del movimiento de datos de la base de datos secundaria (también denominada “réplica de base de datos secundaria”). La directiva está en mal estado cuando se suspende el movimiento de datos. De lo contrario, la directiva está en un estado correcto.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [Base de datos de disponibilidad suspendida](http://go.microsoft.com/fwlink/p/?LinkId=220860) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 La sincronización de datos de esta base de datos de disponibilidad podría haberse suspendido debido al siguiente:  
  
-   Debido a un error, el sistema puede haber suspendido la sincronización de datos.  
  
-   El administrador de la base de datos puede haber suspendido la sincronización de datos con fines de mantenimiento.  
  
## <a name="possible-solution"></a>Solución posible  
 Reanude la sincronización de datos. Si el problema persiste, compruebe el grupo de disponibilidad en el registro de eventos y, a continuación, diagnostique por qué el sistema suspendió el movimiento de datos.  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
