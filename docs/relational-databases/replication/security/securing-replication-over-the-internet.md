---
title: "Proteger la replicación por Internet | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 429f7ada41541596948ce3546b37c1d50cecdb1f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="securing-replication-over-the-internet"></a>Proteger la replicación por Internet
  La replicación por Internet puede proporcionar flexibilidad, en especial a los suscriptores móviles, pero debe configurarla de forma correcta para garantizar la seguridad adecuada. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomienda utilizar una de estas dos técnicas para compartir información de forma segura en Internet:  
  
-   Red privada virtual (VPN)  
  
-   La opción Sincronización web para la replicación de mezcla.  
  
## <a name="virtual-private-network"></a>Red privada virtual  
 Las redes privadas virtuales proporcionan un método por capas seguro y sencillo para replicar datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por Internet. La conexión VPN a través de Internet funciona lógicamente como un vínculo de red de área extensa (WAN) entre los sitios.  
  
 Esto se consigue permitiendo que el usuario utilice Internet u otra red pública por medio de un protocolo como el Protocolo de túnel punto a punto (PPTP) de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] , incluido en el sistema operativo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT versión 4.0 o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000, o el Protocolo de túnel de capa dos (L2TP), incluido en Windows 2000. Este proceso proporciona seguridad y características parecidas a las disponibles en una red privada.  
  
 Para obtener más información acerca de la configuración de una VPN, vea la documentación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows.  
  
## <a name="web-synchronization-through-iis"></a>Sincronización web mediante IIS  
 La opción de sincronización web en la replicación de mezcla proporciona la capacidad de replicar datos utilizando el protocolo HTTPS, que puede ser un método cómodo para replicar datos a través de un firewall. Para más información sobre la seguridad en la sincronización web, vea [Configure Web Synchronization](../../../relational-databases/replication/configure-web-synchronization.md) (Configurar la sincronización web) y [Security Architecture for Web Synchronization](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md) (Arquitectura de seguridad para la sincronización web).  
  
## <a name="see-also"></a>Vea también  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Seguridad y protección &#40;replicación&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
