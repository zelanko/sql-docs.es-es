---
title: Realizar una conmutación por error manualmente de una sesión de creación de reflejo de la base de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 10b4ac5e992e39c9c45f82ab0a1c720ec759100a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703744"
---
# <a name="manually-fail-over-a-database-mirroring-session-transact-sql"></a>Realizar una conmutación por error manualmente de una sesión de creación de reflejo de la base de datos (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Cuando la base de datos reflejada se sincroniza (es decir, cuando el estado de la base de datos es SYNCHRONIZED), el propietario de la base de datos puede iniciar una conmutación por error manual en el servidor reflejado. La conmutación por error manual solo se puede iniciar desde el servidor principal.  
  
### <a name="to-manually-fail-over-a-database-mirroring-session"></a>Para realizar una conmutación por error manual en una sesión de creación de reflejo de la base de datos  
  
1.  Conéctese al servidor principal.  
  
2.  Establezca el contexto de la base de datos en la base de datos **maestra** :  
  
     **USE master;**  
  
3.  Emita la siguiente instrucción en el servidor principal:  
  
     [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md) *database_name* SET PARTNER FAILOVER, donde *database_name* es la base de datos reflejada.  
  
     Esto inicia una transición inmediata del servidor reflejado hacia el rol principal.  
  
 En el principal antiguo, los clientes se desconectan de la base de datos y las transacciones en curso se revierten.  
  
> [!NOTE]  
>  Las transacciones que se han preparado mediante el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] pero que aún no están confirmadas en el momento de la conmutación por error se consideran anuladas tras la conmutación por error de la base de datos.  
  
## <a name="see-also"></a>Ver también  
 [Reflejo de la base de datos ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [Realizar manualmente la conmutación por error de una sesión de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  
