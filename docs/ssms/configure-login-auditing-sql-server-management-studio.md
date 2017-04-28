---
title: "Configurar la auditoría de inicio de sesión (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], logins
- logins [SQL Server], auditing
ms.assetid: 16961116-57ac-4eef-8037-791b26ade548
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1153704ae4f345436c05a37cae98a522ef991ba1
ms.lasthandoff: 04/11/2017

---
# <a name="configure-login-auditing-sql-server-management-studio"></a>Configurar la auditoría de inicio de sesión (SQL Server Management Studio)
En este tema se describe cómo configurar la auditoría de inicio de sesión en [!INCLUDE[ssCurrent](../includes/sscurrent_md.md)] para supervisar la actividad de inicio de sesión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)]. Se puede configurar para que escriba en el registro de errores cuando se produzcan los eventos que se indican a continuación.  
  
-   Inicios de sesión erróneos  
  
-   Inicios de sesión correctos  
  
-   Inicios de sesión correctos y erróneos  
  
Para que esta opción surta efecto, debe reiniciar [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] .  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-configure-login-auditing"></a>Para configurar la auditoría de inicio de sesión  
  
1.  En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)], conéctese a una instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)] con el Explorador de objetos.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en el nombre del servidor y, después, haga clic en **Propiedades**.  
  
3.  En la página **Seguridad** , bajo **Auditoría de inicio de sesión** , haga clic en la opción que desee y cierre la página **Propiedades del servidor** .  
  
4.  En el Explorador de objetos, haga clic con el botón derecho en el nombre del servidor y, luego, haga clic en **Reiniciar**.  
  

