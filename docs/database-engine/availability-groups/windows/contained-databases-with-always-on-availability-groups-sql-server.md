---
title: Bases de datos independientes con grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- contained database, AlwaysOnAvailabilityGroups
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8226893f960bd0c1b64c589219121f323226766d
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34768651"
---
# <a name="contained-databases-with-always-on-availability-groups-sql-server"></a>Bases de datos independientes con grupos de disponibilidad AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tema contiene información sobre cómo utilizar una base de datos independiente con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 **En este tema:**  
  
-   [Requisitos previos](#Prerequisites)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   Antes de agregar una base de datos independiente a un grupo de disponibilidad, asegúrese de que la opción de servidor **contained database authentication** está establecida en **1** en cada instancia de servidor que hospeda una réplica de disponibilidad para el grupo de disponibilidad. Para obtener más información, vea [contained database authentication (opción de configuración del servidor)](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md) y [Opciones de configuración de servidor &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Opciones de configuración de servidor &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Bases de datos independientes](../../../relational-databases/databases/contained-databases.md)  
  
  
