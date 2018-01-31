---
title: "Ver información sobre una alerta | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69ce81f865d3b01d2316f913317fe63505b49aa9
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="view-information-about-an-alert"></a>Ver información acerca de una alerta
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo ver información sobre las alertas del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para ver información acerca de una alerta, utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ver información acerca de una alerta. A otros usuarios debe concederse el rol fijo de base de datos **SQLAgentOperatorRole** en la base de datos **msdb** .  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-alert"></a>Para ver información acerca de una alerta  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor en el que desea ver información acerca de una alerta.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Alertas** .  
  
4.  Haga clic con el botón derecho en la alerta que tiene la información que desea ver y seleccione **Propiedades**.  
  
    Para obtener más información sobre las opciones disponibles presentes en el cuadro de diálogo *Propiedades de la alerta***nombre_de_alerta*, consulte:  
  
    -   [Propiedades de alerta - Nueva alerta &#40;Página General&#41;](../../ssms/agent/alert-properties-new-alert-general-page.md)  
  
    -   [Propiedades de alerta - Nueva alerta &#40;Página Respuesta&#41;](../../ssms/agent/alert-properties-new-alert-response-page.md)  
  
    -   [Propiedades de alerta - Nueva alerta &#40;Página Opciones&#41;](../../ssms/agent/alert-properties-new-alert-options-page.md)  
  
    -   [Propiedades de alerta &#40;Página Historial&#41;](../../ssms/agent/alert-properties-history-page.md)  
  
5.  Cuando termine, haga clic en **Aceptar**.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-view-information-about-an-alert"></a>Para ver información acerca de una alerta  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- reports information about the Demo: Sev. 25 Errors alert  
    -- This example assumes that the 'Demo: Sev. 25 Errors' alert exists.  
    USE msdb ;  
    GO  
  
    EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors'  
    GO  
    ```  
  
Para más información, consulte [sp_help_alert (Transact-SQL)](http://msdn.microsoft.com/en-us/850cef4e-6348-4439-8e79-fd1bca712091).  
  
