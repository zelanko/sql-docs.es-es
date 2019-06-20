---
title: Iniciar SQL Server con la configuración mínima | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cf7065d064e322e45fb95a38aed514b2acfc714a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62756222"
---
# <a name="start-sql-server-with-minimal-configuration"></a>Iniciar SQL Server con la configuración mínima
  Si tiene problemas de configuración que impiden el inicio del servidor, puede iniciar una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la opción de inicio con configuración mínima. Esta es la opción de inicio **-f**. Al iniciar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configuración mínima, el servidor utilizará automáticamente el modo de usuario único.  
  
 Tenga en cuenta los siguientes aspectos cuando inicie una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de configuración mínima:  
  
-   Solo se podrá conectar un usuario y no se ejecutará el proceso CHECKPOINT.  
  
-   El acceso remoto y la lectura anticipada quedan deshabilitadas.  
  
-   No se ejecutan los procedimientos almacenados de inicio.  
  
 Después de iniciar el servidor con la configuración mínima, debe modificar los valores que haga falta del servidor, detenerlo y después reiniciarlo.  
  
> [!IMPORTANT]  
>  Use la utilidad **sqlcmd** y la conexión de administrador dedicada (DAC) para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si utiliza una conexión típica, detenga el servicio del Agente SQL Server antes de conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de configuración mínima. En caso contrario, el servicio Agente SQL Server utilizará la conexión y, por tanto, la bloqueará.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar, detener o pausar el servicio del Agente SQL Server](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)   
 [Conexión de diagnóstico para administradores de bases de datos](diagnostic-connection-for-database-administrators.md)   
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Opciones de inicio del servicio de motor de base de datos](database-engine-service-startup-options.md)  
  
  
