---
title: Conectividad de cliente de AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 1368d29801a414de866003b86c63fb4823c4a7b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62790664"
---
# <a name="always-on-client-connectivity-sql-server"></a>Conectividad de cliente de AlwaysOn (SQL Server)
  En este tema se describen las consideraciones para la conectividad de cliente a grupos de AlwaysOn, incluidos los requisitos previos, las restricciones y las recomendaciones para las configuraciones y los valores de cliente.  
  
 
  
##  <a name="ClientConnSupport"></a> Compatibilidad con conectividad de cliente  
 En la próxima sección se ofrece información acerca de la compatibilidad de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] con conectividad de cliente.  
  
 **Compatibilidad de controlador**  
  
 En la tabla siguiente se resume la compatibilidad de los controladores con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
|Controlador|Conmutación por error de múltiples subredes|Intención de aplicaciones|Enrutamiento de solo lectura|Conmutación por error de múltiples subredes: Más rápida una sola conmutación por error de punto de conexión de subred|Conmutación por error de múltiples subredes: Las instancias en clúster de resolución de instancias con nombre para SQL|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|Sí|Sí|Sí|Sí|Sí|  
|SQL Native Client 11.0 OLEDB|Sin|Sí|Sí|No|Sin|  
|ADO.NET con .NET Framework 4.0 con revisión de conectividad **<sup>*</sup>**|Sí|Sí|Sí|Sí|Sí|  
|ADO.NET con .NET Framework 3.5 SP1 con revisión de conectividad **<sup>** </sup>**|Sí|Sí|Sí|Sí|Sí|  
|Controlador JDBC 4.0 de Microsoft para SQL Server|Sí|Sí|Sí|Sí|Sí|  
  
 **<sup>*</sup>**  Descargar la revisión de conectividad para ADO .NET con .NET Framework 4.0: [ https://support.microsoft.com/kb/2600211 ](https://support.microsoft.com/kb/2600211).  
  
 **<sup>** </sup>** Descargar la revisión de conectividad para ADO.NET con .NET Framework 3.5 SP1: [ https://support.microsoft.com/kb/2654347 ](https://support.microsoft.com/kb/2654347).  
  
> [!IMPORTANT]  
>  Para conectarse a un agente de escucha del grupo de disponibilidad, los clientes deben usar una cadena de conexión de TCP.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  

  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Agrupación en clústeres de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Acerca del acceso de conexión de cliente a réplicas de disponibilidad &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Guía de soluciones de Microsoft SQL Server AlwaysOn para alta disponibilidad y recuperación ante desastres](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [Blog del equipo de AlwaysOn SQL Server: El blog del equipo de AlwaysOn oficial SQL Server](https://blogs.msdn.com/b/sqlalwayson/)   
 [Se produce un retraso prolongado cuando se vuelve a conectar una conexión de IPSec desde un equipo que ejecuta Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 o Windows Server 2008 R2](https://support.microsoft.com/kb/980915)   
 [El servicio de clúster tarda en torno a 30 segundos en la conmutación por error de las direcciones IP IPv6 en Windows Server 2008 R2](https://support.microsoft.com/kb/2578113)   
 [Reducir la operación de conmutación por error si no existe un enrutador entre el clúster y un servidor de aplicaciones](https://support.microsoft.com/kb/2582281)  
  
  
