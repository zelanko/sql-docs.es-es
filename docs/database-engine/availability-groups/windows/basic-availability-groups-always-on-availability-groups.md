---
title: "Grupos de disponibilidad básica (grupos de disponibilidad AlwaysOn) | Microsoft Docs"
ms.custom: 
ms.date: 09/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 285adbc7-ac9b-40f6-b4a9-3f1591d3b632
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 15696e7bf14fb5a240f1ef14070f28bb5d87a1f2
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="basic-availability-groups-always-on-availability-groups"></a>Grupos de disponibilidad básica (grupos de disponibilidad AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Los grupos de disponibilidad básica Always On ofrecen una solución de alta disponibilidad para SQL Server 2016 y SQL Server 2017 Standard Edition. Un grupo de disponibilidad básica admite un entorno de conmutación por error para una base de datos única. Se crea y administra prácticamente igual que [Grupos de disponibilidad Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) tradicional (avanzado) con Enterprise Edition. En este documento se resumen las diferencias y limitaciones de los grupos de disponibilidad básica.  
  
## <a name="features"></a>Características  
 Grupos de disponibilidad básica AlwaysOn reemplaza la característica en desuso de creación de reflejo de la base de datos y proporciona un nivel similar de compatibilidad de características. Los grupos de disponibilidad básica permiten que una base de datos principal mantenga una réplica única. Esta réplica puede usar el modo de confirmación sincrónica o el modo de confirmación asincrónica. Para obtener más información sobre los modos de disponibilidad, vea [Modos de disponibilidad &#40;Grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md). La réplica secundaria permanece inactiva a menos que exista una necesidad de conmutación por error. Esta conmutación por error invierte las asignaciones principales y secundarias de roles, lo que provoca que la réplica secundaria se convierta en la principal base de datos activa. Para obtener más información sobre la conmutación por error, vea [Conmutación por error y modos de conmutación por error &#40;Grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md). Los grupos de disponibilidad básica pueden funcionar en un entorno híbrido que abarca el local y Microsoft Azure.  
  
## <a name="limitations"></a>Limitaciones  
 Los grupos de disponibilidad básica usan un subconjunto de características en comparación con los grupos de disponibilidad avanzada en SQL Server 2016 Enterprise Edition. Los grupos de disponibilidad básica incluyen las siguientes limitaciones:  
  
- Límite de dos réplicas (principal y secundaria).  
  
- Sin acceso de lectura en la réplica secundaria.  
  
- Sin copias de seguridad en la réplica secundaria.  

- Sin comprobaciones de integridad en las réplicas secundarias. 

- No se admiten réplicas hospedadas en servidores que ejecutan una versión de SQL Server anterior a SQL Server 2016 Community Technology Preview 3 (CTP3).  
  
- No se admite la opción de agregar o quitar una réplica de un grupo de disponibilidad básica existente.  
  
- Admite una base de datos de disponibilidad.  
  
- Los grupos de disponibilidad básica no pueden actualizarse a los grupos de disponibilidad avanzada. El grupo debe quitarse y agregarse de nuevo a un grupo que contenga servidores que solo ejecuten SQL Server 2016 Enterprise Edition.  
  
- Los grupos de disponibilidad básica solo son compatibles con los servidores Standard Edition. 

- Los grupos de disponibilidad básica no pueden formar parte de un grupo de disponibilidad distribuido. 
  
## <a name="configuration"></a>Configuración  
 Un grupo de disponibilidad básica AlwaysOn se puede crear en dos servidores SQL Server 2016 Standard Edition. Cuando crea un grupo de disponibilidad básica, debe especificar ambas réplicas durante la creación.  
  
 Para crear un grupo de disponibilidad básica, use el comando Transact-SQL **CREATE AVAILABILITY GROUP** y especifique la opción **WITH BASIC** (el valor predeterminado es **ADVANCED**). Para obtener más información, vea [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md). En este momento, no existe ninguna compatibilidad de interfaz de usuario para crear grupos de disponibilidad básica en SQL Server Management Studio.  
  
> [!NOTE]  
>  Las limitaciones de los grupos de disponibilidad básica se aplican al comando **CREATE AVAILABILITY GROUP** cuando **WITH BASIC** está especificado. Por ejemplo, obtendrá un error si intenta crear un grupo de disponibilidad básica que permita el acceso de lectura. Otras limitaciones se aplican de la misma manera. Consulte la sección Limitaciones de este tema para obtener más información.  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
