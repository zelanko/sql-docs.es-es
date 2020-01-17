---
title: Réplicas de disponibilidad que no sincronizan datos
description: Posibles causas y soluciones para cuando una o varias réplicas de disponibilidad de un grupo de disponibilidad AlwaysOn no están sincronizando datos con la réplica principal.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 66ebb11535fe2eecc6495b8c5e194d286ecc88ed
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822584"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>Algunas réplicas de disponibilidad no sincronizan datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de sincronización de datos de las réplicas de disponibilidad|  
|**Problema**|Algunas réplicas de disponibilidad no sincronizan datos.|  
|**Categoría**|**Warning (ADVERTENCIA)**|  
|**Faceta**|grupo de disponibilidad|  
  
## <a name="description"></a>Descripción  
 Esta directiva acumula el estado de sincronización de datos de todas las réplicas de disponibilidad en el grupo de disponibilidad y comprueba si la sincronización de alguna réplica de disponibilidad no está operativa. La directiva está en mal estado si alguno de los estados de sincronización de datos de la réplica de disponibilidad es NOT SYNCHRONIZING.  
  
 Esta directiva está en un estado correcto si ninguno de los estados de sincronización de datos de la réplica de disponibilidad es NOT SYNCHRONIZING.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [Algunas réplicas de disponibilidad no sincronizan datos](https://go.microsoft.com/fwlink/p/?LinkId=220852) de la wiki de TechNet.  
  
## <a name="possible-causes"></a>Causas posibles  
 En este grupo de disponibilidad, al menos una réplica secundaria tiene un estado de sincronización NOT SYNCHRONIZING y no recibe datos de la réplica principal.  
  
## <a name="possible-solution"></a>Solución posible  
 Use el estado de directiva de la réplica de disponibilidad para buscar la réplica de disponibilidad con un estado NOT SYNCHRONIZING y, a continuación, resuelva el problema en la réplica de disponibilidad.  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
