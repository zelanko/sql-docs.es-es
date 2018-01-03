---
title: Dar de alta un servidor de destino en un servidor maestro | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc92c1f5c408d2001e469cc83658321098e40bd1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Dar de alta un servidor de destino en un servidor maestro
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo agregar servidores de destino a una configuración de administración multiservidor. Ejecute este procedimiento en el servidor maestro. en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)]u Objetos de administración de SQL Server (SMO).  
  
Para información sobre cómo la cuenta de Windows usada para el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] afecta a un entorno multiservidor, consulte [Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md).  
  
El cifrado SSL (Capa de sockets seguros) y la validación de certificados completos se habilita para las conexiones entre los servidores maestros y los servidores de destino de forma predeterminada. Para más información, [Establecer opciones de cifrado en servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
**En este tema**  
  
-   **Para dar de alta un servidor de destino, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Para dar de alta un servidor de destino  
  
1.  En el **Explorador de objetos**, expanda un servidor que esté configurado como servidor maestro.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración de multiservidor**y, luego, en **Agregar servidores de destino**.  
  
3.  Complete el Asistente para establecer servidor de destino, que le guía a través del proceso.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Para dar de alta un servidor de destino  
  
1.  Use el procedimiento almacenado **sp_msx_enlist** .  Para más información, consulte [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f).  
  
## <a name="see-also"></a>Ver también  
[Administración automatizada en una empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
