---
title: El estado de sincronización de datos de bases de datos de disponibilidad no es correcto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ed541e86bf531dd9681e9926e4acb6d1bdc6042
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936876"
---
# <a name="data-synchronization-state-of-availability-database-is-not-healthy"></a>El estado de sincronización de datos de bases de datos de disponibilidad no está en buen estado
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de sincronización de datos de la base de datos de disponibilidad|  
|**Problema**|El estado de sincronización de datos de las bases de datos de disponibilidad no es correcto|  
|**Categoría**|**Warning (ADVERTENCIA)**|  
|**Agrupa**|Base de datos de disponibilidad|  
  
## <a name="description"></a>Descripción  
 Esta directiva acumula el estado de sincronización de datos de todas las bases de datos de disponibilidad (también conocidas como "réplicas de base de datos") en la réplica de disponibilidad. La directiva está en mal estado cuando alguna réplica de la base de datos no está en el estado esperado de sincronización de datos. De lo contrario, la directiva está en un estado correcto.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [El estado de sincronización de datos de alguna base de datos de disponibilidad no está en buen estado](https://go.microsoft.com/fwlink/p/?LinkId=220858) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Causas posibles  
 El estado de sincronización de datos de esta base de datos de disponibilidad no es correcto. En una réplica de disponibilidad de confirmación asincrónica, cada base de datos de disponibilidad debe estar en el estado SYNCHRONIZING. En una réplica de confirmación sincrónica, cada base de datos de disponibilidad debe estar en el estado SYNCHRONIZED.  
  
## <a name="possible-solution"></a>Solución posible  
 Use la directiva de réplica de base de datos para buscar la réplica de base de datos que está en un estado incorrecto de sincronización de datos y, a continuación, resuelva el problema en la réplica de base de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Información general de Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
