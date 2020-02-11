---
title: Ver información sobre una alerta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c5567abc0893bd183c2468f82278a014e2005113
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211292"
---
# <a name="view-information-about-an-alert"></a>Ver información acerca de una alerta
  En este tema se describe cómo ver información [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acerca de las [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] alertas del [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] agente [!INCLUDE[tsql](../../includes/tsql-md.md)]en mediante o.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver información acerca de una alerta, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ver información acerca de una alerta. A otros usuarios debe concederse el rol fijo de base de datos **SQLAgentOperatorRole** en la base de datos **msdb** .  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-alert"></a>Para ver información acerca de una alerta  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor en el que desea ver información acerca de una alerta.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Alertas** .  
  
4.  Haga clic con el botón derecho en la alerta que tiene la información que desea ver y seleccione **Propiedades**.  
  
     Para obtener más información sobre las opciones disponibles contenidas en el cuadro de diálogo _alert_name_**propiedades de alerta** , consulte:  
  
    -   [Propiedades de alerta-nueva alerta &#40;página general&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
    -   [Propiedades de alerta-nueva página de respuesta de &#40;de alerta&#41;](alert-properties-new-alert-response-page.md)  
  
    -   [Propiedades de alerta: nueva página de opciones de &#40;de alertas&#41;](alert-properties-new-alert-options-page.md)  
  
    -   [Propiedades de alerta &#40;página historial&#41;](alert-properties-history-page.md)  
  
5.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-information-about-an-alert"></a>Para ver información acerca de una alerta  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
 Para obtener más información, vea [sp_help_alert &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-help-alert-transact-sql).  
  
  
