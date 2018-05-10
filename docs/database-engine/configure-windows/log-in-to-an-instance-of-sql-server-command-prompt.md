---
title: Iniciar sesión en una instancia de SQL Server (símbolo del sistema) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8e9f93fceb417676da4e67b273a822ce9815d6c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>Iniciar una sesión en una instancia de SQL Server (símbolo del sistema)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Ver también  
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)   
 [osql (utilidad)](../../tools/osql-utility.md)  
  
  
