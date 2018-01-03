---
title: Dar formato a las direcciones de buscapersonas para alertas | Microsoft Docs
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
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b64ab3bad4cb7264a95a6d9fd3045f2c3748aee
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="format-pager-addresses-for-alerts"></a>Format Pager Addresses for Alerts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo dar formato a las direcciones del buscapersonas de las alertas del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para dar formato a direcciones del buscapersonas, utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ver información acerca de una alerta. A otros usuarios debe concederse el rol fijo de base de datos **SQLAgentOperatorRole** en la base de datos **msdb** .  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-format-pager-addresses"></a>Para dar formato a direcciones del buscapersonas  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la alerta que desea enviar a un buscapersonas.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En **Seleccionar una página**, seleccione **Sistema de alerta**.  
  
4.  En los cuadros **Línea Para** y **Línea CC** del campo **Formato de dirección para correo electrónico de buscapersonas** , escriba el prefijo o el sufijo de la dirección del buscapersonas. La dirección del buscapersonas real del operador se inserta cuando se envía una notificación.  
  
5.  En el cuadro **Asunto** , escriba el prefijo o el sufijo de la línea del asunto.  
  
6.  Active la casilla **Incluir cuerpo del mensaje en la notificación** para incluir todo el mensaje de correo electrónico en el mensaje del buscapersonas (en vez de incluir solo la línea del asunto).  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  
