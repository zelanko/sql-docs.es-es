---
title: Algunas réplicas sincrónicas no están sincronizadas
description: Describe algunas causas posibles y soluciones para los casos en los que una réplica sincrónica no está sincronizada para un grupo de disponibilidad Always On.
ms.custom: seo-lt-2019
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
author: cawrites
ms.author: chadam
ms.openlocfilehash: a8e5fc7b3aa708acc3542082ece0d980c938eb34
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583868"
---
# <a name="some-synchronous-replicas-are-not-synchronized"></a>Algunas réplicas sincrónicas no están sincronizadas
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de sincronización de los datos de réplicas sincrónicas|  
|**Problema**|Algunas réplicas sincrónicas no están sincronizadas.|  
|**Categoría**|**Warning (ADVERTENCIA)**|  
|**Faceta**|grupo de disponibilidad|  
  
## <a name="description"></a>Descripción  
 Esta directiva acumula el estado de sincronización de datos de todas las réplicas de disponibilidad y comprueba que no están en el estado de sincronización esperado. La directiva está en mal estado cuando alguna réplica asincrónica no está en un estado SYNCHRONIZING y alguna réplica sincrónica no tiene un estado SYNCHRONIZED. De lo contrario, el estado de la directiva es correcto.  
  
> [!NOTE]  
>  En esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [Algunas réplicas sincrónicas no están sincronizadas](https://go.microsoft.com/fwlink/p/?LinkId=220853) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Causas posibles  
 En este grupo de disponibilidad, al menos una réplica sincrónica no está sincronizada actualmente. El estado de sincronización de la réplica puede ser SYNCHRONIZING o NOT SYNCHRONIZING.  
  
## <a name="possible-solution"></a>Solución posible  
 Use el estado de la directiva de réplica de disponibilidad para buscar la réplica de disponibilidad cuyo estado de sincronización es incorrecto, y después resuelva el problema en la réplica de disponibilidad.  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
