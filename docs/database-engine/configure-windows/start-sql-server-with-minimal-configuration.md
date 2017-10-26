---
title: "Iniciar SQL Server con la configuración mínima | Microsoft Docs"
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 68750ae32638376ae20ccd04da3991eb88b7bd95
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="start-sql-server-with-minimal-configuration"></a>Iniciar SQL Server con la configuración mínima
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Si tiene problemas de configuración que impiden el inicio del servidor, puede iniciar una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la opción de inicio con configuración mínima. Esta es la opción de inicio **-f**. Al iniciar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configuración mínima, el servidor utilizará automáticamente el modo de usuario único.  
  
 Tenga en cuenta los siguientes aspectos cuando inicie una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de configuración mínima:  
  
-   Solo se podrá conectar un usuario y no se ejecutará el proceso `CHECKPOINT`.  
  
-   El acceso remoto y la lectura anticipada quedan deshabilitadas.  
  
-   No se ejecutan los procedimientos almacenados de inicio.  

-   `tempdb` se configura con el tamaño más pequeño posible.
  
 Después de iniciar el servidor con la configuración mínima, debe modificar los valores que haga falta del servidor, detenerlo y después reiniciarlo.  
  
> [!IMPORTANT]  
>  Use la utilidad **sqlcmd** y la conexión de administrador dedicada (DAC) para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si utiliza una conexión típica, detenga el servicio del Agente SQL Server antes de conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de configuración mínima. En caso contrario, el servicio Agente SQL Server utilizará la conexión y, por tanto, la bloqueará.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar, detener o pausar el servicio del Agente SQL Server](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [Conexión de diagnóstico para administradores de bases de datos](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  

