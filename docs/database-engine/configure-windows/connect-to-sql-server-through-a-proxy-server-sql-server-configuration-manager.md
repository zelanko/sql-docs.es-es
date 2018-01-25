---
title: "Conectarse a SQL Server a través de un servidor proxy (Administrador de configuración de SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 12/15/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6781cce5ed2b04d72a8eeec9bcba9a5688e3e53
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>Conectarse a SQL Server a través de un servidor proxy (Administrador de configuración de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo conectarse a SQL Server mediante un servidor proxy en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando el Administrador de configuración de SQL Server. Para escuchar de forma remota mediante WinSock remoto (RWS), defina la tabla de direcciones locales (LAT) del servidor proxy de modo que la dirección del nodo en espera de conexiones quede fuera de la lista de entradas LAT.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>Para permitir conexiones a SQL Server a través de Microsoft Proxy Server   
  
1.  Siga los pasos de [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md) para determinar qué puertos TCP/IP usa [!INCLUDE[ssDE](../../includes/ssde-md.md)], o para configurar [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar un puerto deseado.  
  
2.  Defina en su servidor proxy la tabla de direcciones locales (LAT) del servidor proxy de manera que la dirección del nodo en espera de conexiones se encuentre fuera del rango de entradas LAT. Para obtener más información, vea la documentación de su servidor proxy.  
  
>  [!NOTE]
>  Este tema se aplica a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]local. En caso de problemas de conexión relacionados con [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], consulte [Solución de problemas de conexión de Base de datos SQL de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-common-connection-issues).  


