---
title: "Publicación de datos a través de Internet mediante VPN | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- VPNs [SQL Server replication]
- Web publishing [SQL Server replication], VPNs
- Internet [SQL Server replication], VPNs
ms.assetid: 9ffb6546-9973-4574-aaa0-8fe0017e3601
caps.latest.revision: "33"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a851ec36920e6300a25ebf815e8f1c6998263d5
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="publish-data-over-the-internet-using-vpn"></a>Publicar datos a través de Internet mediante VPN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La tecnología de red privada virtual (VPN) permite a los usuarios que trabajan en su casa, oficinas subsidiarias, clientes remotos y otras empresas conectarse a una red corporativa por Internet, al tiempo que se mantiene una comunicación segura. Los usuarios pueden utilizar la autenticación de Windows como si estuvieran en una red de área local (LAN). Todos los tipos de replicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden replicar datos a través de una red privada virtual (VPN), pero se puede usar la sincronización web si se está usando la replicación de mezcla, porque con la sincronización web no es necesario usar una VPN. Para más información, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Una VPN incluye el software cliente para que los equipos se conecten a través de Internet (o incluso en una Intranet, en casos especiales) al software de un equipo dedicado o servidor. Opcionalmente, se utiliza el cifrado en ambos extremos y métodos de autenticación de usuario. La conexión VPN a través de Internet funciona lógicamente como un vínculo de red de área extensa (WAN) entre los sitios.  
  
 Una VPN conecta los componentes de una red por medio de otra red. Para la conexión, el usuario utiliza Internet u otra red pública mediante un protocolo como el Protocolo de túnel punto a punto (PPTP) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] o el Protocolo de túnel de capa 2. Este proceso garantiza la misma seguridad y características que anteriormente solo estaban disponibles en una red privada. El protocolo PPTP está disponible con los sistemas operativos Microsoft Windows NT versión 4.0 y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 (y posteriores), y el protocolo L2TP, con Windows 2000 y posteriores.  
  
 El usuario no puede ver la infraestructura intermedia de enrutamiento de Internet y parece como si los datos se enviaran a través de un vínculo privado dedicado. Desde el punto de vista del usuario, una VPN es una conexión punto a punto entre el equipo del usuario y un servidor corporativo.  
  
 Después de configurar el cliente remoto para la conexión mediante VPN, y que el cliente disponga de acceso a Internet y se conecte a la LAN corporativa, podrá configurar la replicación como si el cliente remoto estuviera conectado directamente a la LAN. Por razones de seguridad, es posible disponer de recursos de red diferentes para los usuarios conectados a través de VPN y los conectados directamente a la LAN.  
  
 Para obtener más información acerca de la configuración de una VPN, vea la documentación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="see-also"></a>Ver también  
 [Replicación por Internet](../../relational-databases/replication/replication-over-the-internet.md)  
  
  
