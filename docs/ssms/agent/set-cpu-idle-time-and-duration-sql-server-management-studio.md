---
description: Establecimiento de la duración y el tiempo de inactividad de la CPU
title: Establecimiento de la duración y el tiempo de inactividad de la CPU
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CPU [SQL Server], idle conditions
- time [SQL Server], CPU idle and duration
- duration of CPU idle [SQL Server]
- SQL Server Agent, CPU idle conditions
- idle time [SQL Server]
ms.assetid: 8647b465-d899-4cc7-9640-134a506d0a2e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 75670401aa4049c66083f0dce5bf4212e4f74f5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418081"
---
# <a name="set-cpu-idle-time-and-duration"></a>Establecimiento de la duración y el tiempo de inactividad de la CPU

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

En este tema se explica cómo definir la condición de inactividad de la CPU para el servidor en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. La definición de inactividad de la CPU influye en la forma en que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] responde a los eventos. Por ejemplo, supongamos que define la condición de inactividad de la CPU como el momento en que el uso de la CPU se sitúa por debajo del 10% y permanece en este nivel durante 10 minutos. En este caso, si ha definido trabajos que deben ejecutarse cuando la CPU del servidor alcance una condición de inactividad, estos trabajos se iniciarán cuando el uso de la CPU se sitúe por debajo del 10% y permanezca en este nivel durante 10 minutos. Si se trata de un trabajo que tiene consecuencias importantes sobre el rendimiento del servidor, es importante la forma en que define la condición de inactividad de la CPU.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-set-cpu-idle-time-and-duration"></a>Para establecer la duración y el tiempo de inactividad de la CPU  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Haga clic con el botón derecho en el **Agente SQL Server**, haga clic en **Propiedades**y seleccione la página **Avanzadas** .  
  
3.  En **Condición de CPU inactiva**, haga lo siguiente:  
  
    -   Active la opción **Definir condición de CPU inactiva**.  
  
    -   Especifique un porcentaje para el cuadro **El promedio de uso de la CPU baja de** (para todas las CPU). Esto establece el nivel de uso por debajo del cual debe situarse la CPU para que se considere inactiva.  
  
    -   Especifique un número de segundos para el cuadro **Y permanece por debajo durante** . Esto establece la duración del uso mínimo de la CPU para que ésta se considere inactiva.  
  
