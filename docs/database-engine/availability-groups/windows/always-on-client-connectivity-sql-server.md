---
title: Compatibilidad con la conectividad de cliente y controlador para grupos de disponibilidad
description: 'En este tema se describen las consideraciones para la conectividad de cliente a grupos de Always On, incluidos los requisitos previos, las restricciones y las recomendaciones para las configuraciones y los valores de cliente. '
ms.custom: seodec18
ms.date: 04/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], client connectivity
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 298e0639aad54384b3586e27fcbd5d6223e646de
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578435"
---
# <a name="always-on-client-connectivity-sql-server"></a>Conectividad de cliente de AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describen las consideraciones para la conectividad de cliente a grupos de Always On, incluidos los requisitos previos, las restricciones y las recomendaciones para las configuraciones y los valores de cliente.  
  
 
##  <a name="ClientConnSupport"></a> Compatibilidad con conectividad de cliente  
 En la próxima sección se ofrece información acerca de la compatibilidad de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] con conectividad de cliente.  
  
 **Compatibilidad de controlador**  
  
 En la tabla siguiente se resume la compatibilidad de los controladores con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
|Controlador|Conmutación por error de múltiples subredes|Intención de aplicaciones|Enrutamiento de solo lectura|Conmutación por error de varias subredes: Conmutación por error más rápida del extremo de una sola subred|Conmutación por error de varias subredes: Resolución de instancias con nombre para las instancias en clúster SQL |  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|Sí|Sí|Sí|Sí|Sí|  
|SQL Native Client 11.0 OLEDB|No|Sí|Sí|No|No|  
|ADO.NET con .NET Framework 4.0 con revisión de conectividad*|Sí|Sí|Sí|Sí|Sí|  
|ADO.NET con .NET Framework 3.5 SP1 con revisión de conectividad **|Sí|Sí|Sí|Sí|Sí|  
|Controlador JDBC 4.0 de Microsoft para SQL Server|Sí|Sí|Sí|Sí|Sí| 
|Controlador Microsoft OLE DB para SQL Server|Sí|Sí|Sí|Sí|Sí| 
  
 *Descargar la revisión de conectividad para ADO .NET con .NET Framework 4.0: [https://support.microsoft.com/kb/2600211](https://support.microsoft.com/kb/2600211).  
  
 **Descargar la revisión de conectividad para ADO.NET con .NET Framework 3.5 SP1: [https://support.microsoft.com/kb/2654347](https://support.microsoft.com/kb/2654347).  
 
 *Descargar el nuevo controlador de Microsoft OLE DB para SQL Server: [https://www.microsoft.com/download/details.aspx?id=56730](https://www.microsoft.com/download/details.aspx?id=56730).  

> [!IMPORTANT]  
>  Para conectarse a un agente de escucha del grupo de disponibilidad, los clientes deben usar una cadena de conexión de TCP.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Clústeres de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Acerca del acceso de conexión de cliente a réplicas de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Guía de soluciones AlwaysOn de Microsoft SQL Server para lograr alta disponibilidad y recuperación ante desastres](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [Blog del equipo Always On de SQL Server: el blog oficial del equipo de Always On de SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)   
 [Se produce un retraso prolongado cuando se vuelve a conectar una conexión de IPSec desde un equipo que ejecuta Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 o Windows Server 2008 R2](https://support.microsoft.com/kb/980915)   
 [El servicio de clúster tarda en torno a 30 segundos en la conmutación por error de las direcciones IP IPv6 en Windows Server 2008 R2](https://support.microsoft.com/kb/2578113)   
 [Reducir la operación de conmutación por error si no existe un enrutador entre el clúster y un servidor de aplicaciones](https://support.microsoft.com/kb/2582281)  
  
  
