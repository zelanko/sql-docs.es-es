---
title: Algunas réplicas sincrónicas no están sincronizadas | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp5synchronized.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: e58ed56e-4c30-42e6-a9fc-a8c401620e02
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 0580e24a4e67e0e31a7d4f8115cd610f7a311573
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794293"
---
# <a name="some-synchronous-replicas-are-not-synchronized"></a>Algunas réplicas sincrónicas no están sincronizadas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de sincronización de los datos de réplicas sincrónicas|  
|**Problema**|Algunas réplicas sincrónicas no están sincronizadas.|  
|**Categoría**|**Advertencia**|  
|**Faceta**|grupo de disponibilidad|  
  
## <a name="description"></a>Descripción  
 Esta directiva acumula el estado de sincronización de datos de todas las réplicas de disponibilidad y comprueba que no están en el estado de sincronización esperado. La directiva está en mal estado cuando alguna réplica asincrónica no está en un estado SYNCHRONIZING y alguna réplica sincrónica no tiene un estado SYNCHRONIZED. De lo contrario, el estado de la directiva es correcto.  
  
> [!NOTE]  
>  En esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [Algunas réplicas sincrónicas no están sincronizadas](https://go.microsoft.com/fwlink/p/?LinkId=220853) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 En este grupo de disponibilidad, al menos una réplica sincrónica no está sincronizada actualmente. El estado de sincronización de la réplica puede ser SYNCHRONIZING o NOT SYNCHRONIZING.  
  
## <a name="possible-solution"></a>Solución posible  
 Use el estado de la directiva de réplica de disponibilidad para buscar la réplica de disponibilidad cuyo estado de sincronización es incorrecto, y después resuelva el problema en la réplica de disponibilidad.  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
