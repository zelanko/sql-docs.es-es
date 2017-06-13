---
title: Alta disponibilidad (Reporting Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], Reporting Services
- high availability [Reporting Services]
- Reporting Services, high availability
ms.assetid: 50e0813f-f591-4688-9cd1-e6389a3808e5
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b4b2d373dfc2467e10a9a6ee79d98aa3a690bd4c
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="high-availability-reporting-services"></a>Alta disponibilidad (Reporting Services)
  Un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es un servidor sin estado que almacena dato de la aplicación, contenido, propiedades e información de la sesión en dos bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relacionales. Como tal, la mejor manera de asegurarse la disponibilidad de la funcionalidad de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es hacer el siguiente:  
  
-   Use las características de alta disponibilidad del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] para maximizar el tiempo de funcionamiento de las bases de datos del servidor de informes. Si configura una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que se ejecute en un clúster de conmutación por error, puede seleccionar dicha instancia al crear una base de datos del servidor de informes.  
  
-   Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] con los orígenes de datos y las bases de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , según sea posible. Para más información, consulte [Reporting Services con Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md).  
  
-   Configure varios servidores de informes para que se ejecuten en una implementación escalada, en la que todos los servidores comparten una única base de datos de servidor de informes. La implementación de varias instancias del servidor de informes, preferentemente en servidores diferentes, en una implementación escalada puede ayudar a proporcionar un servicio ininterrumpido en el caso de que se bloquee una de las instancias del servidor de informes.  
  
 Una implementación escalada proporciona una manera de compartir una base de datos. Si un servidor de informes se bloquea, otros servidores de la misma implementación continuarán funcionando.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no detecta los clústeres. Por sí sola, una implementación escalada no proporciona equilibrio de carga; no detecta las cargas de procesamiento en un servidor de informes y enruta las nuevas solicitudes de procesamiento al servidor menos ocupado. No vuelve a enrutar las solicitudes de procesamiento que no fueron correctas antes de la finalización. Para obtener características de equilibrio de carga, debe configurar el equilibrio de carga para los servidores web que hospedan los servidores de informes y, a continuación, obtener los servidores de informes en una implementación escalada de manera que compartan la misma base de datos del servidor de informes.  
  
 El servicio de Windows y el servicio web del servidor de informes están estrechamente integrados y se ejecutan en conjunto como una instancia del servidor de informes única. No puede configurar la disponibilidad para un servicio de manera independiente del otro.  
  
## <a name="see-also"></a>Vea también  
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](http://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c)  
  
  
