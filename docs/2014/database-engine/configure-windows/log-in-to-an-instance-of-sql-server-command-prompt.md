---
title: Iniciar sesión en una instancia de SQL Server (símbolo del sistema) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 496f9c15e344577918045fe8cabca6f901019a3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282061"
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>Iniciar una sesión en una instancia de SQL Server (símbolo del sistema)
  En este tema se describe cómo probar la conectividad a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mediante la utilidad **sqlcmd** .  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-log-in-to-the-default-instance-of-sql-server"></a>Para iniciar una sesión en la instancia predeterminada de SQL Server  
  
1.  En el símbolo del sistema, escriba el siguiente comando para conectarse mediante la autenticación de Windows:  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### <a name="to-log-in-to-a-named-instance-of-sql-server"></a>Para iniciar una sesión en una instancia con nombre de SQL Server  
  
1.  En el símbolo del sistema, escriba el siguiente comando para conectarse mediante la autenticación de Windows:  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## <a name="see-also"></a>Vea también  
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)   
 [osql (utilidad)](../../tools/osql-utility.md)  
  
  
