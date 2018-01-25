---
title: "Cambiar la seguridad de las transacciones en una sesión de creación de reflejo de la base de datos (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 828a9d7c3bbb7ee46029bcc6bb81dab4477bcd6a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>Cambiar la seguridad de las transacciones en una sesión de creación de reflejo de la base de datos (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La seguridad de las transacciones es el atributo que controla el modo operativo de la sesión. No obstante, el propietario de la base de datos puede cambiar la seguridad de las transacciones en cualquier momento. De forma predeterminada, el nivel de seguridad de las transacciones está establecido en FULL (modo operativo sincrónico).  
  
 Si se desactiva la seguridad de las transacciones, la sesión cambia al modo operativo asincrónico, lo que maximiza el rendimiento. Si la base de datos principal no está disponible, la base de datos reflejada se detiene pero está disponible como base de datos en espera semiactiva (la conmutación por error requiere forzar el servicio, con una posible pérdida de datos).  
  
### <a name="to-turn-on-transaction-safety"></a>Para activar la seguridad de las transacciones  
  
1.  Conéctese al servidor principal.  
  
2.  Escriba la instrucción Transact-SQL siguiente:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     donde *\<base de datos>* es el nombre de la base de datos reflejada.  
  
### <a name="to-turn-off-transaction-safety"></a>Para desactivar la seguridad de las transacciones  
  
1.  Conéctese al servidor principal.  
  
2.  Emita la instrucción siguiente:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     donde *\<base de datos>* es la base de datos reflejada.  
  
## <a name="see-also"></a>Ver también  
 [Reflejo de la base de datos ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  
