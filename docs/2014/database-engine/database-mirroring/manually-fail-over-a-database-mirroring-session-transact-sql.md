---
title: Realizar una conmutación por error manualmente de una sesión de creación de reflejo de la base de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a78dc1647095f5ef444713a7ad46f12e45fc7c65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106198"
---
# <a name="manually-fail-over-a-database-mirroring-session-transact-sql"></a>Realizar una conmutación por error manualmente de una sesión de creación de reflejo de la base de datos (Transact-SQL)
  Cuando la base de datos reflejada se sincroniza (es decir, cuando el estado de la base de datos es SYNCHRONIZED), el propietario de la base de datos puede iniciar una conmutación por error manual en el servidor reflejado. La conmutación por error manual solo se puede iniciar desde el servidor principal.  
  
### <a name="to-manually-fail-over-a-database-mirroring-session"></a>Para realizar una conmutación por error manual en una sesión de creación de reflejo de la base de datos  
  
1.  Conéctese al servidor principal.  
  
2.  Establezca el contexto de la base de datos en la base de datos **maestra** :  
  
     `USE master;`  
  
3.  Emita la siguiente instrucción en el servidor principal:  
  
     [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) *database_name* SET PARTNER FAILOVER, donde *database_name* es la base de datos reflejada.  
  
     Esto inicia una transición inmediata del servidor reflejado hacia el rol principal.  
  
 En el principal antiguo, los clientes se desconectan de la base de datos y las transacciones en curso se revierten.  
  
> [!NOTE]  
>  Las transacciones que se han preparado mediante el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] pero que aún no están confirmadas en el momento de la conmutación por error se consideran anuladas tras la conmutación por error de la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Reflejo de la base de datos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Realizar manualmente la conmutación por error de una sesión de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  
