---
title: Designar un servidor (SQL Server Management Studio) de reenvío de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6d8e24883fe71463b4c03e4caefc1735cf794bc1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167275"
---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designate an Events Forwarding Server (SQL Server Management Studio)
  En este tema se describe cómo designar un servidor al que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reenvía eventos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Observe que el reenvío de eventos se aplica a los eventos reenviados entre servidores, no a los eventos reenviados entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedadas en un único equipo. Tenga en cuenta también que para recibir eventos reenviados, el servidor de administración de alertas debe ser una instancia predeterminada de SQL Server.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para designar un servidor de reenvío de eventos. utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>Para designar un servidor de reenvío de eventos  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor desde el que desea reenviar eventos a otro servidor.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server –***nombre_de_servidor*, en **Seleccionar una página**, seleccione **Avanzadas**.  
  
4.  En **Reenvío de eventos de SQL Server**, active la casilla **Reenviar eventos a otro servidor** .  
  
5.  En la lista **Servidor** , seleccione un servidor y, a continuación, en **Eventos**, realice una de las selecciones siguientes:  
  
    -   Seleccione la opción **No controlados** para reenviar solo los eventos que no han sido controlados por alertas locales.  
  
    -   Seleccione la opción **Todos los eventos** para reenviar todos los eventos, independientemente de si han sido controlados o no por alertas locales.  
  
6.  En la lista **Si el evento tiene una gravedad de o por encima de** , haga clic en el nivel de gravedad a partir del cual se reenvían los eventos al servidor seleccionado.  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  
  
