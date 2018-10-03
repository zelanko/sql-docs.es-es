---
title: Bases de datos independientes con grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- contained database [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 13dd6e87b6442b8c1b908ceb73d1e5c7f135308c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48107555"
---
# <a name="contained-databases-with-always-on-availability-groups-sql-server"></a>Bases de datos independientes con grupos de disponibilidad AlwaysOn (SQL Server)
  Este tema contiene información sobre cómo utilizar una base de datos independiente con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 **En este tema:**  
  
-   [Requisitos previos](#Prerequisites)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   Antes de agregar una base de datos independiente a un grupo de disponibilidad, asegúrese de que la opción de servidor `contained database authentication` está establecida en `1` en cada instancia de servidor que hospeda una réplica de disponibilidad para el grupo de disponibilidad. Para obtener más información, vea [contained database authentication (opción de configuración del servidor)](../../configure-windows/contained-database-authentication-server-configuration-option.md) y [Opciones de configuración de servidor &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Opciones de configuración de servidor &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Bases de datos independientes](../../../relational-databases/databases/contained-databases.md)  
  
  
