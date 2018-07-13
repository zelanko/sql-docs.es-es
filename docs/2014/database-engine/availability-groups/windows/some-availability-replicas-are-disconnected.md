---
title: Algunas réplicas de disponibilidad están desconectadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e963182a4f2ec817ca17e52aa311f1fe6a70b8ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161066"
---
# <a name="some-availability-replicas-are-disconnected"></a>Algunas réplicas de disponibilidad están desconectadas
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de conexión de las réplicas de disponibilidad|  
|**Problema**|Algunas réplicas de disponibilidad están desconectadas.|  
|**Categoría**|**Advertencia**|  
|**Faceta**|grupo de disponibilidad|  
  
## <a name="description"></a>Descripción  
 Esta directiva acumula el estado de todas las réplicas de disponibilidad y comprueba las que están en estado DISCONNECTED. La directiva está en mal estado cuando cualquier réplica de disponibilidad está en estado DISCONNECTED. De lo contrario, la directiva está en un estado correcto.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [Algunas réplicas de disponibilidad están desconectadas](http://go.microsoft.com/fwlink/p/?LinkId=220855) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 En este grupo de disponibilidad, al menos una réplica secundaria no está conectada con la réplica principal. El estado de conexión es DISCONNECTED.  
  
## <a name="possible-solution"></a>Solución posible  
 Use el estado de directiva de la réplica de disponibilidad para buscar la réplica de disponibilidad que está en estado DISCONNECTED y, a continuación, resuelva el problema en la réplica de disponibilidad.  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
