---
title: Iniciar SQL Server con la configuración mínima | Microsoft Docs
description: Familiarícese con la opción de inicio con la configuración mínima en SQL Server. Vea cuándo y cómo usarlo y obtenga información sobre cómo limita la funcionalidad.
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e6e301cd7dc29cc5e2a2cffc34066369ed67d57a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85763999"
---
# <a name="start-sql-server-with-minimal-configuration"></a>Iniciar SQL Server con la configuración mínima
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Si tiene problemas de configuración que evitan el inicio del servidor, puede iniciar una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la opción de inicio con configuración mínima. Esta es la opción de inicio **-f**. Al iniciar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configuración mínima, el servidor utilizará automáticamente el modo de usuario único.  
  
 Tenga en cuenta los siguientes aspectos cuando inicie una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de configuración mínima:  
  
-   Solo se podrá conectar un usuario y no se ejecutará el proceso `CHECKPOINT`.  
  
-   El acceso remoto y la lectura anticipada quedan deshabilitadas.  
  
-   No se ejecutan los procedimientos almacenados de inicio.  

-   `tempdb` se configura con el tamaño más pequeño posible.

-   La auditoría se deshabilitará pero todavía se puede emitir la auditoría de DDL. En la práctica, **-m** debe ser suficiente para la mayoría de los casos que requieran la reconfiguración de la auditoría de SQL Server. Para obtener más información sobre la seguridad en la configuración de auditoría, vea [Auditoría en SQL Server](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/dd392015(v=sql.100)#security).
  
 Después de iniciar el servidor con la configuración mínima, debe modificar los valores que haga falta del servidor, detenerlo y después reiniciarlo.  
  
> [!IMPORTANT]  
>  Use la utilidad **sqlcmd** y la conexión de administrador dedicada (DAC) para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si utiliza una conexión típica, detenga el servicio del Agente SQL Server antes de conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de configuración mínima. En caso contrario, el servicio Agente SQL Server utilizará la conexión y, por tanto, la bloqueará.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar, detener o pausar el servicio del Agente SQL Server](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [Conexión de diagnóstico para administradores de bases de datos](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
