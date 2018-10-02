---
title: Topologías para sincronización web | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: ea1eef083342bbf3d7a4d57281171efecde030a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718673"
---
# <a name="topologies-for-web-synchronization"></a>Topologies for Web Synchronization
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede elegir entre una amplia variedad de topologías de replicación de sincronización web de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Entre las maneras habituales de configurar una sincronización web se incluyen:  
  
-   Servidor único  
  
-   Dos servidores  
  
-   Varios sistemas con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) y republicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Para más información sobre cómo configurar la sincronización web, vea [Configurar la sincronización web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="single-server"></a>Servidor único  
 En la topología más sencilla, IIS, el publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] residen en un único servidor. Los suscriptores se sincronizan conectándose a IIS en el publicador. El publicador puede estar situado detrás de un firewall.  
  
> [!NOTE]  
>  Esta configuración se recomienda solo para intranet. En el resto de las situaciones, se recomienda que el servidor IIS y el distribuidor o publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estén en equipos independientes.  
  
 ![Sincronización web con un solo servidor](../../relational-databases/replication/media/web-sync02.gif "Sincronización web con un solo servidor")  
  
## <a name="two-servers"></a>Dos servidores  
 Se puede colocar IIS en un servidor y configurar el publicador y el distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en otro distinto. El servidor en el que se ejecuta IIS puede aislarse de Internet mediante un firewall. Los suscriptores se sincronizan conectándose a IIS.  
  
 ![Sincronización web con dos servidores](../../relational-databases/replication/media/web-sync03.gif "Sincronización web con dos servidores")  
  
## <a name="multiple-iis-systems-and-sql-server-republishing"></a>Varios sistemas IIS y republicación de SQL Server  
 Si dispone de un gran número de suscriptores que se sincronizan al mismo tiempo, puede dividir el trabajo entre varios equipos que ejecuten IIS.  
  
 ![Sincronización web con varios servidores IIS](../../relational-databases/replication/media/web-sync04.gif "Sincronización web con varios servidores IIS")  
  
 Si necesita mayor equilibrio de carga en el equipo en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede crear una jerarquía de republicación en varios equipos. El publicador de más alto nivel publica datos en los suscriptores, que a su vez los vuelven a publicar, con lo que se equilibra la carga de las solicitudes de los suscriptores.  
  
> [!NOTE]  
>  Los suscriptores solo pueden sincronizarse con un publicador específico. Por ejemplo, un suscriptor a un republicador A no puede sincronizarse con el republicador B si A no está disponible.  
  
 ![Sincronización web con nueva publicación](../../relational-databases/replication/media/web-sync05.gif "Sincronización web con nueva publicación")  
  
## <a name="see-also"></a>Ver también  
 [Configurar la sincronización web](../../relational-databases/replication/configure-web-synchronization.md)   
 [Sincronización web para la replicación de mezcla](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
