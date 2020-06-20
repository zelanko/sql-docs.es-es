---
title: Conectarse a SQL Server a través de un servidor proxy (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: de22ad6043c509f08471a6bea40c0efa18d76842
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935476"
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>Conectarse a SQL Server a través de un servidor proxy (Administrador de configuración de SQL Server)
  En este tema se describe cómo conectarse a SQL Server mediante un servidor proxy en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando el Administrador de configuración de SQL Server. Para escuchar de forma remota mediante WinSock remoto (RWS), defina la tabla de direcciones locales (LAT) del servidor proxy de modo que la dirección del nodo en espera de conexiones quede fuera de la lista de entradas LAT.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>Para permitir conexiones a SQL Server a través de Microsoft Proxy Server  
  
1.  Siga los pasos de [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](configure-a-server-to-listen-on-a-specific-tcp-port.md) para determinar qué puertos TCP/IP usa [!INCLUDE[ssDE](../../includes/ssde-md.md)], o para configurar [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar un puerto deseado.  
  
2.  Defina en su servidor proxy la tabla de direcciones locales (LAT) del servidor proxy de manera que la dirección del nodo en espera de conexiones se encuentre fuera del rango de entradas LAT. Para obtener más información, vea la documentación de su servidor proxy.  
  
  
