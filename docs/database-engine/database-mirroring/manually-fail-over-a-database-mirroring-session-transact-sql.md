---
title: "Realizar una conmutaci&#243;n por error manualmente de una sesi&#243;n de creaci&#243;n de reflejo de la base de datos (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conmutación por error [SQL Server], creación de reflejo de la base de datos"
  - "conmutación por error manual [SQL Server]"
  - "creación de reflejo de la base de datos [SQL Server], conmutación por error"
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
caps.latest.revision: 32
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 32
---
# Realizar una conmutaci&#243;n por error manualmente de una sesi&#243;n de creaci&#243;n de reflejo de la base de datos (Transact-SQL)
  Cuando la base de datos reflejada se sincroniza (es decir, cuando el estado de la base de datos es SYNCHRONIZED), el propietario de la base de datos puede iniciar una conmutación por error manual en el servidor reflejado. La conmutación por error manual solo se puede iniciar desde el servidor principal.  
  
### Para realizar una conmutación por error manual en una sesión de creación de reflejo de la base de datos  
  
1.  Conéctese al servidor principal.  
  
2.  Establezca el contexto de la base de datos en la base de datos **maestra** :  
  
     **USE master;**  
  
3.  Emita la siguiente instrucción en el servidor principal:  
  
     [ALTER DATABASE](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md) *database_name* SET PARTNER FAILOVER, donde *database_name* es la base de datos reflejada.  
  
     Esto inicia una transición inmediata del servidor reflejado hacia el rol principal.  
  
 En el principal antiguo, los clientes se desconectan de la base de datos y las transacciones en curso se revierten.  
  
> [!NOTE]  
>  Las transacciones que se han preparado mediante el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] pero que aún no están confirmadas en el momento de la conmutación por error se consideran anuladas tras la conmutación por error de la base de datos.  
  
## Vea también  
 [Reflejo de la base de datos ALTER DATABASE &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [Realizar manualmente la conmutación por error de una sesión de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  