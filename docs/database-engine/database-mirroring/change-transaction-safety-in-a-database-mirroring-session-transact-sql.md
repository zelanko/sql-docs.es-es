---
title: Cambiar la seguridad de las transacciones en una sesión de creación de reflejo de la base de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 250d077becd2261c98f14f062b3d490a71f7a5fe
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35311484"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>Cambiar la seguridad de las transacciones en una sesión de creación de reflejo de la base de datos (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La seguridad de las transacciones es el atributo que controla el modo operativo de la sesión. No obstante, el propietario de la base de datos puede cambiar la seguridad de las transacciones en cualquier momento. De forma predeterminada, el nivel de seguridad de las transacciones está establecido en FULL (modo operativo sincrónico).  
  
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
  
  
