---
title: Topologías para sincronización web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web synchronization, topologies
- IIS server configuration [SQL Server replication]
ms.assetid: 59444faf-bcb6-4421-a3df-8715753e453b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62fd4cd78beaeff479fc7cc9ec3abbd79e227e04
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63273557"
---
# <a name="topologies-for-web-synchronization"></a>Topologies for Web Synchronization
  Puede elegir entre una variedad de topologías de replicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sincronización Web. Entre las maneras habituales de configurar una sincronización web se incluyen:  
  
-   Servidor único  
  
-   Dos servidores  
  
-   Varios sistemas con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) y republicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Para más información sobre cómo configurar la sincronización web, vea [Configurar la sincronización web](configure-web-synchronization.md).  
  
## <a name="single-server"></a>Servidor único  
 En la topología más sencilla, IIS, el publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] residen en un único servidor. Los suscriptores se sincronizan conectándose a IIS en el publicador. El publicador puede estar situado detrás de un firewall.  
  
> [!NOTE]  
>  Esta configuración se recomienda solo para intranet. En el resto de las situaciones, se recomienda que el servidor IIS y el distribuidor o publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estén en equipos independientes.  
  
 ![Sincronización web con un solo servidor](media/web-sync02.gif "Sincronización web con un solo servidor")  
  
## <a name="two-servers"></a>Dos servidores  
 Se puede colocar IIS en un servidor y configurar el publicador y el distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en otro distinto. El servidor en el que se ejecuta IIS puede aislarse de Internet mediante un firewall. Los suscriptores se sincronizan conectándose a IIS.  
  
 ![Sincronización web con dos servidores](media/web-sync03.gif "Sincronización web con dos servidores")  
  
## <a name="multiple-iis-systems-and-sql-server-republishing"></a>Varios sistemas IIS y republicación de SQL Server  
 Si dispone de un gran número de suscriptores que se sincronizan al mismo tiempo, puede dividir el trabajo entre varios equipos que ejecuten IIS.  
  
 ![Sincronización web con varios servidores IIS](media/web-sync04.gif "Sincronización web con varios servidores IIS")  
  
 Si necesita mayor equilibrio de carga en el equipo en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede crear una jerarquía de republicación en varios equipos. El publicador de más alto nivel publica datos en los suscriptores, que a su vez los vuelven a publicar, con lo que se equilibra la carga de las solicitudes de los suscriptores.  
  
> [!NOTE]  
>  Los suscriptores solo pueden sincronizarse con un publicador específico. Por ejemplo, un suscriptor a un republicador A no puede sincronizarse con el republicador B si A no está disponible.  
  
 ![Sincronización web con nueva publicación](media/web-sync05.gif "Sincronización web con nueva publicación")  
  
## <a name="see-also"></a>Consulte también  
 [Configurar la sincronización Web](configure-web-synchronization.md)   
 [Sincronización web para la replicación de mezcla](web-synchronization-for-merge-replication.md)  
  
  
