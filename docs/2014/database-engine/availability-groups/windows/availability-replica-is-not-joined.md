---
title: La réplica de disponibilidad no está unida | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 50a2dcbb776b9f8bc3a736e8e6f06f572f76b449
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194965"
---
# <a name="availability-replica-is-not-joined"></a>La réplica de disponibilidad no está unida
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de unión de réplica de disponibilidad|  
|**Problema**|La réplica de disponibilidad no está unida.|  
|**Categoría**|**Advertencia**|  
|**Faceta**|Réplica de disponibilidad|  
  
## <a name="description"></a>Descripción  
 Esta directiva comprueba el estado de unión de la réplica de disponibilidad. La directiva está en mal estado cuando la réplica de disponibilidad se agrega al grupo de disponibilidad, pero no se une correctamente. De lo contrario, la directiva está en un estado correcto.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [La réplica de disponibilidad no está unida](http://go.microsoft.com/fwlink/p/?LinkId=220859) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 La réplica secundaria no se ha unido al grupo de disponibilidad. Para que una réplica de disponibilidad se una correctamente al grupo de disponibilidad, el estado de la unión debe ser Instancia independiente unida (1) o Clúster de conmutación por error unido (2).  
  
## <a name="possible-solution"></a>Solución posible  
 Use Transact-SQL, PowerShell o SQL Server Management Studio para combinar la réplica secundaria con el grupo de disponibilidad. Para obtener más información sobre cómo combinar las réplicas secundarias con los grupos de disponibilidad, vea [Combinar una réplica secundaria con un grupo de disponibilidad (SQL Server)](http://msdn.microsoft.com/en-sg/library/ff878473\(en-us,SQL.110\).aspx).  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
