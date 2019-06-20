---
title: Dar formato a las direcciones de buscapersonas para alertas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 535ae5f92fea0222468ed64f567154495e329a61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63044217"
---
# <a name="format-pager-addresses-for-alerts"></a>Dar formato a las direcciones de buscapersonas para alertas
  En este tema se describe cómo dar fomato a las direcciones del buscapersonas de las alertas del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para dar formato a direcciones del buscapersonas, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ver información acerca de una alerta. A otros usuarios debe concederse el rol fijo de base de datos **SQLAgentOperatorRole** en la base de datos **msdb** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-format-pager-addresses"></a>Para dar formato a direcciones del buscapersonas  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la alerta que desea enviar a un buscapersonas.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En **Seleccionar una página**, seleccione **Sistema de alerta**.  
  
4.  En los cuadros **Línea Para** y **Línea CC** del campo **Formato de dirección para correo electrónico de buscapersonas** , escriba el prefijo o el sufijo de la dirección del buscapersonas. La dirección del buscapersonas real del operador se inserta cuando se envía una notificación.  
  
5.  En el cuadro **Asunto** , escriba el prefijo o el sufijo de la línea del asunto.  
  
6.  Active la casilla **Incluir cuerpo del mensaje en la notificación** para incluir todo el mensaje de correo electrónico en el mensaje del buscapersonas (en vez de incluir solo la línea del asunto).  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  
  
