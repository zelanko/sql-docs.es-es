---
title: Soluciones de alta disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/19/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f5c07a9689453e11058dedcdcd0d014f01b6e480
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502420"
---
# <a name="high-availability-solutions-sql-server"></a>Soluciones de alta disponibilidad (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se presentan varias soluciones de alta disponibilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que mejoran la disponibilidad de los servidores o las bases de datos. Una solución de alta disponibilidad enmascara los efectos de un error de hardware o software y mantiene la disponibilidad de las aplicaciones a fin de minimizar el tiempo de inactividad que perciben los usuarios.    
    
   
>  **Nota:** ¿Quiere saber qué ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten una determinada solución de alta disponibilidad? Vea la sección sobre alta disponibilidad AlwaysOn de [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).    
     
    
##  <a name="TermsAndDefinitions"></a> Información general de las soluciones de alta disponibilidad de SQL Server    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece varias opciones para crear alta disponibilidad para un servidor o una base de datos. Entre las opciones de alta disponibilidad figuran las siguientes:    
    
*  Instancias de clúster de conmutación por error de AlwaysOn    
 Como parte de la oferta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Always On, las instancias de clúster de conmutación por error de Always On aprovechan la funcionalidad de Clústeres de conmutación por error de Windows Server (WSFC) para proporcionar alta disponibilidad local mediante la redundancia en el nivel de instancias de servidor, una *instancia de clúster de conmutación por error* (FCI). Una FCI es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se instala a través de los nodos de Clústeres de conmutación por error de Windows Server (WSFC) y, posiblemente, a través de varias subredes. En la red, una FCI aparece como una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en un equipo individual, pero proporciona la conmutación por error entre nodos de WSFC si el nodo actual deja de estar disponible.    
    
 Para obtener más información, vea [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).    
    
*  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]    
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] es una solución de alta disponibilidad y recuperación ante desastres de nivel empresarial presentada en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] que permite maximizar la disponibilidad para una o varias bases de datos de usuario. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] necesita que las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se encuentren en nodos de Clústeres de conmutación por error de Windows Server (WSFC). Para obtener más información, vea [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).    
    
  
>  **Nota:** Una FCI puede aprovechar las ventajas de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] para proporcionar recuperación remota ante desastres en la base de datos. Para obtener más información, vea [Clúster de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).    
    
*  Creación de reflejo de base de datos. **Nota:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Se recomienda utilizar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] en su lugar.     
La creación de reflejo de la base de datos es una solución para aumentar la disponibilidad de la base de datos mediante una conmutación por error casi inmediata. La creación de reflejo de la base de datos puede utilizarse para mantener una sola base de datos en estado de espera, o *base de datos reflejada*, para una base de datos de producción correspondiente a la que se conoce como *base de datos principal*. Para obtener más información, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).    
    
*  Trasvase de registros    
 Al igual que [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] y la creación de reflejo de la base de datos, el trasvase de registros se aplica en la base de datos. Puede usar el trasvase de registros para mantener una o varias bases de datos en estado de espera activa (denominadas *bases de datos secundarias*) para una sola base de datos de producción denominada *base de datos principal*. Para obtener más información sobre el trasvase de registros, vea [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).    
    
##  <a name="RecommendedSolutions"></a> Soluciones recomendadas para utilizar SQL Server para proteger datos    
 Esta es nuestra recomendación para proporcionar protección de datos en el entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :    
    
-   Para la protección de datos en una solución de disco compartido de otro fabricante (una SAN), se recomienda usar las instancias de clúster de conmutación por error de AlwaysOn.    
    
-   Para la protección de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se recomienda utilizar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].    
    
       >  Recomendamos usar el trasvase de registros si ejecuta una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no admite [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]. Para obtener más información sobre qué ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], vea la sección sobre alta disponibilidad AlwaysOn de [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).    
    
## <a name="see-also"></a>Ver también    
 [Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)     
 [Creación de reflejo de la base de datos: interoperabilidad y coexistencia &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)     
 [Características desusadas del motor de base de datos de SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)    
    
  

