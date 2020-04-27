---
title: Proteger la replicación por Internet | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78dfc544d7fd01f6641df6c0968d4a59a668cdd3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62960039"
---
# <a name="securing-replication-over-the-internet"></a>Securing Replication Over the Internet
  La replicación por Internet puede proporcionar flexibilidad, en especial a los suscriptores móviles, pero debe configurarla de forma correcta para garantizar la seguridad adecuada. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomienda utilizar una de estas dos técnicas para compartir información de forma segura en Internet:  
  
-   Red privada virtual (VPN)  
  
-   La opción Sincronización web para la replicación de mezcla.  
  
## <a name="virtual-private-network"></a>Red privada virtual  
 Las redes privadas virtuales proporcionan un método por capas seguro y sencillo para replicar datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por Internet. La conexión VPN a través de Internet funciona lógicamente como un vínculo de red de área extensa (WAN) entre los sitios.  
  
 Esto se consigue permitiendo que el usuario utilice Internet u otra red pública por medio de un protocolo como el Protocolo de túnel punto a punto (PPTP) de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] , incluido en el sistema operativo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT versión 4.0 o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000, o el Protocolo de túnel de capa dos (L2TP), incluido en Windows 2000. Este proceso proporciona seguridad y características parecidas a las disponibles en una red privada.  
  
 Para obtener más información acerca de la configuración de una VPN, vea la documentación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows.  
  
## <a name="web-synchronization-through-iis"></a>Sincronización web mediante IIS  
 La opción de sincronización web en la replicación de mezcla proporciona la capacidad de replicar datos utilizando el protocolo HTTPS, que puede ser un método cómodo para replicar datos a través de un firewall. Para más información sobre la seguridad en la sincronización web, vea [Configure Web Synchronization](../configure-web-synchronization.md) (Configurar la sincronización web) y [Security Architecture for Web Synchronization](security-architecture-for-web-synchronization.md) (Arquitectura de seguridad para la sincronización web).  
  
## <a name="see-also"></a>Consulte también  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Seguridad de Replicación de SQL Server](view-and-modify-replication-security-settings.md)  
  
  
