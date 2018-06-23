---
title: Algunas réplicas sincrónicas no están sincronizadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.agdashboard.agp5synchronized.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: e58ed56e-4c30-42e6-a9fc-a8c401620e02
caps.latest.revision: 9
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 3f90c5cf3ecfbd5a55a343833fa6b88624eab69b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113204"
---
# <a name="some-synchronous-replicas-are-not-synchronized"></a>Algunas réplicas sincrónicas no están sincronizadas
    
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
>  En esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [Algunas réplicas sincrónicas no están sincronizadas](http://go.microsoft.com/fwlink/p/?LinkId=220853) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 En este grupo de disponibilidad, al menos una réplica sincrónica no está sincronizada actualmente. El estado de sincronización de la réplica puede ser SYNCHRONIZING o NOT SYNCHRONIZING.  
  
## <a name="possible-solution"></a>Solución posible  
 Use el estado de la directiva de réplica de disponibilidad para buscar la réplica de disponibilidad cuyo estado de sincronización es incorrecto, y después resuelva el problema en la réplica de disponibilidad.  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  