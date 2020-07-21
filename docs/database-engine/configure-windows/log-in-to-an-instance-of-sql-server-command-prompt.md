---
title: Iniciar sesión en una instancia de SQL Server (símbolo del sistema) | Microsoft Docs
description: Obtenga información sobre la utilidad sqlcmd. Vea cómo usarla en un símbolo del sistema para probar la conectividad a una instancia de SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0723a5d463757eca93dd7bacb1fc2b8fe232cdd8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772404"
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>Iniciar una sesión en una instancia de SQL Server (símbolo del sistema)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
## <a name="see-also"></a>Consulte también  
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)   
 [osql (utilidad)](../../tools/osql-utility.md)  
  
  
